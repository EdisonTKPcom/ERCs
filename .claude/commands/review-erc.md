---
description: Run the erc-reviewer subagent on a draft and print its review
argument-hint: <path-to-erc-file>
---

Invoke the `erc-reviewer` subagent on the file at: **$ARGUMENTS**.

Pass the file path through unchanged. The subagent will:

1. Read the file and a couple of accepted ERCs (e.g. `ERCS/erc-20.md`,
   `ERCS/erc-721.md`) for style comparison.
2. Check frontmatter, section structure, RFC 2119 boilerplate, copyright
   line, and EIP-1 conformance.
3. Return a markdown review with **Blocking issues**, **Recommendations**,
   and **Looks good** sections.

Print the subagent's review verbatim. Do not modify the ERC file.
