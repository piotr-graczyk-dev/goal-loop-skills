# Quality Rubric

Use this rubric before returning a final launch prompt. If a required item fails, revise the prompt or ask clarifying questions.

## Required Checks

- `GOAL` names a deliverable that can be observed or inspected.
- `MODE` matches the actual work: research, execution, review, monitoring, or mixed.
- `CONTEXT` includes the minimum facts another agent needs without relying on hidden conversation history.
- `SCOPE` includes both in-scope and out-of-scope boundaries.
- `RULES` define what counts as valid, verified, accepted, or complete.
- `SOURCES` name allowed source types and disallowed source types when source quality matters.
- `METHOD` gives an execution path without over-constraining harmless implementation details.
- `OUTPUT` specifies artifact type, location or naming, required sections, and schema when applicable.
- `ON CONFLICT` prevents silent resolution of contradictions.
- `STOP CONDITION` tells the agent when to halt instead of guessing.
- `DONE CRITERIA` describe observable success.

## Scoring

Use this scale internally:

- `Ready`: all required checks pass and no blocking ambiguity remains.
- `Draft with assumptions`: non-blocking facts are assumed and listed explicitly.
- `Clarifications needed`: a required check fails or the prompt would produce materially different work depending on the answer.

## Common Failure Patterns

- The goal names a topic instead of a deliverable.
- The scope only says what to do and not what to avoid.
- The validation rule says "accurate" or "high quality" without evidence criteria.
- The sources allow broad web search when primary sources are required.
- The output says "report" but does not define sections or fields.
- The stop condition is missing, so the loop is encouraged to invent.
- The prompt depends on "as discussed above" instead of embedding the facts.
