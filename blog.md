---
layout: default
title: "Blog"
permalink: /blog/
---

# Blog

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      {% if post.date %}
        &mdash; <small>{{ post.date | date: "%B %e, %Y" }}</small>
      {% endif %}
    </li>
  {% endfor %}
</ul>
