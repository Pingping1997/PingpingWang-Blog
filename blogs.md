---
layout: page
title: Blogs
permalink: /blogs/
description: "Personal blog posts"
header-img: img/bg-little-universe.jpg 
---

## 📝 My Blog Posts

<ul>
  {% assign entries = site.blogs | sort: "date" | reverse %}
  {% for b in entries %}
    <li>
      <a href="{{ b.url }}">{{ b.title }}</a>
      <small>— {{ b.date | date: "%B %d, %Y" }}</small>
      {% if b.subtitle %}<div><em>{{ b.subtitle }}</em></div>{% endif %}
      {% if b.tags %}<div>Tags: {{ b.tags | join: ", " }}</div>{% endif %}
    </li>
  {% else %}
    <li>Coming soon…</li>
  {% endfor %}
</ul>

(*This section includes my personal reflections, project updates, and thoughts on engineering, climate, and life.*)