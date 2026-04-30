---
title: Desktop Bundle Handoff -- complete pushable-artifact inventory + soft-publish workflow
date: 2026-04-30
audience: Sage in Claude Desktop (Projects + Research mode) reviewing public-flip candidacy
purpose: Final candidacy push -- update LinkedIn + Resume + flip a few public repos so Sage applies with worth-it candidate signal
canary: dispatch|opus-only|caveman|Sage-only|no-em-dash|15=PROCEED|100%=1-token
---

# Desktop Bundle Handoff -- 2026-04-30

## ANSWER THIS PROMPT FIRST (Sage's verbatim morning ask)

> "great let's go back and check for seamless handoff - i will clear session - it is morning and we will focus on ensuring github is good with help of the desktop claude chat / research -> after clear we will be reviewing the published private and review the pushable artificat inventory as well as finalizing my resume and linked in using the PE we found. Since the repos aren't public - i want to you to prepare a desktop handoff that is a bundle of all the work on github and all the workfound that can be pushed. Cover everything and include format details, licensing, the contents of each repo, the function, does it work, what does it do etc. a basic, but detailed sufficient for the chat to ask to publish things... what we can do is soft-publish to public a few at a time, have the chat bot look at it, recommend how we should fix it, you will fix it, then it will check it. I want to give it information and an overview. use sub agents openrouter to do all this but i want opus to take the time to write the plans for them and to ensure that they can be evaluated by a zero context agent after, which it should do. send multiple agents to check and provide more and more info. also i don't see the breakdown i asked for open brain - was that in the publishable artifact inventory from last night? I am looking at it and it looks good. We want to reduce the amount of extra work we need to get us public faciing repos that show my candidacy. we can send out linkedin announcemnet after we update my profile and resume and then we'll apply. we should have most of what we need."

Desktop's job is to consume this bundle, decide which repos to flip public first, and supervise the soft-publish iteration loop with the CLI.

## CONFIDENCE LOOP (system_directive_protocol)

"100% = 1 token" -- spend MORE tokens on certainty BEFORE writing or recommending. For every claim Desktop makes about a repo, every URL, every LICENSE, every content-fit assertion: cite a source (gh api output, file path, git log line). If something is UNKNOWN, say UNKNOWN. Do not fabricate.

3-category Confidence Loop runs at every decision point:
- **Architecture & State:** what's actually on GitHub right now? what's local? what's the delta?
- **Evidence & Sourcing:** is each public-flip claim grounded in an inspectable artifact?
- **Intent & Constraint:** what does Sage want this public-flip to achieve, and at what cost / risk?

## What Desktop receives (this handoff = entry point)

```
HANDOFF_DESKTOP_BUNDLE_2026-04-30.md  <-- THIS FILE; entry point
```

Plus these COMPANION files Desktop loads as project sources:

### Application materials (CRITICAL for AM)
- `wiki/anthropic_application/` -- the entire folder; has resume v3 + v4 + v4_RC + LinkedIn draft v1 + LinkedIn UPDATE STEPS + OPEN_Q_ANSWERS_PREFILLED + positioning_frame
- `HANDOFF_DESKTOP_2026-04-30_application_finalize.md` (root) -- 3 deliverables for AM (Resume v5 + LinkedIn final + Greenhouse form fill)
- `HANDOFF_DESKTOP_PROJECT_PATHS_2026-04-30.md` (root) -- curated path-list for Desktop project loading

### Final closure handoffs (read SECOND on Desktop entry)
- `HANDOFF_2026-04-30_FINAL_SESSION_CLOSURE.md` (root) -- TLDR + done + in-flight + open matters + next-5
- `wiki/handoffs/HANDOFF_2026-04-30_cli_session_close_state.md` -- prior CLI checkpoint
- `wiki/handoffs/HANDOFF_2026-04-30_session_close_state.md` -- parallel Opus orchestrator close (book-library, OR dispatch infra, Obsidian RAG, TurboQuant, modular categorization, agentic-activity-review)

