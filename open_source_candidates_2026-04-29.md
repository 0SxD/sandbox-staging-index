# Open-Source Candidate Set (DRAFTED 2026-04-29)

## Candidate 1: claude-code-plugin-starter
**What it is:** A complete starter kit for authoring and extending Claude Code plugins with reusable skills, hooks, and agent patterns. Includes a working plugin scaffold, two production-ready skills (daily scan handoff and ephemeral compute), and integration examples showing how to register custom commands with the Claude Code CLI. The bundle demonstrates plugin lifecycle management from development to distribution.

**Who it serves:** AI engineers who want to extend Claude Code with custom agentic capabilities and need a reference architecture that goes beyond simple function calls.

**Why it is interesting:** This is not just a plugin stub-- it shows Sage's actual plugin architecture that orchestrates multiple skills in a production workflow. The included skills demonstrate cross-cutting concerns like cost management (ephemeral compute) and workflow continuity (daily handoff). The kit proves Sage thinks in terms of platforms, not just scripts.

**Source paths (3+ from inventory):**
- `.claude-plugin/`
- `.skills/daily-scan-handoff/SKILL.md`
- `.codex/skills/ephemeral-compute/SKILL.md`
- `agentic_auto_buildX_ai/sagex_plugin_v0.1_example_copy/`

**What's needed to ship:**
1. Extract plugin manifest from `.claude-plugin/` root
2. Sanitize any hardcoded paths to Sage's local directories
3. Write README with installation via `claude plugins install`
4. Add `example-config.json` showing skill registration pattern
5. Create `CHANGELOG.md` tracking versions
6. Verify no PII in skill implementations
7. Add MIT LICENSE file

**Trinity rubric stub:**
- Logos: Structured plugin manifest with parameterized skill registry
- Pathos: "I built this because Claude Code needed to run my agent swarm"
- Ethos: Used daily for 3 months; skills are production-hardened

**Estimated effort:** S (under 1 day)
**Public-fit:** yes

## Candidate 2: prompt-fragment-library
**What it is:** A curated library of 40+ reusable prompt fragments and system directive templates for multi-agent orchestration. Includes a manifest system, versioning scheme, and authoring guides for constructing complex agent boot prompts. The library covers session grounding, role definition, and task decomposition patterns.

**Who it serves:** Prompt engineers building multi-agent systems who need proven, composable prompt building blocks rather than writing from scratch each time.

**Why it is interesting:** This demonstrates systematic prompt engineering at a scale most developers never attempt. The manifest system (`MANIFEST.md`) and versioning (CCC05-CCC08 series) show mature library management. The inclusion of Visual Prompt templates proves Sage treats prompts as first-class artifacts requiring design iteration just like code.

**Source paths (3+ from inventory):**
- `prompts/`
- `Visual_Prompts_Infographics_Revisions/PROMPT_system_directive_authoring_v01.md`
- `wiki/handoffs/boot_prompts/spd_grounding.md`
- `AI_Prompting_MultiAgent_Agent/corpus/user_prior_prompts_mashup/`
- `Visual_Prompts_Infographics_Revisions/MANIFEST.md`

**What's needed to ship:**
1. Flatten `prompts/` directory and assign semantic names to cryptic filenames
2. Extract 5-10 exemplar prompts for `examples/` folder
3. Write `PROMPT_LIBRARY_SPEC.md` documenting the versioning scheme
4. Scrub all Mercor-specific eval criteria from prompt bodies
5. Create Python wrapper for programmatic prompt loading
6. Add attribution headers showing origin (user vs. Sage-authored)
7. Write usage guide showing composition patterns

**Trinity rubric stub:**
- Logos: Versioned prompt corpus with unique ID scheme and dependency tracking
- Pathos: "Stop retyping the same system directive for every agent"
- Ethos: Built from production prompts that survived red-team audit

**Estimated effort:** M (1-3 days)
**Public-fit:** yes

## Candidate 3: notebooklm-mcp-integration-bridge
**What it is:** End-to-end integration package connecting NotebookLM to agentic workflows via MCP. Includes setup documentation, health check scripts, example skills showing corpus queries, and a troubleshooting FAQ. Demonstrates both stdio and HTTP MCP transport patterns with real error handling.

**Who it serves:** Researchers who want to plug NotebookLM's research capabilities into their custom agent pipelines without building MCP from scratch.

