---
layout: default
title: "Blog"
permalink: /blog/
---

# blog <a href="/blog/feed.xml" title="RSS Feed" style="text-decoration: none;"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="#f26522"><circle cx="6.18" cy="17.82" r="2.18"/><path d="M4 4.44v2.83c7.03 0 12.73 5.7 12.73 12.73h2.83c0-8.59-6.97-15.56-15.56-15.56zm0 5.66v2.83c3.9 0 7.07 3.17 7.07 7.07h2.83c0-5.47-4.43-9.9-9.9-9.9z"/></svg></a>

<ul class="post-list">
  {% for post in site.posts %}
    <li{% if post.featured %} class="featured"{% endif %}>
      {% if post.featured %}<span class="star"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="#f5c518"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/></svg></span>{% endif %}
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      {% if post.date %}
        &mdash; <small>{{ post.date | date: "%B %e, %Y" }}</small>
      {% endif %}
    </li>
  {% endfor %}
</ul>
