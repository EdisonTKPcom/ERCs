---
description: Scaffold a new ERC draft under ERCS/ from erc-template.md
argument-hint: <short-title-slug>
---

Create a new ERC draft file for the topic: **$ARGUMENTS**.

Steps:

1. Copy `erc-template.md` to `ERCS/eip-draft_$ARGUMENTS.md` (lowercase, hyphens
   for spaces, no leading `eip-` in `$ARGUMENTS`).
2. Fill in the frontmatter using the conventions observed across existing
   files in `ERCS/`:
   - `status: Draft`
   - `type: Standards Track`
   - `category: ERC`
   - `created:` today's date in `yyyy-mm-dd` format.
   - Leave `author`, `discussions-to`, and the title placeholders for the
     user to complete, but pre-fill the title from `$ARGUMENTS`.
3. Remove all `TODO: Remove this comment before submitting` HTML comment
   blocks from the template before saving.
4. Do **not** assign an EIP number — editors do that on PR.
5. Print the path of the new file and a diff-style summary of the frontmatter
   you populated.

Do not modify any other files.
