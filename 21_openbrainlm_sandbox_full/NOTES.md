# 21 -- OpenBrainLM Sandbox FULL (every session, BIRTHDAY through now)
**Source:** `OpenBrainLM_sandbox/`

## Contents
- openbrainlm/layers/ (pathos.py + biomimetic neural layers: active_sensing, basal_ganglia, chromatophore, ganglion, relevance, stigmergy, base.py)
- openbrainlm/agents/ (hippocampus.py + others)
- openbrainlm/orchestrator.py
- sagex/skills/ (audit-loop, brain-harness, coding-harness, edit-mode, notebooklm-research, research-gate, worktree-isolation -- 7 skills Sage authored)
- sagex/hooks/ (validate_research, destructive_command_guard, audit_gate_check, agent_result_capture, auto_reviewer_trigger, brainstem_inject, precompact_save, propagation_check, session_savepoint_inject -- 9 hooks)
- sagex/agents/
- sandbox/ (with OpenBrain_Upgrades incl Gemini_AntiGravity reference plugins)
- research/ (with audits/, gemini_handoff_2026-03-25, gemini_ag_audit_2026-03-30, agents_arcs_audit_patterns_2026-03-24, openbrain-briefing-v2, session38_44_full_inventory)
- .agents, .claude, .gemini configs
- AGENT_RULES.md (12K), ARCHITECTURE.md (13K), BIRTHDAY.md (1.5K -- THE ORIGIN doc), IMPLEMENTATION_PLAN.md (23K), OPERATIONAL_LAYERS.md (32K), WHAT_IS_OPENBRAIN.md (5.8K), WHITEPAPER.md (24K), OPEN_BRAIN.md (3.7K), CLAUDE.md (3.4K), README.md (8.1K)
- pyproject.toml, uv.lock, tests/, notebooks/, knowledge/, handoffs/, docs/

## Good
HUGE codebase. THE primary OpenBrainLM project. BIRTHDAY.md is the canonical project origin (the user explicitly referenced this). WHITEPAPER + ARCHITECTURE + OPERATIONAL_LAYERS are publication-grade research artifacts. pathos.py is the Trinity Pathos layer. sagex/skills + sagex/hooks are Sage-authored production agentic infrastructure.

## Bad / risk
The 2026-04-19-pushed 0SxD/archive-openbrain repo is likely an OLDER snapshot. Local OpenBrainLM_sandbox/ tree may be ahead. Pre-EXIF-strip on visuals; codename rename needed (OpenBrain, sagex, 143_protocol, PEL).

## Desktop action
COMPARE 0SxD/archive-openbrain vs current local tree. If local is ahead (likely): push delta to a NEW private repo 0SxD/openbrainlm-sandbox-current OR replace 0SxD/archive-openbrain with current. The existing 0SxD/openbrainlm-sandbox repo (per the 36-repo list) MAY be empty placeholder; verify.
