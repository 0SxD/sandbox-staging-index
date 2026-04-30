# Known Corrections (orchestrator-verified)

These are inventory-level errors caught during the 2026-04-29 night sweep. Apply during Desktop AM review.

## 1. ethos.py and logos.py do not exist
The 12-category sweep INFERRED these existed in `OpenBrainLM_sandbox/openbrainlm/layers/`. They do not. The dir has only:
- `pathos.py` (Trinity Pathos layer)
- `active_sensing.py`, `basal_ganglia.py`, `chromatophore.py`, `ganglion.py`, `relevance.py`, `stigmergy.py` (biomimetic neural layers, NOT Trinity rubric)
- `base.py`, `__init__.py`

The full Trinity Logos / Pathos / Ethos rubric lives at:
- `_github_export_staging/trinity_dialectic/trinity.py` (already pushed to 0SxD/trinity-dialectic, PRIVATE)

## 2. Review_Report_Pass_Fail_Audit_Agent/skills/ is EMPTY
The directory exists but has zero files. Sage-authored docs ARE present at:
- `PROTOCOL.md`, `spec.md`, `system_directive.md`, `bootstrap.md`, `REPORT_wikiLLM_karpathy_setup.md`, `skills.md` (skills.md is a markdown doc, not a directory)

## 3. Resume v4 NEEDS_REVISION cleanup items
From minimax + kimi zero-context checkers:
- Remove "Anthropic Greenhouse 5159669008" from header
- Strip trailing HTML comment
- Resolve [GREEN_PAPER_URL pending Sage]
- Confirm $80M wording
- Verify Virtual Educator chronological placement
- Confirm legal-name-in-header posture
- Embed OQ resolution evidence (or keep out-of-band)

## 4. Inventory checker findings (NEEDS_REVISION on 5 dimensions)
- Coverage 3/5: 8 wiki/concepts/ files truncated by row limit (RL_finance, Kubernetes, LLM_Wiki, Flash_Loans, MEV, ve(3,3), GCN, Spiking_NN, Post_Quantum)
- Categorization 4/5
- Qualification mapping 4/5
- Risk assessment 2/5: Review_Report_Pass_Fail_Audit_Agent risk should be MEDIUM, not low
- Confidence calibration 3/5: "ambiguous" misused for audit dirs

## 5. Failed dispatch
- `deepseek/deepseek-v3.2-speciale` slug FAILED (exit code 4, no output). May not be a real OR slug. Substituted with kimi-k2-thinking zero-context.
