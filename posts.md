---
layout: page
title: Blog
permalink: /posts/
---

<style>
.posts-grid {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  margin-top: 2rem;
}

.post-card {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  border-bottom: 1px solid #e0e0e0;
  padding-bottom: 1rem;
}

.post-card-image img {
  width: 120px;
  height: 80px;
  object-fit: cover;
  border-radius: 6px;
}

.post-card-content {
  flex: 1;
}

.post-card-content h3 {
  margin-top: 0.2rem;
  margin-bottom: 0.4rem;
}

.post-card-content p {
  margin: 0.2rem 0 0;
  color: #666;
  font-size: 0.95rem;
}
</style>

<div class="home">
  <h1 class="page-heading">All Posts</h1>
  
  {%- if site.posts.size > 0 -%}
    <div class="posts-grid">
      {%- for post in site.posts -%}
      <div class="post-card">
        {%- if post.cover -%}
        <div class="post-card-image">
          <a href="{{ post.url | relative_url }}">
            <img src="{{ post.cover | relative_url }}" alt="Cover image for {{ post.title }}">
          </a>
        </div>
        {%- endif -%}
        <div class="post-card-content">
          <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
          <h3>
            <a class="post-link" href="{{ post.url | relative_url }}">
              {{ post.title | escape }}
            </a>
          </h3>
          {%- if site.show_excerpts -%}
            <p>{{ post.excerpt }}</p>
          {%- endif -%}
        </div>
      </div>
      {%- endfor -%}
    </div>
  {%- endif -%}
</div>
