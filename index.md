---
layout: default
---

# Welcome to my personal website!☁️
[Know more about author!](./about.html).

Latest posts

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

