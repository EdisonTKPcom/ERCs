# Reports

Generated reports about the contents of this repository.

## `erc-matrix.md`

A snapshot of every proposal under `ERCS/` broken down by `status`, `type`,
`category`, and creation year. The frontmatter of each `ERCS/*.md` file is
parsed and aggregated.

### Regenerate

From the repository root, run:

```sh
python3 - <<'PY' > reports/erc-matrix.md
import os, re, collections, datetime

d = 'ERCS'
STATUSES = ['Draft', 'Review', 'Last Call', 'Final', 'Stagnant', 'Withdrawn', 'Living']
TYPES = ['Standards Track', 'Meta', 'Informational']

rows = []
for f in sorted(os.listdir(d)):
    if not f.endswith('.md'):
        continue
    with open(os.path.join(d, f), encoding='utf-8', errors='replace') as fh:
        txt = fh.read()
    m = re.match(r'^---\s*\n(.*?)\n---', txt, re.DOTALL)
    if not m:
        continue
    fm = m.group(1)
    def g(key):
        mm = re.search(rf'^{key}\s*:\s*(.*?)\s*$', fm, re.MULTILINE)
        return mm.group(1).strip() if mm else ''
    rows.append((f, g('status'), g('type'), g('category'), g('created')))

total = len(rows)
today = datetime.date.today().isoformat()

print(f"# ERC status matrix\n")
print(f"_Auto-generated snapshot of every proposal under `ERCS/`. Last generated: {today}._\n")
print(f"This report aggregates the YAML frontmatter (`status`, `type`, `category`) of")
print(f"all {total} files currently in `ERCS/`. Re-run the command in")
print(f"`reports/README.md` to refresh it.\n")

print("## Status × Type\n")
header = "| Status | " + " | ".join(TYPES) + " | **Total** |"
sep = "|" + "---|" * (len(TYPES) + 2)
print(header); print(sep)
status_totals = collections.Counter(); type_totals = collections.Counter()
for s in STATUSES:
    counts = []; row_total = 0
    for t in TYPES:
        c = sum(1 for r in rows if r[1] == s and r[2] == t)
        counts.append(str(c) if c else '—'); row_total += c; type_totals[t] += c
    status_totals[s] = row_total
    print(f"| {s} | " + " | ".join(counts) + f" | **{row_total}** |")
print("| **Total** | " + " | ".join(f"**{type_totals[t]}**" for t in TYPES) + f" | **{total}** |\n")

cats = sorted({r[3] for r in rows if r[3]})
print("## Status × Category\n")
print("| Status | " + " | ".join(cats) + " | _(none)_ | **Total** |")
print("|" + "---|" * (len(cats) + 3))
for s in STATUSES:
    counts = []; row_total = 0
    for c in cats:
        n = sum(1 for r in rows if r[1] == s and r[3] == c)
        counts.append(str(n) if n else '—'); row_total += n
    n_none = sum(1 for r in rows if r[1] == s and not r[3])
    counts.append(str(n_none) if n_none else '—'); row_total += n_none
    print(f"| {s} | " + " | ".join(counts) + f" | **{row_total}** |")
print()

years = collections.Counter()
for r in rows:
    y = r[4][:4] if len(r[4]) >= 4 else 'unknown'
    years[y] += 1
print("## Proposals by creation year\n")
print("| Year | Count |"); print("|---|---|")
for y in sorted(years):
    print(f"| {y} | {years[y]} |")
print()

print("## Largest status buckets\n")
for s, n in status_totals.most_common():
    if n:
        print(f"- **{s}**: {n} ({n*100//total}%)")
print()

print("## Notes\n")
print("- Vocabulary follows [EIP-1](https://eips.ethereum.org/EIPS/eip-1).")
print("- `Standards Track` proposals in this repo carry `category: ERC` by convention.")
print("- Files without parseable frontmatter are omitted from totals.")
PY
```

The report is a static snapshot; regenerate after bulk status changes.
