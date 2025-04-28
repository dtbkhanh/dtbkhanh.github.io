---
layout: page
title: Blog
permalink: /posts/
---

<style>
.posts-grid {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  margin-top: 2rem;
}

.post-card {
  display: flex;
  flex-wrap: wrap;
  gap: 1.5rem;
  border-bottom: 1px solid #e0e0e0;
  padding-bottom: 1.5rem;
}

.post-card-image {
  flex: 1 1 300px;
  max-width: 400px;
}

.post-card-image img {
  width: 100%;
  height: auto;
  object-fit: cover;
  border-radius: 8px;
}

.post-card-content {
  flex: 2 1 400px;
  min-width: 280px;
  text-align: justify;
}

.post-card-content h3 {
  margin-top: 0.3rem;
  margin-bottom: 0.5rem;
}

.post-card-content p {
  margin: 0.5rem 0 0;
  color: #555;
  font-size: 1rem;
  line-height: 1.6;
}

/* Mobile responsiveness */
@media (max-width: 768px) {
  .post-card {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }
  
  .post-card-content {
    text-align: justify;
  }
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
          <span class="post-meta">{{ post.date | date: "%B %d, %Y" }}</span>
          <h3>
            <a class="post-link" href="{{ post.url | relative_url }}">
              {{ post.title | escape }}
            </a>
          </h3>
          {%- if site.show_excerpts -%}
            <p>{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
          {%- endif -%}
        </div>
      </div>
      {%- endfor -%}
    </div>
  {%- endif -%}
</div>
