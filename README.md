# Agents
Repo consists of agents for share

⸻

Architect — Read-Only Code & Architecture Review Agent

architect is a read-only architecture and code review subagent designed for use with OpenCode.
It behaves like a senior software architect: calm, risk-focused, non-intrusive, and concise — even on very large commits.

This agent never edits code, never narrates its thinking, and never loops.

⸻

What This Agent Is For

The Architect agent is intended to:
	•	Review proposed or completed changes
	•	Identify architectural, security, and scalability risks
	•	Validate alignment with system design and standards
	•	Provide actionable, non-blocking recommendations
	•	Handle large diffs (5k+ lines) without spiraling or narrating

It is optimized for:
	•	Monorepos
	•	Large commits
	•	Long-lived systems
	•	Teams that want signal, not noise

⸻

What This Agent Will Never Do

The Architect agent will not:
	•	Modify, generate, or refactor code
	•	Provide patches, diffs, or commit instructions
	•	Narrate investigation steps or file access
	•	Comment on tooling, editor behavior, or filesystem activity
	•	Perform line-by-line walkthroughs
	•	Loop, re-scan endlessly, or “think out loud”
	•	Override product or implementation decisions

It is advisory only.

⸻

Key Design Principles

1. Read-Only by Construction

All edit permissions are denied.
The agent can only analyze and recommend.

2. Deterministic Output
	•	Low temperature (0.1)
	•	Strict output schema
	•	Single response per invocation

3. Large-Diff Safe

For large change sets (≈500+ lines or 5+ files), the agent:
	•	Performs a high-level triage
	•	Focuses only on high-risk areas
	•	Ignores boilerplate, renames, and test churn
	•	Caps recommendations to 5 maximum

4. Tool Blindness

Tool usage (file reads, searches, diffs) is treated as an invisible implementation detail.
The agent never reports or reasons about tool activity.

5. Hard Stop Guarantees
	•	Max steps enforced
	•	Explicit loop termination rules
	•	Early exit when no signal exists

⸻

Model & Runtime
	•	Provider: OpenRouter
	•	Model: x-ai/grok-code-fast-1
	•	Temperature: 0.1
	•	Max steps: 5

This model was chosen for:
	•	Fast code comprehension
	•	Deterministic behavior
	•	Low cost for frequent reviews

⸻

Invocation

Typical usage inside OpenCode:

@architect review README.md

@architect review recent changes

@architect review this commit

Best practice is to scope the review explicitly when possible:

@architect review README.md only


⸻

Output Format

The Architect agent always responds using a strict, machine-readable Markdown format.

Example:

# Architect Review
component: README.md

## Risk Summary
overall_risk: low
recommended_action: proceed

## Passed
- Documentation structure is clear and consistent

## Recommendations
- suggestion: Add a Security policy section
  priority: medium

Notes:
	•	Sections are omitted if empty
	•	primary_risks is omitted entirely when none exist
	•	No narration, no intermediate thoughts

⸻

When to Use This Agent

Use architect when you want:
	•	A calm second opinion on a big change
	•	Architectural risk detection before merging
	•	Documentation or system design review
	•	A senior-level overview instead of line comments

Do not use it for:
	•	Writing code
	•	Refactoring
	•	Implementation planning
	•	Chatty feedback or brainstorming

⸻

Status

This agent is production-ready and hardened against:
	•	Tool-driven loops
	•	Chain-of-thought leakage
	•	Large-diff exhaustion
	•	Over-verbosity

It is intentionally conservative and quiet by design.

⸻

License / Usage

Feel free to:
	•	Fork
	•	Modify
	•	Extend
	•	Use as a base for other review agents (security, performance, infra)

If you build improvements or variants, consider sharing them back.

⸻

If you want, next I can:
	•	Write a short “Quick Start” README
	•	Add a GIF-style usage walkthrough
	•	Help you package sibling agents (architect-deep, architect-docs)
	•	Or help you structure the repo for multiple agents

Just say the word.
