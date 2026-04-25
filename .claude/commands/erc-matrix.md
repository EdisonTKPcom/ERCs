---
description: Regenerate reports/erc-matrix.md from current ERCS/ frontmatter
---

Regenerate `reports/erc-matrix.md` from the YAML frontmatter of every file
under `ERCS/`.

The exact aggregation logic is documented in `reports/README.md`. Run that
one-liner (or an equivalent `python3` script) to produce the new content,
then write it to `reports/erc-matrix.md`.

The output file must contain, in this order:

1. A short header with the generation date and total proposal count.
2. **Status × Type** table.
3. **Status × Category** table (Standards Track only).
4. **By year** table of `created` year × `status`.
5. Totals row at the bottom of each table.

After writing, show a `git diff --stat reports/erc-matrix.md` and a
summary of which counts changed since the previous snapshot.

Do not modify any other files. Do not wire the report into the Jekyll
build — it is a static snapshot.
