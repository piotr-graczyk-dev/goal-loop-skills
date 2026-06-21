# Prompt Patterns

Use these patterns only for the matching loop type. Keep the final prompt self-contained; do not refer to this file in the output.

## Research Loop

Use when the deliverable depends on external evidence, literature, official documentation, product pages, standards, repositories, or primary sources.

Require:

- A precise research question or table objective.
- Source hierarchy: primary first, then explicitly allowed secondary sources if any.
- Verification rule for each row, claim, or finding.
- Recency requirement when facts can change.
- Conflict handling for contradictory sources.
- Evidence output fields: source title, URL or locator, publication/update date when relevant, access date when browsing, and confidence.
- Exclusion rule for aggregators, summaries, SEO pages, low-quality sources, or unsourced claims.

Prefer this method:

```text
METHOD:
- Define the evidence schema before collecting sources.
- Search primary sources first.
- Record only findings that meet RULES.
- Deduplicate equivalent findings and preserve the strongest source.
- Flag conflicts instead of reconciling them silently.
- Produce a concise synthesis after the evidence table.
```

Common output fields:

- `finding`
- `source`
- `source_type`
- `date`
- `evidence`
- `confidence`
- `conflict_notes`

## Execution Loop

Use when the deliverable requires changes to files, code, docs, tests, pull requests, local artifacts, or operational steps.

Require:

- Target repo, branch, worktree, environment, or artifact location.
- Exact deliverable and user-visible behavior.
- In-scope files, modules, or issue IDs.
- Explicit exclusions.
- Validation commands and manual checks.
- Approval boundaries for network, dependencies, migrations, secrets, production systems, destructive actions, commits, or pushes.
- Handling for dirty worktrees and user changes.

Prefer this method:

```text
METHOD:
- Inspect repo instructions and current state before editing.
- Identify the smallest coherent implementation path.
- Edit only in-scope files.
- Preserve user changes and avoid unrelated cleanup.
- Run the requested validation commands.
- Report changed files, validation results, and unresolved risks.
```

Common done criteria:

- Implementation is complete for the stated scope.
- Relevant tests, type checks, or builds pass.
- Known limitations are listed.
- No unrelated changes are introduced.

## Review Loop

Use when the deliverable is critique, code review, prompt review, product review, architecture review, or risk assessment.

Require:

- Review target and baseline: branch, commit, diff, file set, document, or prompt.
- Review stance: bugs, correctness, security, UX, tests, maintainability, prompt quality, or all.
- Severity scale and evidence requirements.
- Whether fixes are out of scope.
- Output order: findings first, summary second.

Prefer this method:

```text
METHOD:
- Read the target and relevant context before judging.
- Prioritize concrete defects over style preferences.
- Tie every finding to evidence.
- Include file and line references when reviewing code.
- Avoid proposing broad rewrites unless the risk justifies it.
- If there are no findings, state residual risk and test gaps.
```

Common output fields:

- `severity`
- `location`
- `finding`
- `evidence`
- `impact`
- `suggested_fix`
