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

<h5>Categories</h5>
{% for category in site.categories %}
    {% assign cat = category[0] %}
    <h6><a href="#">{{ cat }}</a></h6>
    {% for post in site.categories[cat] %}
        <a href="{{ post.url }}">{{ post.title }}</a> <small>{{ post.date }}</small>
    {% endfor %}
{% endfor %}

