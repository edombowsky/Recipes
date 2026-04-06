---
created: 2025.03.17 12:47:03.000 -0700
updated: 2025.07.11 17:34:55.857 -0700
search_term: Italian
dvLimit: 10
cssclasses:
  - cards
  - cards-1-1
  - cards-cover
---

**Cuisine:** `INPUT[inlineSelect(
    option(American),
    option(Asian),
    option(British),
    option(Cajun),
    option(Canadian),
    option(Chinese),
    option(Egyptian),
    option(European),
    option(French),
    option(Greek),
    option(German),
    option(Hawaiian),
    option(Hungarian),
    option(Indian),
    option(Indonesian),
    option(International),
    option(Irish),
    option(Italian),
    option(Japanese),
    option(Kenyan),
    option(Korean),
    option(Lebanese),
    option(Malaysian),
    option(Maltese),
    option(Mediterranean),
    option(Mexican),
    option(Middle-Eastern),
    option(Moroccan),
    option(Persian),
    option(Polish),
    option(Spanish),
    option(TexMex),
    option(Thai),
    option(Tunisian),
    option(Turkish),
    option(Vietnamese),
    title(Cuisine)):search_term]` `INPUT[slider(minValue(10), maxValue(200), defaultValue(100), stepSize(25), addLabels(true)):dvLimit]` *(`VIEW[{dvLimit}]`)*
---

```dataview
table without id 
      link(file.link) as "Recipe", 
      choice(banner, embed(link(meta(default(banner,[[]])).path,"200")), "") as ""
from "Recipes"
where this.search_term != null and
      this.search_term != "" and
      icontains(type, "recipe") and
      icontains(cuisine, this.search_term)
sort filename desc
limit this.dvLimit
```