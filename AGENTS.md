# Skills Documentation

This document describes how skills should be structured and maintained in this repository.

## Repository Scope

This repository is the canonical source for official Kilo skills. Add focused, reusable workflows that are maintained by Kilo and work in Kilo Code, Kilo CLI, or other apps implementing the open [Agent Skills standard](https://agentskills.io/).

Do not add MCP server definitions, agent configurations, general product documentation, or third-party skill mirrors here. Those belong in their source repositories or in Kilo Marketplace.

## What Is a Skill?

A skill is a modular, self-contained package that gives an AI agent specialized knowledge, workflows, and optional tools for a specific class of tasks. A good skill solves a real, repeatable problem and provides enough guidance for an agent to complete it safely and consistently.

## Skill Directory Structure

Every skill must live under `skills/<skill-name>/` and contain a `SKILL.md` file. Add bundled resources only when they are needed by the workflow.

```text
skills/
└── skill-name/
    ├── SKILL.md          # Required: main skill definition
    ├── scripts/          # Optional: executable helpers
    ├── references/       # Optional: documentation loaded as needed
    ├── assets/           # Optional: templates, images, or other resources
    └── examples/         # Optional: representative examples
```

Use lowercase kebab-case for skill directory names. Keep resources inside the skill directory so the skill remains portable.

## SKILL.md Structure

### Frontmatter

Every `SKILL.md` must begin with YAML frontmatter:

```yaml
---
name: skill-name
description: This skill should be used when the user needs a specific, repeatable workflow.
license: Apache-2.0
metadata:
  category: development
  author: Kilo
  version: 1.0.0 # Optional
  suggest_for: # Optional; include only strong relevance signals
    filename:
      - "*.component.ts"
    vscode_extension:
      - ms-toolsai.jupyter
---
```

| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Unique kebab-case identifier matching the directory name |
| `description` | Yes | Clear description of what the skill does and when it should load |
| `license` | Yes* | SPDX identifier; use `Apache-2.0` for original Kilo material |
| `metadata` | No | Container for additional metadata |
| `metadata.category` | No | Broad category such as `development`, `data`, or `productivity` |
| `metadata.author` | No | Author or maintaining organization |
| `metadata.version` | No | Semantic version when the skill is versioned independently |
| `metadata.suggest_for` | No | Container for high-confidence suggestion signals |
| `metadata.suggest_for.filename` | No | Non-empty list of distinctive filename globs such as `"*.component.ts"` |
| `metadata.suggest_for.vscode_extension` | No | Non-empty list of exact VS Code extension IDs such as `ms-toolsai.jupyter` |
| `metadata.source` | No | Source information for material maintained elsewhere |
| `metadata.source.repository` | No | URL of the canonical source repository |
| `metadata.source.path` | No | Path to the skill within the source repository |
| `metadata.source.license_path` | Yes* | License path in the source repository; alternative to `license` |

Either `license` or `metadata.source.license_path` is required, but not both. Do not add `metadata.source` to original Kilo skills because this repository is their canonical source. When importing or adapting third-party material, preserve its attribution and licensing terms and identify its canonical source.

Suggestion metadata is intentionally conservative. Add it only when the filename or installed VS Code extension strongly indicates that the exact skill is relevant; supporting a format is not sufficient. Filename values must use forms such as `"*.ipynb"` or `"*.component.ts"`, not broad patterns such as `"*.ts"`. VS Code values must be exact publisher-extension IDs. If `suggest_for` is present, it must contain at least one of `filename` or `vscode_extension` and no other keys.

### Description

The description controls discovery and loading. It must explain both:

- What capability the skill provides
- The requests, files, or situations that should trigger it

Use direct, specific language. Avoid vague descriptions such as "helps with development" or keyword lists without context.

### Markdown Body

Write instructions for the agent, not marketing copy for the user. Include only sections that improve execution, typically:

- Purpose and supported use cases
- Decision points and prerequisites
- A step-by-step workflow
- Safety and error-handling requirements
- Validation or completion checks
- References to bundled resources

Keep `SKILL.md` focused. Move detailed background material into `references/`, deterministic operations into `scripts/`, and reusable output files into `assets/`.

## Authoring Requirements

Every skill must:

1. Solve a real, repeatable problem.
2. Avoid duplicating an existing skill.
3. Use the minimum instructions and resources necessary.
4. Document required tools, dependencies, credentials, and environment variables.
5. Validate inputs at trust boundaries and confirm destructive operations.
6. Include a clear verification step when output can be tested.
7. Work without assuming a fixed installation path.
8. Use relative resource paths resolved from the loaded skill directory.
9. Preserve third-party notices, licenses, and attribution.
10. Avoid secrets, generated output, and unnecessary binary files.

## Scripts and Resources

- Prefer standard-library or already-available tooling over new dependencies.
- Make scripts deterministic, narrowly scoped, and safe to rerun where practical.
- Provide actionable errors and return a non-zero exit code on failure.
- Do not make network requests or modify user data unless the skill's purpose requires it.
- Never hard-code credentials, machine-specific paths, or assumptions about the current workspace.
- Reference bundled files by paths relative to the skill directory.

## Testing

Before submitting a skill, validate its frontmatter, referenced files, representative prompts, bundled scripts, and expected failure cases.

## Pull Requests

All changes to the default branch must go through a focused pull request and receive an approving review.
