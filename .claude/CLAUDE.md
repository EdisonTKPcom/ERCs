# Repository guide for Claude Code

This file is loaded automatically as project memory by Claude Code. Keep it
concise — it is read on every session.

## What this repo is

A fork of the [ERCs](https://eips.ethereum.org/erc) repository. Proposals
live as Markdown files under `ERCS/`, each with a YAML frontmatter block.
The site is rendered with Jekyll from `_config.yml`, `_layouts/`, `_data/`,
and the contents of `ERCS/`.

`erc-template.md` at the repository root is the canonical template for a
new proposal.

## Frontmatter conventions

Vocabulary used across `ERCS/*.md`:

- `status`: `Draft` | `Review` | `Last Call` | `Final` | `Stagnant` |
  `Withdrawn` | `Living`
- `type`: `Standards Track` | `Meta` | `Informational`
- `category` (only when `type: Standards Track`): `Core` | `Networking` |
  `Interface` | `ERC`
- `created`: ISO 8601 (`yyyy-mm-dd`)
- `requires` (optional): list of EIP numbers

`title` must be ≤ 44 characters and must not repeat the EIP number.

Required sections, in order: `Abstract`, `Specification`, `Rationale`,
`Security Considerations`, `Copyright`. `Motivation`,
`Backwards Compatibility`, `Test Cases`, and `Reference Implementation`
are optional but conventional.

The `Copyright` section must read:

> Copyright and related rights waived via [CC0](../LICENSE.md).

If the spec uses RFC 2119 normative keywords (`MUST`, `SHOULD`, `MAY`,
…), include the RFC 2119 / RFC 8174 boilerplate sentence.

## Filenames

- New drafts: `ERCS/eip-draft_<slug>.md` (lowercase, hyphenated).
- Numbered proposals: `ERCS/erc-<n>.md` — number is assigned by an editor.
- Per-proposal assets live under `assets/eip-<n>/`.

## Build and serve

```sh
bundle install
bundle exec jekyll build
bundle exec jekyll serve
```

These commands are pre-allowed in `.claude/settings.json`.

## Slash commands available in this repo

- `/new-erc <slug>` — scaffold a new draft from `erc-template.md`.
- `/validate-erc <path>` — lint frontmatter and required sections.
- `/review-erc <path>` — run the `erc-reviewer` subagent for an
  editorial review against EIP-1.
- `/list-stagnant` — list proposals with `status: Stagnant`, useful for
  rescue triage.
- `/erc-matrix` — regenerate `reports/erc-matrix.md`.

## Subagents

- `erc-reviewer` — overall editorial review (template + EIP-1 conformance).
- `erc-security-auditor` — deeper review of the **Security Considerations**
  section against threat-modeling expectations.

## Hard rules for any change

1. **Never** edit `LICENSE.md`. It is denied in `settings.json` and the
   CC0 license is a project invariant.
2. **Never** assign or change an EIP number — that is an editor task.
3. **Never** rewrite git history or force-push.
4. Do not introduce non-normative external links inside the spec body
   (per EIP-1). Reference assets via `assets/eip-<n>/...`.
5. Touch only files relevant to the requested change. The repo is large
   (hundreds of ERCs); broad sweeps are almost always wrong.

## Reports

`reports/erc-matrix.md` is a static snapshot of status × type × category
across `ERCS/`. Regenerate it with `/erc-matrix` (or the one-liner in
`reports/README.md`) when the snapshot is stale. It is **not** part of
the Jekyll site build.
