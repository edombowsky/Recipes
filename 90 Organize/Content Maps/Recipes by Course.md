---
created: 2025.03.17 14:56:33.000 -0700
updated: 2025.07.11 17:35:14.279 -0700
cssclasses:
  - cards
  - cards-1-1
  - cards-cover
search_term: Dessert
tags:
  - map
dvLimit: 110
---

**Course:** `INPUT[inlineSelect(
    option(Appetizer),  
    option(Dessert),  
    option(Main),  
    option(Soup),  
    title(Course)):search_term]` `INPUT[slider(minValue(10), maxValue(200), defaultValue(100), stepSize(25), addLabels(true)):dvLimit]` *(`VIEW[{dvLimit}]`)*

```dataview
table without id 
      link(file.link) as "Recipe", 
      choice(banner, embed(link(meta(default(banner,[[]])).path,"200")), "") as ""
from "Recipes"
where this.search_term != null and
      this.search_term != "" and
      icontains(type, "recipe") and
      icontains(course, this.search_term)
sort filename desc
limit this.dvLimit
```