### Research artifacts (CRITICAL for repo-by-repo decisions)
- `wiki/research/publishable_artifact_inventory_2026-04-29.md` -- 12-category sweep with ~80 publishable items, kimi+deepseek paired-doer, includes the OpenBrainLM breakdown Sage asked about (CATEGORY_2 Trinity_PEL + CATEGORY_4 Skills + CATEGORY_3 Plugins all reference OpenBrainLM components)
- `wiki/research/open_source_candidates_2026-04-29.md` -- 7 standalone-repo candidates Sage could ship from existing components (claude-code-plugin-starter, prompt-fragment-library, notebooklm-mcp-integration-bridge, openrouter-dispatch-harness, agentic-bundle-specification, concept-research-synthesizer, multi-agent-swarm-orchestrator)
- `wiki/research/autoresearcher_loop_pattern_2026-04-30.md` -- Karpathy-style summary of the 3x sequential context-passing pattern (locked in as default for OR dispatches)
- `wiki/research/CORPUS_MAP_2026-04-29.md` -- structured corpus map for OR sweep doers

### Per-repo metadata (when KIMI_per_repo_metadata_bundle_output_2026-04-30 lands)
- `wiki/handoffs/dispatches/KIMI_per_repo_metadata_bundle_output_2026-04-30.md` -- THE table Desktop uses for soft-publish decisions; each of 51 repos with format / license / content / does-it-work / public-fit / rename map / first-wave-public-flip order

### Workstream-specific handoffs (Sage explicitly named these)
- `wiki/handoffs/HANDOFF_2026-04-29_session_A_github_push.md` -- private push tasks
- `wiki/handoffs/HANDOFF_2026-04-29_session_B_fatex_sunset.md` -- FATExDAO sunset workstream
- `wiki/handoffs/HANDOFF_2026-04-29_session_C_trading_collection.md` -- trading collection workstream
- `wiki/handoffs/HANDOFF_2026-04-30_modular_categorization_design.md` -- WS-5 cross-topic categorization (parallel Opus session)
- `wiki/handoffs/dispatches/` -- entire directory; ~30+ kimi/deepseek/minimax research outputs from 2026-04-29 + 2026-04-30 (DISPATCH_INDEX_2026-04-30.md inside the staging-index repo lists them all)

### Workflow + plans (read SELECTIVELY when relevant)
- `wiki/handoffs/PLAN_partner_or_cli_gcp_readonly_access_2026-04-30.md` -- partner OR-CLI + GCP read-only-no-extract plan
- `nvidia_gcp_vm_setup_plan/` -- 11-file two-track NVIDIA + GCP plan
- `NOTES_FOR_SAGE.md` (root) -- running blocked-decision log; every override Sage said in this session

## Soft-publish workflow (iterate, not big-bang)

The pattern Sage proposed -- short and good. Refined here.

### Step 1: Pick the candidate
Desktop reviews the per-repo metadata bundle (the kimi dispatch output above) and picks a TIER-1 first-wave candidate based on:
- HAS_CONTENT = YES
- DOES_IT_WORK = YES or LIKELY
- PUBLIC_FIT_RISK = NONE / LOW / MEDIUM
- CODENAME_RENAME = manageable (under 20 specific tokens)
- CANDIDACY_VALUE = high (showcases AI engineering / specification / governance / Trinity rubric / etc.)

Top 5 first-wave candidates (predicted from Sage's stated goals; subject to Desktop's review of the metadata bundle):
1. **`0SxD/trinity-dialectic`** -- standalone evaluation framework; small / clean / novel
2. **`0SxD/143-protocol`** -- 8-module operating directive; documentation-forward
3. **`0SxD/youtube-transcript-skill`** -- a ready-to-ship, smoke-tested skill; fastest possible flip
4. **`0SxD/sandbox-docs-plans`** -- master plan + install guide + superpowers references; demonstrates structured engineering planning
5. **`0SxD/nvidia-gcp-vm-setup-plan`** -- two-track NVIDIA + GCP plan; demonstrates infrastructure thinking

### Step 2: Soft-flip public for 30 minutes max
```
gh repo edit 0SxD/<repo> --visibility public --accept-visibility-change-consequences
```

