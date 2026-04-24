---
description: Validate an ERC file's frontmatter and structure
argument-hint: <path-to-erc-file>
---

Validate the ERC file at: **$ARGUMENTS**.

Check the following and report each issue with a file path and reason:

1. **Frontmatter present**: file begins with a `---` fenced YAML block.
2. **Required keys** (based on `erc-template.md`):
   - `title` (<= 44 chars, no EIP number repeated in title)
   - `description` (one short sentence)
   - `author`
   - `discussions-to` (URL)
   - `status` — one of: `Draft`, `Review`, `Last Call`, `Final`, `Stagnant`,
     `Withdrawn`, `Living`.
   - `type` — one of: `Standards Track`, `Meta`, `Informational`.
   - `category` — required iff `type: Standards Track`; one of: `Core`,
     `Networking`, `Interface`, `ERC`.
   - `created` — `yyyy-mm-dd`.
   - `requires` — optional; numeric EIP numbers.
3. **Required sections**: `## Abstract`, `## Specification`, `## Rationale`,
   `## Security Considerations`, `## Copyright`.
4. **Copyright line**: must contain `CC0` and reference `../LICENSE.md`.
5. **RFC 2119 boilerplate**: if the spec uses MUST/SHOULD/MAY, the standard
   RFC 2119 / RFC 8174 sentence must be present.
6. **No leftover `TODO: Remove this comment before submitting`** markers.

Report `PASS` if all checks succeed, otherwise list each failure with a line
reference. Do not modify the file.
