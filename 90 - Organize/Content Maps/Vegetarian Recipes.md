---
cssclasses:
  - cards
  - cards-1-1
  - cards-cover
tags: [map]
dvLimit: 110
created: 2025.04.16 22:29:08.000 -0700
updated: 2025.07.11 17:29:19.433 -0700
obsidianUIMode: preview
---
`INPUT[slider(minValue(10), maxValue(200), defaultValue(100), stepSize(25), addLabels(true)):dvLimit]` *(`VIEW[{dvLimit}]`)*

```dataview
table without id 
      link(file.link) as "Recipe", 
      choice(banner, embed(link(meta(default(banner,[[]])).path,"200")), "") as ""
from "Recipes"
where  vegetarian = true
sort filename desc
limit this.dvLimit
```
