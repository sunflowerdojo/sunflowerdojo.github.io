---
layout: page
title: "Sunflower Dojo and Design blog, Front Matter"
permalink: /
date: 2020-12-08T22:10:00-05:00
author: Mehron Kugler
---

It's a new look and feel for this blog site.
More coming soon.

<nav>
  {% for item in site.data.navigation %}
    <a href="{{ item.link }}" {% if page.url == item.link %}style="color: red;"{% endif %}>
      {{ item.name }}
    </a>
  {% endfor %}
</nav>
