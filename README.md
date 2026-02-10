# Obsidian CLI Skill for Coding Agents

A reusable skill package for coding agents such as Codex and Claude Code, focused on automating Obsidian workflows from the terminal.

## Overview

This repository provides a self-contained skill directory that agents can load to:

- run common Obsidian-related terminal workflows,
- follow a structured operational guide,
- and expose compatible metadata for agent runtimes that support skill manifests.

The goal is to make note management and vault automation faster, more consistent, and easier to integrate into agent-driven development workflows.

## Repository Structure

- `obsidian-cli/SKILL.md`: Main skill instructions and operational flow.
- `obsidian-cli/references/commands.md`: Command reference for supported CLI actions.
- `obsidian-cli/agents/openai.yaml`: Agent-facing metadata/config for compatible runtimes.

## Installation

### Codex

Copy or symlink the `obsidian-cli/` folder into your Codex skills directory:

```bash
cp -R obsidian-cli "$CODEX_HOME/skills/"
# or
ln -s "$(pwd)/obsidian-cli" "$CODEX_HOME/skills/obsidian-cli"
```

### Other Agents

Any agent framework that supports folder-based skills can point directly to `obsidian-cli/`.

The primary entry point is `SKILL.md`, which includes frontmatter plus the execution guidance used by the agent.

## Usage Notes

- Keep `SKILL.md` as the source of truth for behavior and workflow steps.
- Extend `references/commands.md` as you add new CLI capabilities.
- Update `agents/openai.yaml` when your agent runtime requires additional metadata fields.

## Contributing

If you change command behavior or add new flows, update both:

1. `obsidian-cli/SKILL.md` (how the agent should act)
2. `obsidian-cli/references/commands.md` (what commands are available)

Keeping both files aligned helps avoid runtime confusion and keeps the skill reliable across agents.