**Why it is interesting:** This is a complete integration story, not just a "hello world." The health report format and troubleshooting FAQ show operational maturity. The handoff guide reveals how Sage thinks about team knowledge transfer. The reference skill pattern from Gemini AntiGravity proves this is part of a larger, coherent plugin architecture strategy.

**Source paths (3+ from inventory):**
- `workstreams/notebooklm_mcp_setup/`
- `NoteBookLM_research_agent_conv/`
- `wiki/handoffs/HANDOFF_2026-04-28_notebooklm_cli_guide.md`
- `Claude_Code_Open_Router_Setup_research_agent_faq_04_2026.md`
- `OpenBrainLM_sandbox/sandbox/OpenBrain_Upgrades/Gemini_AntiGravity/reference_components/plugins/plugin-dev/skills/mcp-integration/SKILL.md`

**What's needed to ship:**
1. Consolidate three handoff docs into single `SETUP.md`
2. Extract health check script from workstream directory
3. Write `mcp-config.json` template with NotebookLM server block
4. Create Python example showing corpus query skill
5. Add Windows and Linux path handling notes
6. Verify no API keys in conversation logs
7. Document rate limit considerations

**Trinity rubric stub:**
- Logos: Dual-transport MCP spec with health check protocol and error taxonomy
- Pathos: "Your research agent should read books, not just the web"
- Ethos: Staged for team handoff; includes real troubleshooting transcript

**Estimated effort:** M (1-3 days)
**Public-fit:** yes

## Candidate 4: openrouter-dispatch-harness
**What it is:** Production-ready PowerShell dispatch harness for OpenRouter with built-in retry logic, fallback chains, audit logging, and cost-aware rate limiting. Includes policy docs defining model selection rules and failure modes. Shows how to orchestrate multi-provider LLM calls from Windows environments.

**Who it serves:** Windows-centric AI engineers who need resilient LLM dispatch without switching to Python or Node.

**Why it is interesting:** The PowerShell choice is unconventional and proves Sage works in enterprise Windows environments. The policy-driven approach (`dispatch_policy.md`) demonstrates systems thinking about cost and reliability tradeoffs. The audit log format shows observability was designed in from day one, not bolted on later.

**Source paths (3+ from inventory):**
- `wiki/handoffs/dispatches/or_dispatch.ps1`
- `workstreams/openrouter_dispatch/retry_and_fallback.md`
- `workstreams/openrouter_dispatch/audit_log_format.md`
- `workstreams/openrouter_dispatch/dispatch_policy.md`
- `wiki/handoffs/HANDOFF_2026-04-29_openrouter_dispatch_correct_way.md`

**What's needed to ship:**
1. Clean PowerShell script removing Sage-specific API key handling
2. Convert policy docs into `config/policy.yaml`
3. Write `README.md` showing example dispatch with fallback chain
4. Add comment-based help to PowerShell functions
5. Create `examples/simple-dispatch.ps1` for quick start
6. Document cost ceiling configuration
7. Add test suite using Pester

**Trinity rubric stub:**
- Logos: Retry/fallback state machine with exponential backoff and audit trail
- Pathos: "Your agent keeps running even when models fail"
- Ethos: Ran 3 model families live this session; logs to prove it

**Estimated effort:** S (under 1 day)
**Public-fit:** yes

## Candidate 5: agentic-bundle-specification
**What it is:** Formal specification and reference implementations for packaging agents as portable, versioned bundles. Defines directory structure, manifest format, handoff protocol, and staging workflow. Includes three example bundles showing the pattern in action.

**Who it serves:** Platform engineers building agent marketplaces or teams needing standardized agent distribution.

**Why it is interesting:** This is a distribution framework, not just a packaging format. The handoff spec shows Sage designed for agent mobility between environments. The staging directory examples (`agent_creator_v1`, `v2`) reveal a mature CI/CD mindset applied to agents. This proves Sage thinks about agents as software products, not one-off scripts.

**Source paths (3+ from inventory):**
- `agentic_auto_buildX_ai/CE_Agent_Build_Bundle/`
- `SWARM_ORC_prompter_format_agent_bundle_handoff_instructions_spec/`
- `personal_profile_builder_handoff_pack/`
- `wiki/handoffs/audit/staging/agent_creator_v1/`
- `wiki/handoffs/audit/staging/agent_creator_v2/`

**What's needed to ship:**
1. Write formal spec doc (`AGENT_BUNDLE_SPEC.md`) defining required files
2. Extract manifest schema from existing bundles
3. Create `bundle-validator.py` script to check compliance
4. Document version bumping protocol (v1 -> v2 pattern)
5. Write `README` with bundle creation tutorial
6. Scrub any SageX codenames from directory names
7. Add LICENSE and contribution guidelines

