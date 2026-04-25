---
description: List ERC proposals with status Stagnant for rescue triage
---

List every file under `ERCS/` whose frontmatter declares `status: Stagnant`,
sorted by `created` date (oldest first).

Use this command:

```sh
python3 - <<'PY'
import pathlib, re
rows = []
for p in sorted(pathlib.Path("ERCS").glob("*.md")):
    text = p.read_text(encoding="utf-8", errors="replace")
    m = re.match(r"---\n(.*?)\n---", text, re.S)
    if not m:
        continue
    fm = m.group(1)
    def field(k):
        mm = re.search(rf"^{k}:\s*(.+)$", fm, re.M)
        return mm.group(1).strip() if mm else ""
    if field("status").lower() == "stagnant":
        rows.append((field("created"), p.name, field("title")))
rows.sort()
print(f"{len(rows)} stagnant proposals")
for created, name, title in rows:
    print(f"- {created}  {name}  — {title}")
PY
```

Then print:

- The total count.
- The 10 oldest stagnant entries as candidates for rescue or withdrawal.

Do not modify any files.
