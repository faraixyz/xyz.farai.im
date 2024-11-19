---
date: 2023-02-07T20:07:15+02:00
tech: [python, excel]
tags: [wtf]
draft: false
---

I've got some pretty incel looking code in here.

```py
for row in range(5, 60):
    memcell = f"A{row}"
    idcell = f"D{row}"
    shcell = f"E{row}"
    divcell = f"F{row}"
    arrcell = f"G{row}"
    truecol = sheet[memcell].value + 3
    cells = [idcell, shcell, divcell, arrcell]
    for cell in cells:
        sheet[cell].value = re.sub(r"(\d+)(?!.*\d)", str(truecol), sheet[cell].value)
```

If anyone cares, I was trying to fix some misaligned formulas in Excel.