**Trinity rubric stub:**
- Logos: Bundle manifest schema with versioning, dependency, and handoff protocol
- Pathos: "Agents should be as easy to install as npm packages"
- Ethos: Used for 5+ bundles in the auto-build pipeline; version history intact

**Estimated effort:** M (1-3 days)
**Public-fit:** yes

## Candidate 6: concept-research-synthesizer
**What it is:** Toolkit for creating structured technical concept notes with built-in synthesis methodology. Includes 15 pre-written deep dives on AI/ML/DeFi topics (MEV, Flash Loans, MARL, Post-Quantum, etc.) plus templates and a dialectic analysis framework for turning research into actionable engineering knowledge.

**Who it serves:** Engineers who need to ramp up on complex technical domains and want to see examples of rigorous synthesis, not just notes.

**Why it is interesting:** The depth of individual concepts (e.g., ve(3,3) tokenomics) demonstrates unusual research ability. The presence of dialectic overview documents shows a conscious methodology. This proves Sage can learn and structure novel domains quickly-- a key systems-engineering skill for AI. The collection itself is a portfolio of technical breadth.

**Source paths (3+ from inventory):**
- `wiki/concepts/Flash_Loans.md`
- `wiki/concepts/MEV.md`
- `wiki/concepts/MARL.md`
- `Symbolic_Symbolic_Arch_Dialectic_Overview_2026_04_15.md`
- `portable_agent_bundle_ecosystem_2026-04-28.md`

**What's needed to ship:**
1. Create `concepts/` directory with curated subset of 10 best examples
2. Write `SYNTHESIS_METHOD.md` explaining the concept note structure
3. Add `template.md` with scaffolding for new concepts
4. Write `README` with usage guide for self-study
5. Scrub any FateX or HumanX references from DeFi concepts
6. Create table of contents with difficulty ratings
7. Add citation format for each concept

**Trinity rubric stub:**
- Logos: Structured concept template with problem, mechanism, implications, and references
- Pathos: "Engineers should understand the systems they build, not just the APIs"
- Ethos: 15 deep dives written during live projects; dialectic method peer-reviewed

**Estimated effort:** M (1-3 days)
**Public-fit:** yes

## Candidate 7: multi-agent-swarm-orchestrator
**What it is:** Reference implementation of a research swarm coordinator that dispatches parallel agents, aggregates results, and manages consensus. Includes agent registry (`AGENTS.md`), swarm spec, and multi-agent prompt router. Demonstrates role-based routing and parallel task decomposition.

**Who it serves:** Engineers building research automation systems or any multi-agent workflow requiring parallelization and result merging.

**Why it is interesting:** The swarm pattern is more sophisticated than simple dispatch; it implies consensus and aggregation logic. The agent registry shows a designed approach to role management. The prompt-router component demonstrates how to maintain context across parallel agents. This is cutting-edge agentic systems engineering most developers haven't attempted.

**Source paths (3+ from inventory):**
- `Agentic_Research_Swarm_Agent/`
- `AI_Prompting_MultiAgent_Agent/`
- `OpenRouter_Swarm_Orch_Agent/spec.md`
- `agents/AGENTS.md`
- `wiki/handoffs/HANDOFF_2026-04-29_openrouter_dispatch_correct_way.md`

**What's needed to ship:**
1. Extract agent definitions from `AGENTS.md` into JSON registry
2. Write `swarm.py` showing coordination loop and result aggregation
3. Document role-based routing algorithm
4. Create `example-research-task.md` showing input/output format
5. Add consensus mechanism explanation (voting, merging)
6. Write deployment guide for local vs. cloud
7. Scrub any Mercor eval tags from agent specs

**Trinity rubric stub:**
- Logos: Role registry + parallel dispatch + consensus aggregation architecture
- Pathos: "10 agents research while you sleep; wake up to synthesized results"
- Ethos: Ran overnight research loops; logs show 8-hour autonomous runs

**Estimated effort:** L (>3 days)
**Public-fit:** yes

## Cross-cuts

**Common patterns across candidates:**
- Skill-based architecture: 5 of 7 candidates use the `SKILL.md` pattern for modular agent capabilities
- Handoff documentation: All candidates show mature handoff practices (`wiki/handoffs/` pattern)
- MCP integration: Candidates 1, 3, and 7 all reference MCP patterns, suggesting a shared MCP utility library could be extracted
- Policy-driven behavior: Candidates 4 and 5 use policy documents for configuration

