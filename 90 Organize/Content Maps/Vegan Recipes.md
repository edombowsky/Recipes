---
cssclasses:
  - cards
  - cards-1-1
  - cards-cover
created: 2025.04.16 22:38:54.000 -0700
updated: 2025.07.11 17:28:31.349 -0700
obsidianUIMode: preview
dvLimit: 10
tags:
  - map
---
`INPUT[slider(minValue(10), maxValue(200), defaultValue(100), stepSize(25), addLabels(true)):dvLimit]` *(`VIEW[{dvLimit}]`)*

```dataview
table without id 
      link(file.link) as "Recipe", 
      choice(banner, embed(link(meta(default(banner,[[]])).path,"200")), "") as ""
from "Recipes"
where  vegan = true
sort filename desc
limit this.dvLimit
```
