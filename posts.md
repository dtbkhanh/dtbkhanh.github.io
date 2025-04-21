---
layout: default
title: Blog Posts
permalink: /posts/
---

# Blog Posts

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date: "%B %d, %Y" }}
      {% if post.excerpt %}
        <p><small>{{ post.excerpt | strip_html | truncatewords: 20 }}</small></p>
      {% endif %}
    </li>
  {% endfor %}
</ul>
