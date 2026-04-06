---
created: 2025.03.17 12:35:53.313 -0700
updated: 2025.07.11 17:35:44.019 -0700
search_term: Condiment
dvLimit: 35
cssclasses:
  - cards
  - cards-1-1
  - cards-cover
tags:
  - map
obsidianUIMode: preview
---
**Meal Type:** `INPUT[inlineSelect(
    option(Breakfast),
    option(Brunch),
    option(Lunch),
    option(Dinner),
    option(Bread),
    option(Condiment),
    option(Dressing),
    option(Seasoning),
    option(Side),
    option(Snack),
    title(Meal Type)):search_term]` `INPUT[slider(minValue(10), maxValue(200), defaultValue(100), stepSize(25), addLabels(true)):dvLimit]` *(`VIEW[{dvLimit}]`)*
---

```dataview
table without id 
      link(file.link) as Recipe, 
      choice(banner, embed(link(meta(default(banner,[[]])).path,"200")), "") as ""
from "Recipes"
where this.search_term != null and
      this.search_term != "" and
      icontains(type, "recipe") and
      icontains(meal_type, this.search_term)
sort filename desc
limit this.dvLimit
```