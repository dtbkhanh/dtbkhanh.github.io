---
layout: page
title: Blog
permalink: /posts/
---

<div class="home">
  <h1 class="page-heading">All Posts</h1>
  
  {%- if site.posts.size > 0 -%}
    <ul class="post-list">
      {%- for post in site.posts -%}
      <li>
        {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
        <span class="post-meta">{{ post.date | date: date_format }}</span>

        {%- if post.cover -%}
          <a class="post-link" href="{{ post.url | relative_url }}">
            <img src="{{ post.cover | relative_url }}" alt="{{ post.title | escape }}" style="max-width: 100%; height: auto; margin-bottom: 10px;" />
          </a>
        {%- endif -%}

        <h3>
          <a class="post-link" href="{{ post.url | relative_url }}">
            {{ post.title | escape }}
          </a>
        </h3>

        {%- if site.show_excerpts -%}
          {{ post.excerpt }}
        {%- endif -%}
      </li>
      {%- endfor -%}
    </ul>
  {%- endif -%}
</div>
