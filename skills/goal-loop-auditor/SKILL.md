---
name: goal-loop-auditor
description: Audit existing prompts for Codex goals, autonomous loops, research loops, execution loops, review loops, or long-running agent tasks. Use when the user asks to review, improve, harden, debug, score, or validate a goal/loop prompt for missing facts, ambiguous scope, weak validation rules, source-quality gaps, output-contract gaps, conflict-handling problems, stop-condition problems, or hidden assumptions.
---

# Goal Loop Auditor

## Purpose

Evaluate an existing goal/loop prompt before it launches. Prioritize defects that would cause wrong work, unverifiable results, scope drift, unsafe action, or premature guessing.

## Workflow

1. Identify the loop type: `research`, `execution`, `review`, `monitoring`, or `mixed`.
2. Check whether the prompt contains all required launch fields.
3. Classify gaps by severity.
4. Ask for missing blocking facts when a corrected prompt cannot be produced safely.
5. Produce a corrected prompt only when remaining assumptions are explicit and non-blocking.

## Required Fields

Audit for these fields:

- `PROJECT`: project, repo, product, domain, or target system.
- `GOAL`: one-sentence deliverable, not a topic.
- `MODE`: research, execution, review, monitoring, or mixed.
- `CONTEXT`: minimum facts needed by another agent.
- `SCOPE`: explicit included and excluded work.
- `RULES`: what counts as verified, valid, accepted, or complete.
- `SOURCES`: allowed and disallowed evidence sources when relevant.
- `METHOD`: execution path or research method.
- `OUTPUT`: artifact type, location or naming, sections, schema, and format.
- `ON CONFLICT`: how to handle contradictory evidence or instructions.
- `STOP CONDITION`: when to halt instead of guessing.
- `DONE CRITERIA`: observable success criteria.

For execution loops, also audit `PERMISSIONS` for actions such as network access, file writes, dependencies, migrations, commits, pushes, production operations, and destructive commands.

## Severity

Use this scale:

- `Blocking`: the prompt should not launch until fixed.
- `High`: likely to cause wrong, unsafe, or unverifiable work.
- `Medium`: likely to cause inefficiency, ambiguity, or inconsistent output.
- `Low`: clarity or polish improvement.

Treat missing `GOAL`, `SCOPE`, `RULES`, `OUTPUT`, or `STOP CONDITION` as `Blocking`.

## Audit Checks

Check for:

- Deliverable names a concrete artifact or outcome.
- Scope includes explicit exclusions.
- Validation rules are observable and testable.
- Sources are restricted enough for the task.
- Output contract can be followed without guessing.
- Conflict handling prevents silent reconciliation.
- Stop condition names concrete halt cases.
- Permissions are explicit for risky actions.
- Prompt does not depend on hidden prior conversation.
- Long-running work has checkpoints or budget limits.

## Output Format

Return this structure:

````text
Audit result: [Ready | Needs revision | Do not launch]

Findings:
- [Severity] [Field]: [problem]
  Impact: [why it matters]
  Fix: [specific change]

Missing blocking facts:
- [question or fact needed]

Assumptions:
- [only non-blocking assumptions used in corrected prompt]

Corrected prompt:
```text
[only include when safe to draft]
```
````

If the prompt has no material issues, say `Audit result: Ready` and list any residual risks.

If blocking facts are missing, do not invent them. Provide a partial corrected prompt only when the user explicitly asks for a draft with assumptions.
