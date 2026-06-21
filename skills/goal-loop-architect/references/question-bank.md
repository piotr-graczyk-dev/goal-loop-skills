# Question Bank

Ask only the minimum blocking questions. Prefer 3-6 questions, grouped by decision area.

## Deliverable

- What exact artifact should the loop produce?
- Should the result be a final answer, file, table, patch, PR, checklist, or plan?
- What would make the deliverable unacceptable?

## Scope

- What is explicitly in scope?
- What should the agent avoid even if it looks related?
- Is this limited to a specific repo, branch, issue, file set, date range, market, language, or platform?

## Validation

- What counts as a verified finding, valid row, accepted fix, or completed step?
- Which commands, tests, source checks, or manual checks must pass?
- Should uncertain findings be excluded or included with confidence labels?

## Sources

- Are only primary or official sources allowed?
- Are aggregators, blog posts, AI summaries, forum posts, or vendor pages allowed?
- Is recency important? If yes, what date range or freshness requirement applies?

## Output

- What format should the output use?
- Where should files be written, and how should they be named?
- What fields or sections are required?

## Permissions

- Can the loop browse the web or call networked tools?
- Can it edit files, install dependencies, run migrations, commit, push, or create PRs?
- What actions require the user to approve first?

## Stop Conditions

- When should the agent halt and report instead of guessing?
- What missing access, contradictory evidence, failing validation, or budget limit should stop the loop?
- Should the agent return partial results if the stop condition is hit?
