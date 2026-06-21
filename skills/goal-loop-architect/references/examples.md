# Examples

Use these examples as shape references. Do not copy their facts unless the user gives the same task.

## Research Loop

Weak:

```text
Research the best competitors for FitYez.
```

Stronger:

```text
# PROJECT: FitYez

GOAL: Produce a ranked table of 10 direct Strength & Conditioning LMS competitors for coaches and athletes.

MODE: research

SCOPE:
- In: products that support coach-led programming, athlete management, learning content, or training plan delivery.
- Out: generic fitness trackers, consumer workout apps without coach workflows, and unsourced marketplace listings.

RULES:
- A competitor is verified only when an official website or product documentation confirms at least two in-scope capabilities.

SOURCES:
- Official product websites, docs, pricing pages, and help centers.
- No listicles, app-store summaries, or unsourced aggregator pages.

OUTPUT:
- Format: markdown table.
- Required fields: name, URL, target user, verified capabilities, pricing evidence, source links, confidence.

ON CONFLICT:
- Flag contradictory positioning or pricing evidence in `conflict_notes`.

STOP CONDITION:
- Halt if fewer than 5 competitors can be verified from allowed sources.
```

## Execution Loop

Weak:

```text
Fix the dashboard bugs.
```

Stronger:

```text
# PROJECT: FitYez web app

GOAL: Fix the dashboard athlete list loading bug and verify the list renders for authenticated coaches.

MODE: execution

CONTEXT:
- Repo: /path/to/fityez
- Stack: Next.js App Router, TypeScript, Supabase, TanStack Query.

SCOPE:
- In: athlete list loading, error state, and relevant tests.
- Out: database schema changes, RLS policy changes, dashboard redesign, unrelated lint cleanup.

RULES:
- The fix is accepted only if the athlete list handles loading, success, and error states without console errors.
- Preserve existing user changes in the worktree.

SOURCES:
- Repo code, AGENTS.md, docs/, existing tests.

METHOD:
- Inspect project instructions and current git state.
- Find the athlete list data path.
- Implement the smallest coherent fix.
- Add or update focused tests.
- Run type check and relevant tests.

OUTPUT:
- Final response with changed files, validation commands, and unresolved risks.

ON CONFLICT:
- If docs and code disagree, follow code behavior and flag the doc mismatch.

STOP CONDITION:
- Halt before schema, RLS, dependency, or auth-flow changes.

DONE CRITERIA:
- Relevant validation passes and the scoped dashboard behavior is implemented.
```

## Review Loop

Weak:

```text
Review this PR.
```

Stronger:

```text
# PROJECT: FitYez web app

GOAL: Review the current branch diff for user-facing regressions, data-access risks, and missing tests.

MODE: review

SCOPE:
- In: changed files in the current branch against main.
- Out: implementing fixes, broad architecture redesign, unrelated style comments.

RULES:
- Report only actionable findings with evidence and plausible user impact.
- Order findings by severity.
- Include file and line references for code findings.

SOURCES:
- Local git diff, AGENTS.md, docs/, relevant existing tests.

METHOD:
- Inspect branch status and diff.
- Read surrounding code for each risky change.
- Validate whether each suspected issue is real before reporting.

OUTPUT:
- Findings first.
- Then open questions.
- Then a short residual-risk summary.

ON CONFLICT:
- If docs and code disagree, cite both and do not assume intent.

STOP CONDITION:
- Halt and ask if the baseline branch cannot be determined.
```
