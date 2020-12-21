---
layout: page
title: "Sunflower Dojo and Design blog, Front Matter"
permalink: /
date: 2020-12-08T22:10:00-05:00
author: Mehron Kugler
---
<h1>Design, Coding, and Linux blog by Mehron Kugler</h1>

<nav>
  {% for item in site.data.navigation %}
    <a href="{{ item.link }}" {% if page.url == item.link %}style="color: red;"{% endif %}>
      {{ item.name }}
    </a>
  {% endfor %}
</nav>

<h1>Latest Posts</h1>

<ul>
  {% for post in site.posts limit:3 %}
    <li>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>
