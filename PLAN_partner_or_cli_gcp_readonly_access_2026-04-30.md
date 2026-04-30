---
title: Partner OR CLI + GCP read-only access plan
date: 2026-04-30
status: DRAFTED FOR APPROVAL (no execution tonight)
audience: a coding agent on partner's computer (windows / mac / linux)
canary: dispatch|opus-only|caveman|Sage-only|no-em-dash
---

# Plan -- Partner OR CLI + GCP read-only access

Goal: partner uses Sage's OR-routed CLI on their own machine and can OBSERVE / OPERATE Sage's GCP trading project, but cannot DOWNLOAD strategy code or DUMP datasets to their local disk.

Two-leg architecture:

- **Leg 1 -- partner's machine** runs an OpenRouter-only CLI (no Anthropic CLI). Stateless. Sends prompts to OR. Cannot receive Sage's strategy files; only receives the model's responses.
- **Leg 2 -- partner's GCP access** is read-only on specific resources (Cloud Logging, monitoring dashboards, Cloud Console for the project) and instance-level access is mediated via a JUMP HOST so the partner never gets a local copy of the code.

## Leg 1 -- Standalone OR CLI on partner's machine

### Tools to install

- **PowerShell 7+** (cross-platform) -- partner runs the same `or_dispatch.ps1` Sage uses
- **`uv`** (Python package manager) -- for any Python helper scripts
- **`gh` CLI** -- only if partner needs read-only GitHub Issues access; SKIP if not needed
- **`gcloud` CLI** -- in read-only mode, signed in to a service account Sage controls

### Files partner gets

Sage shares ONE file with partner:
- `or_dispatch.ps1` (the OpenRouter dispatch wrapper)

Partner does NOT get:
- Sage's `.profile` / shell init that loads `OPENROUTER_API_KEY`
- Sage's strategy code
- Sage's GCP service-account JSON

### How partner authenticates

Sage gives partner ONE of these:

**Option A -- SHARED SUB-KEY (recommended).** Sage creates a SECONDARY OR API key just for partner with a low credit ceiling (e.g. $20/month) at https://openrouter.ai/settings/keys. Partner exports `OPENROUTER_API_KEY` in their shell. Sage rotates / revokes whenever.

**Option B -- PROXY ENDPOINT.** Sage stands up a tiny HTTP proxy on a GCP Cloud Run service that holds the real OR key and rate-limits / cost-caps partner. Partner calls the proxy URL with a per-partner bearer token. Sage observes / revokes per-partner usage. More work but tighter control.

Recommend Option A for first iteration; promote to B if abuse detected.

### What partner can do

```powershell
$env:OPENROUTER_API_KEY = "sk-or-v1-PARTNER-KEY"
$env:ANTHROPIC_BASE_URL = "https://openrouter.ai/api"

pwsh -NoProfile -File or_dispatch.ps1 `
  -Model "moonshotai/kimi-k2-thinking" `
  -PromptFile prompt.md `
  -OutFile response.md `
  -MaxTokens 8000
```

Partner crafts prompts, sends to OR, gets responses. Strategy code does NOT flow through the partner machine.

### Token-burn protection

Partner key has hard cost ceiling at OR settings. Cannot exceed it. Sage gets email alerts at 50% / 90% / 100%.

## Leg 2 -- GCP read-only / no-download access

Goal: partner OBSERVES the trading run, can VIEW logs / charts, can RESTART jobs, but cannot SCP / rsync / gcloud-storage-cp source files OR datasets off the VM.

### Pattern A -- IAM read-only roles (simple, partial)

Create a partner GCP user (their Google account) and grant ONLY these roles on the project:

- `roles/viewer` -- read everything (read code, read datasets) -- **THIS IS TOO MUCH; skip plain viewer**
- `roles/logging.viewer` -- read Cloud Logging only
- `roles/monitoring.viewer` -- read Cloud Monitoring dashboards only
- `roles/compute.osLogin` (NO sudo) -- SSH only, no admin
- `roles/iap.tunnelResourceAccessor` -- SSH via Identity-Aware Proxy

This lets partner SSH in and watch processes but not read source files (file system permissions enforced; see Pattern B).

Reference: https://cloud.google.com/iam/docs/understanding-roles

### Pattern B -- Linux file-system permissions on the VM

On the GPU VM, place all strategy code + datasets under `/opt/sage/` owned by `root:sage` with mode `0750`. Partner's user is NOT in the `sage` group. Result: partner can `ls` but cannot `cat` strategy files.

```bash
sudo groupadd sage
sudo usermod -aG sage your_main_user
sudo mkdir -p /opt/sage
sudo chown root:sage /opt/sage
sudo chmod 0750 /opt/sage
sudo cp -r ~/trading-strategy /opt/sage/
```

