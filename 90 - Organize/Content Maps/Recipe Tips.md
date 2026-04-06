---
created: 2024.09.28 18:35:49.179 -0700
updated: 2025.07.11 17:30:22.835 -0700
cssclasses:
  - cards
  - cards-1-1
  - cards-cover
obsidianUIMode: preview
tags: [map]
dvLimit: 110
---
`INPUT[slider(minValue(10), maxValue(200), defaultValue(100), stepSize(25), addLabels(true)):dvLimit]` *(`VIEW[{dvLimit}]`)*

```dataview
table without id link(file.link) as "Recipe", choice(banner, embed(link(meta(default(banner,[[]])).path,"200")), "") as ""
from "Recipes"
where icontains(type, "tip")
sort file.name asc
limit this.dvLimit
```