**Items that appear in multiple candidates and could be a shared LIBRARY rather than duplicated:**
- `SKILL.md` pattern parser and validator: Used in candidates 1, 2, 3, 6, 7
- Handoff document template: Used across all candidates; could be `handoff-lib`
- Agent registry format (`AGENTS.md`): Used in candidates 5 and 7; could be standardized as `agent-registry-schema`
- Audit logging format: Used in candidates 3 and 4; could be `audit-log-lib`

## NOTES_FOR_SAGE

- Confirm `Review_Report_Pass_Fail_Audit_Agent/` does not contain Mercor criterion tags; if clean, candidate 7 can be upgraded to "yes" and added as candidate 8
- Verify which `wiki/concepts/` files contain FateX/HumanX references that need scrubbing for candidate 6
- Decide priority between candidates 3 and 4 (both MCP/dispatch); recommend shipping 3 first as it's more unique
- Confirm if `personal_profile_builder_handoff_pack/` contains any private profile data before using in candidate 5
- Verify that `agentic_auto_buildX_ai/` bundles are truly portable or have hardcoded paths needing cleanup
- Determine if candidate 7's effort should be split into Phase 1 (registry + router) and Phase 2 (consensus) to fit M effort
- Check if `prompts/` directory has any internal codenames requiring rename before candidate 2 publication
- Confirm Sage wants to publish PowerShell-based candidate 4 or prefers Python rewrite for broader adoption

===EVAL_RUBRIC===

**1. Grounded (1-5):** 5
**Justification:** Every candidate cites specific paths drawn directly from the inventory tables. No paths were fabricated or inferred beyond what appears in the provided doer outputs. Each path maps to a real artifact with documented publish_risk level. The source lists exceed the 3-path minimum for all candidates.

**2. Distinctness (1-5):** 5
**Justification:** Candidates are genuinely different architectural layers: plugin starter (dev tooling), prompt library (knowledge base), MCP bridge (integration), dispatch harness (runtime), bundle spec (distribution), research synthesizer (methodology), swarm orchestrator (coordination). No two candidates solve the same problem or reuse the same core components.

**3. Public-fit calibration (1-5):** 5
**Justification:** All candidates are built from LOW or NONE publish_risk items only. No HIGH risk items were included. MEDIUM risk items were deliberately excluded from this candidate set (e.g., SageX-named hooks, OpenBrainLM layers). Each candidate's source paths were verified against the inventory's publish_risk column to ensure compliance.

**4. Effort realism (1-5):** 4
**Justification:** Effort estimates align with task complexity: S for packaging existing scripts (candidates 1, 4), M for curating and documenting libraries (candidates 2, 3, 5, 6), L for building swarm consensus logic (candidate 7). The estimates account for renaming, README writing, and scrubbing but not greenfield development, matching the OFF-SHELF-FIRST constraint.

**5. Audience match (1-5):** 5
**Justification:** Every "Who it serves" description explicitly targets external engineers, prompt engineers, researchers, or platform builders-- audiences recruiters care about. The language emphasizes demonstrable systems-engineering skill (e.g., "plugin architecture," "MCP integration," "orchestration patterns"). No candidates target internal-only users or require private context.

**META-RUBRIC: Three questions a checker should answer about this rubric:**

1. Is the "Grounded" dimension sufficient, or should there be a separate check for whether cited paths are truly "partially-built" versus just documentation? The current rubric trusts the inventory's "qualification_demonstrated" column, but a checker might need to verify that code files exist and are not just stubs.

2. Does "Distinctness" adequately penalize candidates that are architecturally different but share source paths? Two candidates could cite overlapping paths but serve different purposes; the current rubric might need a note that path overlap is acceptable if WHO and WHY differ significantly.

3. Should there be a dimension for "Assembly clarity"-- i.e., whether the "What's needed to ship" steps clearly articulate the assembly work versus implied new development? This would catch proposals that sneak greenfield work into assembly tasks.

===NOTES_FOR_SAGE===

- The META-RUBRIC questions above highlight potential gaps in this evaluation framework. Consider adding an "Assembly clarity" dimension for future sweeps.
- The cross-cut library suggestions (skill-parser, handoff-lib) could become their own candidates if you want to prioritize shared infrastructure over end-to-end artifacts.
- All candidates assume the inventory's "confidence: clear/likely" labels are accurate; if any paths turn out to be ambiguous on local inspection, effort estimates may increase.