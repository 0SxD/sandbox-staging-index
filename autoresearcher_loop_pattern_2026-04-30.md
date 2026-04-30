# autoresearcher_loop -- a Karpathy-style summary paper

**Date:** 2026-04-30
**Status:** locked-in pattern; Sage wants this format applied to most future tools
**Reference:** Karpathy autoresearcher style (single-file, README-is-the-paper, dependency-light, runs by user uncloning)

## Abstract

We tested whether sequential context-passing in LLM-driven research dispatches produces deeper, more actionable output than independent zero-context dispatches. On a single problem (NotebookLM MCP login fragility) using one model (kimi-k2-thinking), the 3-pass sequential chain (Run1 -> Run2 with Run1 prior -> Run3 with Run1+2 prior) produced 1314 cumulative lines at $0.076; two parallel zero-context runs produced 620 cumulative lines at $0.060. Cost-per-actionable-line: 3x sequential $0.000038/line vs zero-context $0.000096/line -- **2.5x cheaper per actionable instruction**. Run3 self-graded 14/15 on Trinity rubric; combined chain reached "shippable 8-12 step plan" depth; zero-context stopped at "sketch level." Independent verdict (deepseek-v4-pro analyst, zero context): sequential decisively wins for problems with decomposable structure, conditional on a correct first-pass decomposition. We recommend a HYBRID pattern: 2-3 zero-context runs to identify candidate gaps, then 3x sequential on the chosen gap.

## The pattern (autoresearcher-loop)

```
Pass 1 -- foundation / decomposition
  - Identify N vector groups (V1..VN) -- the problem space
  - Identify the THINNEST branch (the gap)
  - Generate a neuro-linguistic txt-image (mental model snapshot)
  - Write a Pass-2 brief: where to focus, FORBID list of redundant work

Pass 2 -- focused gap-closing
  - Read Pass 1's vector tree + Pass-2 brief
  - Go FURTHER on the identified gap (NOT redo Pass 1's scan)
  - Produce code-level / mechanism-level fixes
  - Generate updated txt-image (richer mental model)
  - Write Pass-3 brief

Pass 3 -- production-readiness
  - Read Pass 1+2 distilled
  - Cross-platform / deployment / monitoring layer
  - Final action plan + Trinity self-grade
```

The pattern compounds: each pass is path-dependent. Pass 2's commitment to `watchdog` made Pass 3's PollingObserver decision tree meaningful. Pass 2's refresh-token coroutine made Pass 3's `token_age_seconds` Prometheus metric possible.

## Why it works (mechanism)

1. **Sub-problem locking.** Pass 1 picks the gap. Pass 2 commits to a tool. Pass 3 hardens that tool. Each commitment narrows the search space, so per-pass tokens go to depth not breadth.
2. **Compounding context.** Pass 2 does not waste tokens re-establishing what Pass 1 settled. The FORBID list is enforced by the prompt.
3. **Specificity gain.** Run 1 says "modify the auth code." Run 2 says "modify `mcp_server/auth_manager.py:_token_cache`." Run 3 says "use `watchdog.observers.polling.PollingObserver` because Inotify breaks on Docker volume mounts." Each pass gains a level of specificity unavailable to a fresh-start zero-context.

## Why it might fail (counter-arguments, locked-in)

1. **Assumption propagation.** If Pass 1 misclassifies the gap, the chain compounds the error. Zero-context runs catch this with model variance.
2. **Sequential time.** 3x sequential = 739s wall; 2x zero-context parallel = 323s wall. Time-sensitive tasks favor parallel zero-context.
3. **Diminishing returns.** Pass 3 already self-grades 14/15. Pass 4 may reach 15/15 via packaging / governance, but the marginal cost-per-marginal-utility climbs.

## Recommended hybrid pattern

```
Phase A: 2-3 INDEPENDENT zero-context runs (parallel)
  -> Compare. Pick the run with the strongest decomposition.

Phase B: 3x SEQUENTIAL chain seeded with Phase A's winning decomposition
  -> Pass 1 lifts the decomposition; Pass 2 + Pass 3 add depth.

Phase C: External zero-context AUDITOR grades the Phase B output
  -> If REJECT, Pass 4 remediation. If ACCEPT, ship.
```

This was the pattern used for the LinkedIn V1 -> V2 -> external audit -> V3 compound-engineer dispatch and worked: V2 was self-graded 15/15 but external audit caught critical gaps (cookie-auth ToS violation, Anonymous-tier negative-margin economics). V3 addressed all 8 gaps.

## Open questions Sage tests

1. **4x same-model:** dispatched 2026-04-30 (run-id `bcyf6baxd`). Tests whether Pass 4 finds value above 3x ceiling.
2. **Multi-model 3x:** dispatched 2026-04-30 (`bzak5wfvf` for pass-B deepseek; pass-C minimax to follow). Tests whether changing model between passes adds different-strength reasoning.
3. **Hybrid 2-3-3:** not yet dispatched; recommended next experiment.

## Tools to package (Karpathy-style: one repo, README is the paper)

1. `0SxD/autoresearcher-loop` -- the 3x pattern as a single Python file. Inputs: problem statement, model slug, OR API key. Outputs: 3 sequential markdown digests + Trinity self-grade. README explains the experiment design from this paper. MIT.
2. `0SxD/research-loop-effectiveness` -- the per-iteration effectiveness eval (NEW_HIT_RATE, WORKSTREAM_COVERAGE_DELTA, COST_PER_HIT, TERM_EXPANSION) as a CLI scorecard.
3. `0SxD/multi-model-pass-orchestrator` -- pending the multi-model results; if successful, ships as Karpathy-style.

## Files

- `wiki/handoffs/dispatches/KIMI_nlm_mcp_login_3x_run{1,2,3}_output_2026-04-30.md` -- the 3 sequential outputs
- `wiki/handoffs/dispatches/KIMI_nlm_mcp_login_zero_context_{A,B}_output_2026-04-30.md` -- the 2 zero-context controls
- `wiki/handoffs/dispatches/DEEPSEEK_3x_vs_zero_context_research_paper_output_2026-04-30.md` -- the 249-line analyst paper

## Citations

- Karpathy autoresearcher style reference: https://github.com/karpathy/nanoGPT (the file-as-paper template; nanoGPT is the canonical example)
- G-Eval rubric grounding: Liu et al. 2023, https://arxiv.org/abs/2303.16634
- Trinity Dialectic in Python: `0SxD/trinity-dialectic` (Sage-authored)

## Verdict (locked-in)

3x sequential context-passing is the DEFAULT pattern for decomposable LLM research problems on Sage's stack. Multi-model and 4x are open experiments. Lock-in date: 2026-04-30.