### Step 3: Desktop ingests + analyzes
Desktop fetches the public URL, scans for:
- Codename leaks (143_protocol / 0sXai / PEL_GATE / pathos_ethos_logos / Austin B. Green / Mercor terms)
- License compliance (LICENSE file present? compatible with dependencies?)
- README quality (30-second test: outsider knows what / why / how within 30 seconds?)
- Security (no API keys, no .env, no secrets, no PII)
- Code-runs check (does the README's quickstart actually run? smoke test instructions clear?)

### Step 4: Desktop produces fix list
Concrete diff: rename items, README polish, license addition, scrub items, missing examples.

### Step 5: CLI applies fixes
Sage's next CLI session reads the Desktop fix list; applies via Edit / Write / git commits. Pushes to the same repo.

### Step 6: Desktop re-checks
Confirm fixes landed; verify no regressions.

### Step 7: Sage decides
PERMANENTLY public OR flip back to private. Per the Trinity gate: if Logos + Pathos + Ethos all >= 4 of 5, public stays. Else flip back.

### Step 8: Repeat for next candidate
Tier 2, Tier 3, etc. Sage controls cadence (one per day; one per week; whatever).

## How Desktop accesses the GitHub data (since repos are private)

Sage asked: "do we just make it public for 1-30 minutes and have it absord and process it to write my resume and linkedin?"

Three options Desktop chooses from:

### Option A: Soft-publish for ingestion (Sage's idea)
Flip repo public for 5-30 min. Desktop fetches via WebFetch. Sage flips back private. Risk: Google indexes the public window; revoking access does not unindex. MEDIUM RISK -- recommend SHORT windows (5 min max) and ONLY after confirming no PII / Mercor terms / real-name in repo.

### Option B: Local file system
Desktop's Project mode can read local files. Sage uploads (or points Desktop at) the local SandBoxSetup directory. Desktop reads file contents directly without GitHub. NO PUBLIC EXPOSURE. SAFEST. Limitation: Desktop's local-file access depends on Sage's setup; verify before relying.

### Option C: Manual paste
Sage tarballs a repo, uploads to Desktop project as a file. Desktop ingests. Slower but works for any repo regardless of GitHub state. Use for HIGH-PII repos (memory-export, personal-profile-builder-pack).

**Recommended pattern:** Option B for the bulk. Option A only for repos already 95% public-fit (trinity-dialectic, 143-protocol, youtube-transcript-skill). Option C for PII-heavy.

## OpenBrain breakdown (Sage said "i don't see the breakdown")

It LANDED. Two places:

### Place 1: `wiki/research/publishable_artifact_inventory_2026-04-29.md`
- CATEGORY_2 Trinity_PEL covers `OpenBrainLM_sandbox/openbrainlm/layers/pathos.py` and the trinity_dialectic standalone
- CATEGORY_3 Plugins references `OpenBrainLM_sandbox/sandbox/OpenBrain_Upgrades/Gemini_AntiGravity/...`
- CATEGORY_4 Skills covers `OpenBrainLM_sandbox/sagex/skills/` (audit-loop, brain-harness, coding-harness, edit-mode, notebooklm-research, research-gate, worktree-isolation)
- CATEGORY_6 Red-team / audit covers `OpenBrainLM_sandbox/sagex/hooks/` (9 hooks)

### Place 2: `wiki/handoffs/dispatches/KIMI_openbrainlm_component_inventory_output_2026-04-30.md`
The dedicated component-by-component breakdown -- per-file with OSS-equivalent comparison + Verdict (NOD / STANDARD / CUSTOM-NOVEL / VENDORED) + Standalone-repo-candidate flag.

Desktop reads BOTH for the OpenBrainLM evidence layer when deciding what to extract.

## Missing-from-0SxD / pushable-but-not-pushed (Sage flagged)

### 1 -- FATExDEX frontend (NOT on 0SxD)
Not yet on 0SxD GitHub. Local: `wiki/FxD 2026/` + `wiki/apps_ai_research/Research_FxD/`. Action: search for existing public FATExDEX/FATExDAO frontend repo (likely abandoned or on Dolomite GH). If found, fork to `0SxD/fatexdex-frontend-archive` (private). If not found, package the local FxD docs + designs as `0SxD/fatexdex-archive`.

### 2 -- FATExDAO Greenpaper (real, not the draft)
The local file `wiki/handoffs/FATEXDAO_greenpaper_raw.md` is a DRAFT. Sage referenced "the greenpaper fork on github either which is a big deal." Search GH for original published greenpaper. If found, fork to `0SxD/fatexdao-greenpaper-archive` (private). If not, package the local materials. CRITICAL: needs $80M public-disclosure decision from Sage before any public flip.

### 3 -- 2025-through-now trading work (NOT on 0SxD)
Local: `wiki/trading_bot_build_2025/` (huge), `wiki/nautilus_trader/` (with mlflow_config.py + sjm scripts + REAL TRAINED SJM models), `OpenBrainLM_sandbox/sandbox/NT_Bin_Sandbox/`. Action: per the trading-pipelines-shadow-inventory dispatch -- 4-tier split (trading-strategy-prod private, trading-shadow-runs private, trading-research-arm public-fit, trading-audit-pack private). Dispatch this morning to push these.

### 4 -- xD MakerDAO fork archive (NOT on 0SxD)
Local: `raw/other/xD_DAI_BUILD/xd-mvp/` -- 48 Solidity contracts. Per the FATExDEX/MakerDAO/DeFi-bot dispatch -- propose private repo `0SxD/xd-makerdao-fork-archive` (private; AGPL-3.0 inherited from MakerDAO).

## Subagent plan (Opus designs; OR fires; zero-context evaluator audits after)

The pattern Sage wants:
1. Opus writes the plan (this handoff + the per-repo metadata prompt)
2. OR-dispatched kimi/deepseek subagents execute (the metadata bundle dispatch fired, ID `bp...` per CLI logs)
3. Zero-context auditor (different model) grades the output

Already in flight:
- `wiki/handoffs/dispatches/KIMI_per_repo_metadata_bundle_2026-04-30.md` -- prompt
- `wiki/handoffs/dispatches/KIMI_per_repo_metadata_bundle_output_2026-04-30.md` -- output (when complete)

Next step (Desktop or next CLI fires):
- Zero-context auditor on the metadata bundle (deepseek-v4-pro):
  - Verifies every UNKNOWN actually unknown
  - Flags hallucinations (fabricated licenses, repo content claims that contradict what's actually pushed)
  - Re-ranks the first-wave-public-flip order
  - Outputs: `DEEPSEEK_per_repo_metadata_audit_output_2026-04-30.md`

## Workstreams Desktop helps drive

| Workstream | Desktop role |
|---|---|
| Resume v5 + LinkedIn final + Greenhouse form fill | PRIMARY -- finalize tomorrow |
| Soft-publish first-wave public-flip candidates | Iterate with CLI |
| LinkedIn announcement post | Draft after Resume v5 + first public flip |
| Apply to PE / FD / Anthropic JD ID 5159669008 / 5107121008 (resolve which) | After above |
| Answer Q10a-g Greenhouse logistics + Q15 strategy | Sage decides; Desktop drafts |
| Draft anonymous-character marketing (Trinity Auditor) | After application submitted |

## Open questions Desktop resolves

Sage decisions still required:
1. JD-ID: 5159669008 (resume v3/v4) vs 5107121008 (Drive PDF) -- which is current target?
2. Q10a-g Greenhouse logistics
3. Q15 application strategy (PE only / PE then FD / both)
4. $80M public-disclosure approval
5. Green Paper URL
6. Public-flip approval per repo (which goes first)
7. Real-name posture for first public flip (Sage / Austin Bennett Green / 0SxD only)
8. Soft-publish window length (5 min / 30 min / longer)
9. Desktop access pattern (A / B / C above)

## Cost discipline

- All heavy research has been OR-dispatched (kimi / deepseek / minimax) -- under $1 spend total across 30+ dispatches
- Anthropic CLI burn flagged twice; future sessions use OR for non-orchestration work
- Permission rule for `or_dispatch.ps1` MUST be added manually before next CLI session can self-dispatch:
```json
"Bash(pwsh -NoProfile -File *or_dispatch.ps1*)",
"Bash(pwsh -NoProfile -File *)",
"PowerShell(. $PROFILE; Use-OpenRouter; *)",
"PowerShell(Use-OpenRouter)"
```

## Trinity gate

- Lambda (truth): every URL / path / repo name / file referenced exists. 5/5
- Pi (clarity): one entry point; bundle table coming via OR; soft-publish workflow numbered. 5/5
- Theta (ethics): private-only until Sage approves; PII paths flagged; legal-name posture explicit. 5/5

15/15 PROCEED to Desktop ingestion.

## After Desktop is done

Sage's next CLI session:
1. Reads `wiki/handoffs/dispatches/KIMI_per_repo_metadata_bundle_output_2026-04-30.md` (the table)
2. Reads Desktop's first-wave-public-flip pick + rationale
3. Applies whatever rename / scrub / README fixes Desktop recommends BEFORE the soft-flip
4. Soft-flips repo public; Desktop verifies; flips back or commits to public
5. Iterates Tier 2, Tier 3
