# Goal Loop Skills

[![skills.sh](https://img.shields.io/badge/skills.sh-goal--loop--skills-000000)](#install-with-skillssh)

Reusable skills for designing and auditing long-running goal and loop prompts for agentic products.
They work best with tools that can load skills, run autonomous goals, or execute repeatable research, review, and implementation loops.

- `goal-loop-architect`: turns rough task intent into a launch-ready goal or loop prompt.
- `goal-loop-auditor`: reviews an existing goal or loop prompt for missing facts, weak scope, validation gaps, and hidden assumptions.

## Install

### Codex: Plugin Marketplace

Add this repository as a Codex plugin marketplace:

```bash
codex plugin marketplace add piotr-graczyk-dev/goal-loop-skills --ref main
```

Then open the Codex plugin browser, choose `Goal Loop Skills`, and install `goal-loop-skills`.

Start a new Codex thread after installing so the plugin-provided skills are loaded.

### Portable: Install With skills.sh

Use this path if you want the skills copied directly into your global agent skills directory without using the Codex plugin browser. This is the better fit for products that load skills from `~/.agents/skills/`.

Install both skills globally for the Codex agent:

```bash
npx skills add piotr-graczyk-dev/goal-loop-skills -g -a codex --skill '*' -y
```

Install one skill:

```bash
npx skills add piotr-graczyk-dev/goal-loop-skills -g -a codex --skill goal-loop-architect -y
```

List the available skills without installing:

```bash
npx skills add piotr-graczyk-dev/goal-loop-skills --list
```

Current `skills.sh` versions install global agent skills into `~/.agents/skills/`.
That is expected. Start a new thread or restart your agent product if the skills do not appear immediately.

For another supported agent, change the `-a codex` target or use the manual copy path below.

### Manual Fallback

If you want to copy the skills manually:

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/piotr-graczyk-dev/goal-loop-skills.git
cp -R goal-loop-skills/skills/goal-loop-architect ~/.agents/skills/
cp -R goal-loop-skills/skills/goal-loop-auditor ~/.agents/skills/
```

## Usage

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

## What Is Included

This package contains two skills:

- `goal-loop-architect`: use when you want a new prompt for a research loop, execution loop, review loop, monitoring loop, autonomous goal, or other long-running agent task.
- `goal-loop-auditor`: use when you already have a prompt and want to check whether it is specific, safe, and verifiable enough to launch.

The Codex plugin bundles the same two skills from `./skills/`. The skills themselves are plain skill directories and can be used by other products that support goal or loop workflows. They do not require external authentication, apps, MCP servers, hooks, or network credentials.

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

## Compatibility Notes

- `SKILL.md` files include the required `name` and `description` frontmatter.
- Optional OpenAI/Codex UI metadata lives in each skill's `agents/openai.yaml`.
- The plugin manifest uses relative `./skills/` component paths from the plugin root.
- The repo marketplace points at the public GitHub repository as a Git-backed plugin source.
- `skills.sh.json` groups both skills under `Goal Loops` for the skills.sh index.

## Contributing

Keep changes focused on reusable goal-loop prompt design and audit workflows. Do not add private paths, secrets, credentials, machine-specific assumptions, or project-specific workflow notes.

Before opening a PR, validate:

```bash
python3 /path/to/skill-creator/scripts/quick_validate.py skills/goal-loop-architect
python3 /path/to/skill-creator/scripts/quick_validate.py skills/goal-loop-auditor
python3 /path/to/plugin-creator/scripts/validate_plugin.py .
```

## License

MIT. See [LICENSE](LICENSE).
