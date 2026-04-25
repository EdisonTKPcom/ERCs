# Claude Code configuration

This directory contains shared [Claude Code](https://docs.claude.com/claude-code)
configuration for the ERCs repository. It is intentionally committed so every
contributor gets the same slash commands, agents, and tool permissions.

## Layout

- `settings.json` — shared project settings (tool permissions, deny-list).
  Committed.
- `settings.local.json` — personal overrides (API keys, local paths, extra
  permissions). **Not** committed (see `.gitignore`).
- `commands/` — project slash commands available as `/<filename>` in Claude
  Code sessions run from this repo.
- `agents/` — project-scoped subagents with repo-specific instructions.

## Commands

- `/new-erc` — scaffold a new ERC draft under `ERCS/` using `erc-template.md`.
- `/validate-erc` — lint an ERC's frontmatter against the conventions used
  across `ERCS/*.md` (status/type/category vocabulary).
- `/review-erc` — run the `erc-reviewer` subagent for a full editorial
  review against EIP-1.
- `/list-stagnant` — list `status: Stagnant` proposals (oldest first) for
  rescue triage.
- `/erc-matrix` — regenerate `reports/erc-matrix.md` from current
  frontmatter.

## Agents

- `erc-reviewer` — reviews an ERC draft for structural and editorial
  compliance with `erc-template.md` and EIP-1.
- `erc-security-auditor` — deeper review of the **Security Considerations**
  section against a standard threat-modeling checklist.

## Project memory

`CLAUDE.md` in this directory is loaded automatically by Claude Code on
every session. It captures the repository's frontmatter vocabulary,
required section order, build commands, and hard rules (e.g. never edit
`LICENSE.md`, never assign EIP numbers).

## Local overrides

To add personal permissions without committing them, create
`.claude/settings.local.json`:

```json
{
  "permissions": {
    "allow": ["Bash(open*)"]
  }
}
```
