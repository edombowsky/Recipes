---
cssclasses:
  - cards
  - cards-1-1
  - cards-cover
obsidianUIMode: preview
tags: [map]
dvLimit: 110
created: 2025.07.04 17:53:22.000 -0700
updated: 2025.07.11 17:31:57.464 -0700
---
`INPUT[slider(minValue(10), maxValue(200), defaultValue(100), stepSize(25), addLabels(true)):dvLimit]` *(`VIEW[{dvLimit}]`)*

```dataview
table without id 
      link(file.link) as "Recipe", 
      choice(banner, embed(link(meta(default(banner,[[]])).path,"200")), "") as ""
from "Recipes"
where favourite = true
sort filename desc
limit this.dvLimit
```
