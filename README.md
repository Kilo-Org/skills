<h1 align="center">Kilo Skills</h1>

Official Kilo skills for data, development, and AI-agent workflows, built on the open [Agent Skills standard](https://agentskills.io/).

---

## What Are Kilo Skills?

Skills are self-contained packages that extend an AI agent with specialized knowledge and repeatable workflows. Each skill is a folder containing a `SKILL.md` file with metadata and instructions, plus any scripts, references, templates, or examples needed to complete the task.

This repository is the canonical source for skills maintained by Kilo. The skills are designed for Kilo Code, Kilo CLI, and any app that supports the Agent Skills standard.

**Key benefits:**

- **Portable**: Use the same skill across compatible AI agents
- **Auditable**: Review the instructions and bundled resources before use
- **Focused**: Load specialized guidance only when a task needs it
- **Reusable**: Share proven workflows across projects and teams

## Installation

Install all skills with the Skills CLI:

```bash
npx skills add Kilo-Org/skills
```

Install a specific skill:

```bash
npx skills add Kilo-Org/skills --skill <skill-name>
```

You can also copy an individual directory from `skills/` into the skills directory used by your app.

## Skill Structure

Each skill lives under `skills/` and follows this structure:

```text
skills/
└── skill-name/
    ├── SKILL.md          # Required: instructions and metadata
    ├── scripts/          # Optional: executable helpers
    ├── references/       # Optional: supporting documentation
    ├── assets/           # Optional: templates and resources
    └── examples/         # Optional: example inputs and outputs
```

A minimal `SKILL.md` starts with YAML frontmatter:

```markdown
---
name: skill-name
description: A clear description of what the skill does and when it should be used.
license: Apache-2.0
---

# Skill Name

Instructions for the agent.
```

See [AGENTS.md](AGENTS.md) for the repository's authoring requirements.

## Compatibility

Skills use the open Agent Skills format and are intended to work with Kilo and other compatible apps, including Claude Code, OpenAI Codex, Cursor, GitHub Copilot, Gemini CLI, OpenCode, Windsurf, and Cline.

Compatibility can vary when a skill depends on app-specific tools. Any such requirements must be documented in the skill.

## Contributing

Contributions should solve a real, repeatable problem and include clear instructions, practical examples, safe error handling, and appropriate validation. Before opening a pull request:

1. Check that an equivalent skill does not already exist.
2. Follow the structure and metadata requirements in [AGENTS.md](AGENTS.md).
3. Test the skill in Kilo and document any external requirements.
4. Submit the change through a pull request for review.

## Distribution

This repository is the canonical source for Kilo-maintained skills. Skills may also be listed in Kilo Marketplace, [skills.sh](https://skills.sh/), and other compatible catalogs, with those listings pointing back to this repository.

## License

This repository is licensed under the [Apache License 2.0](LICENSE). Bundled third-party material must preserve its original attribution and licensing terms.
