---
name: goal-loop-architect
description: Build high-quality prompts for launching goals, autonomous loops, research loops, execution loops, review loops, or long-running agent tasks in products that support goal/loop workflows. Use when the user wants to create, improve, or normalize a goal/loop prompt with reliable structure, explicit scope, source rules, validation rules, conflict handling, output contract, and stop condition; ask clarifying questions first when required facts are missing.
---

# Goal Loop Architect

## Purpose

Turn a rough task intent into a launch-ready goal/loop prompt. Optimize for unambiguous execution, verifiable outputs, and early clarification of missing facts.

## Workflow

1. Classify the loop as `research`, `execution`, `review`, `monitoring`, or `mixed`.
2. Run the Fact Gate before drafting the prompt.
3. Ask concise clarification questions if blocking facts are missing.
4. Load the relevant reference files listed below when they match the request.
5. Draft the prompt only after the required facts are known or explicitly marked as assumptions.
6. Keep the final prompt self-contained so another agent can run it without hidden context.

## References

- Read `references/prompt-patterns.md` when drafting `research`, `execution`, or `review` loops.
- Read `references/quality-rubric.md` before finalizing any launch prompt.
- Read `references/question-bank.md` when blocking facts are missing or the request is vague.
- Read `references/examples.md` when the user asks for examples or when a rough prompt needs substantial reshaping.

## Fact Gate

Require these facts before producing the final prompt:

- `PROJECT`: project, repo, product, domain, or target system.
- `GOAL`: one-sentence deliverable, not a topic or vague direction.
- `SCOPE`: what is included and what is explicitly out.
- `RULES`: what counts as a verified finding, valid row, accepted fix, or completed step.
- `SOURCES`: allowed evidence sources and source hierarchy.
- `OUTPUT`: artifact type, count, naming, location, schema, and formatting requirements.
- `ON CONFLICT`: how to handle contradictory evidence or requirements.
- `STOP CONDITION`: when to halt and report instead of guessing.

For long-running loops, also establish:

- `CHECKPOINTS`: when to report progress or request review.
- `BUDGET`: time, token, depth, file count, source count, or iteration limits.
- `PERMISSIONS`: actions that require approval, such as network access, writes, commits, schema changes, or production operations.
- `DONE CRITERIA`: how the user can tell the loop actually succeeded.

## Clarification Policy

Ask questions before drafting when any missing fact would change execution materially. Prefer 3-6 targeted questions, grouped by decision area.

Do not ask about facts that can be safely inferred from provided context. When making a non-blocking assumption, write it into the prompt under `ASSUMPTIONS`.

Do not emit a final launch prompt if any of these are missing:

- Deliverable
- Scope boundary
- Validation rule
- Output contract
- Stop condition

## Prompt Standard

Use this structure unless the user explicitly requests another format:

```text
# PROJECT: [name / repo / domain]

GOAL: [one sentence: the deliverable, not the topic]

MODE: [research | execution | review | monitoring | mixed]

CONTEXT:
- [brief facts the agent needs to know]

SCOPE:
- In: [included work]
- Out: [explicit exclusions]

RULES:
- [validation rules: what counts as verified, accepted, or complete]

SOURCES:
- [allowed sources in priority order]
- [disallowed sources, if relevant]

METHOD:
- [ordered workflow the loop should follow]

OUTPUT:
- Format: [file/message/table/PR/report/etc.]
- Location/name: [path or naming rules]
- Required fields/sections: [schema or outline]

ON CONFLICT:
- Flag the conflict with evidence and do not resolve silently.

STOP CONDITION:
- Halt and report when [specific uncertainty, missing access, source conflict, risk, or budget limit].

CHECKPOINTS:
- [progress cadence, review gates, or omit if not needed]

DONE CRITERIA:
- [observable completion criteria]
```

## Quality Bar

Make every field operational, then cross-check against `references/quality-rubric.md`:

- Replace abstract words like "better", "analyze", or "research" with observable actions.
- Convert preferences into rules where possible.
- State source quality explicitly: primary, official, peer-reviewed, internal docs, codebase truth, or user-provided artifacts.
- Include negative scope to prevent drift.
- Include failure handling for missing access, stale data, contradictions, and low-confidence evidence.
- Avoid hidden dependencies on prior conversation unless the final prompt quotes or summarizes the needed facts.

## Output Behavior

Return one of two outputs:

1. `Clarifications needed` with the minimum blocking questions.
2. `Launch prompt` with the completed prompt in a fenced text block.

If the user asks for both, include clarifications first and then a draft marked `Draft with assumptions`.
