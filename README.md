# Goal Loop Skills

[![skills.sh](https://skills.sh/b/piotr-graczyk-dev/goal-loop-skills)](https://skills.sh/piotr-graczyk-dev/goal-loop-skills)

Reusable Codex skills for designing and auditing long-running agent prompts. The package contains two skills:

- `goal-loop-architect`: turns rough task intent into a launch-ready Codex goal or loop prompt with explicit scope, source rules, validation, conflict handling, output contract, and stop conditions.
- `goal-loop-auditor`: reviews an existing goal or loop prompt for missing facts, ambiguous scope, weak validation rules, source-quality gaps, output-contract gaps, conflict handling, stop conditions, and hidden assumptions.

## Repository Layout

```text
.
├── .agents/plugins/marketplace.json
├── .codex-plugin/plugin.json
├── skills/
│   ├── goal-loop-architect/
│   │   ├── SKILL.md
│   │   ├── agents/openai.yaml
│   │   └── references/
│   └── goal-loop-auditor/
│       ├── SKILL.md
│       └── agents/openai.yaml
├── skills.sh.json
├── LICENSE
└── README.md
```

The `skills/` directory is compatible with the open agent skills layout used by `skills.sh`. The repository root is also a Codex plugin root through `.codex-plugin/plugin.json`.

## When To Use These Skills

Use `goal-loop-architect` when you want a new prompt for a research loop, execution loop, review loop, monitoring loop, autonomous goal, or other long-running Codex task. It is most useful when the task needs clear boundaries, validation rules, source hierarchy, output schema, permissions, and halt conditions.

Use `goal-loop-auditor` when you already have a prompt and want to check whether it is safe and specific enough to launch. It reports blocking gaps, high-risk ambiguity, and a corrected prompt when that can be done without inventing missing facts.

## Install With skills.sh

List the available skills:

```bash
npx skills add piotr-graczyk-dev/goal-loop-skills --list
```

Install both skills globally for Codex:

```bash
npx skills add piotr-graczyk-dev/goal-loop-skills -g -a codex --skill '*' -y
```

Install one skill:

```bash
npx skills add piotr-graczyk-dev/goal-loop-skills -g -a codex --skill goal-loop-architect -y
```

The `skills.sh.json` file groups both skills under `Goal Loops` on the skills.sh repository page once the repository is seen by the telemetry-backed index.

## Manual Codex Skill Installation

Codex reads global user skills from `~/.codex/skills/`. To install manually:

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/piotr-graczyk-dev/goal-loop-skills.git
cp -R goal-loop-skills/skills/goal-loop-architect ~/.codex/skills/
cp -R goal-loop-skills/skills/goal-loop-auditor ~/.codex/skills/
```

Start a new Codex thread or restart Codex if the skills do not appear immediately.

## Codex Plugin Usage

This repository includes a Codex plugin manifest at `.codex-plugin/plugin.json` and a repo marketplace at `.agents/plugins/marketplace.json`.

Add the marketplace:

```bash
codex plugin marketplace add piotr-graczyk-dev/goal-loop-skills --ref main
```

Then open the plugin browser in Codex, choose the `Goal Loop Skills` marketplace, and install `goal-loop-skills`. Start a new thread after installation so Codex loads the plugin-provided skills.

The plugin bundles the same two skills from `./skills/` and does not require external authentication, apps, MCP servers, hooks, or network credentials.

## Examples

Create a launch-ready execution goal:

```text
Use $goal-loop-architect to turn this into a complete execution-loop prompt:
ship issue #42 in repo owner/project, keep scope to the issue, run tests, open a PR, and stop if auth or CI access is missing.
```

Audit a draft prompt before launch:

```text
Use $goal-loop-auditor to review this goal prompt for missing scope, validation, source rules, permissions, and stop conditions:
[paste prompt]
```

## Compatibility Notes

- `SKILL.md` files include the required `name` and `description` frontmatter.
- Optional Codex UI metadata lives in each skill's `agents/openai.yaml`.
- The plugin manifest uses relative `./skills/` component paths from the plugin root.
- The repo marketplace points at the public GitHub repository as a Git-backed plugin source.

## Contributing

Issues and pull requests are welcome. Keep changes focused on reusable goal-loop prompt design and audit workflows. Do not add private paths, secrets, credentials, machine-specific assumptions, or project-specific workflow notes.

Before opening a PR, validate:

```bash
python3 /path/to/skill-creator/scripts/quick_validate.py skills/goal-loop-architect
python3 /path/to/skill-creator/scripts/quick_validate.py skills/goal-loop-auditor
python3 /path/to/plugin-creator/scripts/validate_plugin.py .
```

## License

MIT. See [LICENSE](LICENSE).