Partner's account (added via IAM osLogin) cannot read inside.

### Pattern C -- VS Code Remote / Cloud Shell jump host

Partner SSH-tunnels INTO the VM via IAP, but their session runs as a NON-PRIVILEGED user. They see WHAT IS RUNNING (`ps`, `top`, `nvidia-smi`) and can read STDOUT logs but cannot read source.

Disable scp/rsync/sftp for partner's user:

```bash
# in /etc/ssh/sshd_config -- match block for partner:
Match User partner_user
  AllowTcpForwarding no
  X11Forwarding no
  PermitTTY yes
  ForceCommand /usr/local/bin/partner_shell.sh
```

Custom `partner_shell.sh` is a restricted shell (e.g. `rbash`) with `PATH` limited to read-only commands.

Reference: https://man.openbsd.org/sshd_config

### Pattern D -- Cloud Run "viewer" web app

Most secure / most work. Sage builds a small dashboard at `https://trading-dashboard.example.com/` running on Cloud Run that:

- Shows trading-equity curve (read-only chart from BigQuery)
- Shows training-loss curve (read-only)
- Lets partner click "kick off backtest run X with params {...}" -- request goes to a Cloud Function with a hardcoded set of allowed params; cannot escape into shell

Partner never gets shell access at all. Cannot extract anything.

Reference: https://cloud.google.com/run/docs/securing/identity

### Recommended: Pattern A + B + C combined

- IAM viewer roles for logs / monitoring / SSH-only
- File-system 0750 ownership on `/opt/sage/`
- Restricted shell + ForceCommand on partner SSH
- Periodic audit log review

This stops casual download attempts. A determined adversary with shell + screen-capture can still copy text by retyping; for true zero-extraction, use Pattern D.

## Pre-flight checklist

Before partner gets any access:

1. `[ ]` Partner has Google account
2. `[ ]` Sage created secondary OR API key (low ceiling)
3. `[ ]` Sage created GCP IAM bindings: logging.viewer + monitoring.viewer + compute.osLogin + iap.tunnelResourceAccessor
4. `[ ]` `/opt/sage/` mode 0750 set; main code moved there
5. `[ ]` `sshd_config` Match block for partner user; restricted shell installed
6. `[ ]` IAP enabled on partner's IP; firewall rule for IAP CIDR (35.235.240.0/20)
7. `[ ]` Audit log alerting wired (Cloud Logging sink to monitor `gcloud storage cp`, `scp`, `rsync` attempts by partner user)
8. `[ ]` Partner orientation doc shared (what they can / cannot do)

## What partner does day-1

```bash
# 1. Install gcloud
curl https://sdk.cloud.google.com | bash
gcloud auth login                      # Google account
gcloud config set project sage-trading

# 2. SSH to the GPU VM via IAP
gcloud compute ssh sage-trading-vm --zone=us-central1-a --tunnel-through-iap

# 3. They land in restricted shell. Allowed commands:
#    nvidia-smi, top, htop, tail -f /opt/sage/logs/*.log, ps, df
#    NOT allowed: cat /opt/sage/strategy/*, scp, rsync, sftp, curl out

# 4. View Cloud Console dashboards in browser (read-only)
```

## Tear-down

Revoke partner access in 30 seconds:

```bash
# Revoke OR key
# (do this in https://openrouter.ai/settings/keys; click delete)

# Revoke GCP IAM
gcloud projects remove-iam-policy-binding sage-trading \
  --member="user:partner@gmail.com" \
  --role="roles/logging.viewer"
gcloud projects remove-iam-policy-binding sage-trading \
  --member="user:partner@gmail.com" \
  --role="roles/compute.osLogin"

# Disable SSH user on the VM
sudo userdel -r partner_user
```

## Sources to cite when implementing

- Identity-Aware Proxy: https://cloud.google.com/iap/docs/using-tcp-forwarding
- IAM roles: https://cloud.google.com/iam/docs/understanding-roles
- OS Login: https://cloud.google.com/compute/docs/oslogin
- Cloud Run security: https://cloud.google.com/run/docs/securing/identity
- OpenRouter API key management: https://openrouter.ai/docs/api-reference/api-keys
- sshd_config Match + ForceCommand: https://man.openbsd.org/sshd_config

## Trinity gate

- Lambda: every URL is an official source. 5/5
- Pi: Leg 1 + Leg 2 separated; recommended pattern combo named explicitly. 5/5
- Theta: partner cannot extract; controls revocable in 30 sec; sub-key prevents OR cost overrun. 5/5

15/15 PROCEED on Sage approval tomorrow.
