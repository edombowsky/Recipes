---
created: 2025.01.25 22:55:12.015 -0800
updated: 2025.07.11 17:27:26.170 -0700
dvLimit: 110
cssclasses:
  - cards
  - cards-1-1
  - cards-cover
obsidianUIMode: preview
tags: [map]
---

`INPUT[slider(minValue(10), maxValue(200), defaultValue(100), stepSize(25), addLabels(true)):dvLimit]` *(`VIEW[{dvLimit}]`)*

```dataview
table without id link(file.link) as "Recipe", choice(banner, embed(link(meta(default(banner,[[]])).path,"200")), "") as ""
from "Recipes"
where icontains(type, "recipe")
where tried = true
sort file.name asc
limit this.dvLimit
```
