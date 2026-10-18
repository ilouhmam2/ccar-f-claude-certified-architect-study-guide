# CCAR-F task statements, one line each

All 30 task statements of the Claude Certified Architect – Foundations exam guide (v1.0, July 2026), each reduced to the decision the exam expects. Back to the [study guide](../README.md).

> Unofficial, independently created study notes. Not affiliated with or endorsed by Anthropic.

## D1 · Agentic Architecture & Orchestration (27%)

- **1.1 Loops:** continue on `"tool_use"`, stop on `"end_turn"`; return *every* requested tool result; the model chooses the next step (not a decision tree).
- **1.2 Coordinator:** decomposes, routes all traffic, handles errors, aggregates; picks subagents by query complexity; partitions scope; iterates until coverage criteria are met.
- **1.3 Spawning:** Task (now Agent) tool must be in `allowedTools`; pass findings, IDs and criteria explicitly; parallel = several calls in one response; give goals and criteria, not step lists.
- **1.4 Enforcement & handoff:** prompts have a non-zero failure rate, so gate critical sequences in code; decompose multi-issue requests; hand humans a structured summary.
- **1.5 Hooks:** PreToolUse blocks or redirects (deny with a reason); PostToolUse normalizes, trims or redacts results before the model sees them.
- **1.6 Decomposition:** predictable → prompt chaining; open-ended → adaptive plan; large reviews → per-file passes + an integration pass.
- **1.7 Sessions:** `--resume <name>` when context is still valid (list the changed files); fresh session + summary when results are stale; `fork_session` for divergent options.

## D2 · Tool Design & MCP Integration (18%)

- **2.1 Descriptions:** inputs, examples, edge cases, "use X instead when…"; rename or split overlapping tools; check the system prompt for keyword traps.
- **2.2 Errors:** `isError` + `errorCategory` (transient / validation / business / permission) + `isRetryable` + a readable message; access failure ≠ empty result; recover locally, propagate the rest with partial results.
- **2.3 Distribution:** about 4–5 tools per role; constrained tools instead of generic ones; one narrow cross-role tool for a frequent need; `tool_choice` any/forced when a call must happen.
- **2.4 MCP config:** `.mcp.json` (project, shared, `${VAR}` secrets) · `~/.claude.json` (local or user, personal) · all servers available together · resources for catalogs · community servers for standard integrations.
- **2.5 Built-in tools:** Grep content · Glob paths · Edit unique anchor · Read + Write fallback · Grep an entry point, then Read along imports · list aliases before searching re-exports.

## D3 · Claude Code Configuration & Workflows (20%)

- **3.1 CLAUDE.md:** user `~/.claude/CLAUDE.md` (not shared) · project root or `.claude/CLAUDE.md` · subdirectory files · `@import` for modular standards · `.claude/rules/` topic files · `/memory` to see what loaded.
- **3.2 Commands & skills:** `.claude/commands/` and `.claude/skills/` are shared; `~/.claude/...` is personal · `context: fork` · `argument-hint` · `$ARGUMENTS` · skills are on demand, CLAUDE.md is always loaded.
- **3.3 Path rules:** YAML `paths:` globs load a rule only for matching files; best for conventions spread across directories.
- **3.4 Plan vs direct:** plan for architecture, many files, or several valid approaches; direct for clear, small fixes; Explore subagent for heavy discovery; plan, then execute.
- **3.5 Refinement:** 2–3 input/output examples · tests first, then share failures · interview pattern · one message for interacting issues, sequential for independent ones.
- **3.6 CI/CD:** `-p` · `--output-format json` + `--json-schema` · CLAUDE.md supplies CI context · independent reviewer · pass prior findings and existing tests.

## D4 · Prompt Engineering & Structured Output (20%)

- **4.1 Criteria:** define what to report and what to skip, plus severity levels with code examples; disable a noisy category while you fix it.
- **4.2 Few-shot:** 2–4 targeted examples of ambiguous cases with reasoning; show the output format; show varied document layouts.
- **4.3 Schemas:** tool_use + JSON schema; nullable optional fields; `"unclear"` and `"other"` + detail; normalization rules in the prompt; valid ≠ correct.
- **4.4 Validation–retry:** send the document + failed output + specific error; don't retry absent information; add `calculated_total` vs `stated_total`, `conflict_detected`, `detected_pattern`.
- **4.5 Batches:** about 50% cheaper, ≤ 24 h, no SLA, tools may be declared but never executed mid-request, `custom_id`; resubmit only failures (chunked); refine the prompt on a sample first.
- **4.6 Review design:** independent instance > self-review or more thinking; per-file + integration passes; per-finding confidence for routing (calibrate it).

## D5 · Context Management & Reliability (15%)

- **5.1 Context:** case-facts block for amounts, dates and promises; trim tool output; key summary first + headers; structured upstream outputs with metadata.
- **5.2 Escalation:** explicit human request, policy gap, or no progress. Not sentiment, not self-rated confidence. Several matches → ask for an identifier.
- **5.3 Error propagation:** structured context with partial results; no silent success; no whole-workflow abort; annotate coverage gaps.
- **5.4 Large codebases:** scratchpad files, subagents for focused questions, phase summaries, `/compact`, state manifests for crash recovery.
- **5.5 Human review:** per document type and per field accuracy; stratified sampling; confidence calibrated on labeled data; route low-confidence or contradictory items.
- **5.6 Provenance:** claim → source (URL/doc, page, excerpt, date) through synthesis; conflicts side by side; established vs contested; tables for numbers, prose for news.

---

The free [CCAR-F Pocket Guide](https://issaml.gumroad.com/l/ccar-f-pocket-guide?wanted=true&price=0) adds decision tables, 60-second drills, an exam-day plan and a 10-question readiness check with explained answers.
