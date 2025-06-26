---
layout: page
title: Tags
permalink: /tags/
---

<style>
  .tags-filter {
    margin-bottom: 2rem;
    display: flex;
    flex-wrap: wrap;
  }

  .tag-pill {
    display: inline-block;
    background-color: #4a90e2;
    color: white;
    font-weight: 600;
    padding: 6px 14px;
    margin: 0 0.6rem 0.6rem 0;
    border-radius: 20px;
    cursor: pointer;
    text-decoration: none;
    user-select: none;
    transition: background-color 0.3s ease;
  }

  .tag-pill:hover,
  .tag-pill.active {
    background-color: #357ABD;
  }

  .posts-grid {
    display: flex;
    flex-direction: column;
    gap: 2rem;
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

  .post-categories {
    margin: 0.5rem 0;
  }

  .post-category {
    display: inline-block;
    background-color: #f0f0f0;
    color: #333;
    padding: 2px 8px;
    margin-right: 0.5rem;
    border-radius: 12px;
    font-size: 0.85rem;
    text-decoration: none;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .post-category:hover {
    background-color: #e0e0e0;
    text-decoration: none;
  }

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

<!-- Tags Filter Pills -->
<h1 class="page-heading">Tags</h1>
<div class="tags-filter" id="tags-bar">
  <span class="tag-pill active" data-tag="all">All</span>
  {% assign tags_sorted = site.tags | sort %}
  {% for tag in tags_sorted %}
    {% assign tag_slug = tag[0] | downcase | replace: ' ', '-' %}
    <span class="tag-pill" data-tag="{{ tag_slug }}">{{ tag[0] }} ({{ tag[1].size }})</span>
  {% endfor %}
</div>

<!-- Posts Grid -->
<h1 class="page-heading">All Posts</h1>
<div class="posts-grid" id="posts-grid">
  {% for post in site.posts %}
    {% assign taglist = post.tags | join: '|' | downcase | replace: ' ', '-' %}
    <div class="post-card" data-tags="{{ taglist }}">

      {% if post.cover %}
        <div class="post-card-image">
          <a href="{{ post.url | relative_url }}">
            <img src="{{ post.cover | relative_url }}" alt="Cover image for {{ post.title }}">
          </a>
        </div>
      {% elsif post.thumbnail %}
        <div class="post-card-image">
          <a href="{{ post.url | relative_url }}">
            <img src="{{ post.thumbnail | relative_url }}" alt="Cover image for {{ post.title }}">
          </a>
        </div>
      {% elsif post.image %}
        <div class="post-card-image">
          <a href="{{ post.url | relative_url }}">
            <img src="{{ post.image | relative_url }}" alt="Cover image for {{ post.title }}">
          </a>
        </div>
      {% endif %}

      <div class="post-card-content">
        <span class="post-meta">{{ post.date | date: "%B %d, %Y" }}</span>

        {% if post.categories %}
          <div class="post-categories">
            {% for cat in post.categories %}
              <span class="post-category">
                {{ cat }}
              </span>
            {% endfor %}
          </div>
        {% endif %}

        <h3>
          <a class="post-link" href="{{ post.url | relative_url }}">
            {{ post.title | escape }}
          </a>
        </h3>

        {% if site.show_excerpts %}
          <p>{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
        {% endif %}
      </div>
    </div>
  {% endfor %}
</div>

<script>
  document.addEventListener('DOMContentLoaded', function () {
    const tagsBar = document.getElementById('tags-bar');
    const postsGrid = document.getElementById('posts-grid');
    const posts = postsGrid.querySelectorAll('.post-card');
    const tagPills = tagsBar.querySelectorAll('.tag-pill');

    function filterPosts(tag) {
      posts.forEach(post => {
        const tags = post.dataset.tags;
        if (tag === 'all' || (tags && tags.split('|').includes(tag))) {
          post.style.display = 'flex';
        } else {
          post.style.display = 'none';
        }
      });
    }

    function setActiveTag(selectedTag) {
      tagPills.forEach(pill => {
        pill.classList.toggle('active', pill.dataset.tag === selectedTag);
      });
    }

    tagsBar.addEventListener('click', function (e) {
      if (e.target.classList.contains('tag-pill')) {
        const tag = e.target.dataset.tag;
        filterPosts(tag);
        setActiveTag(tag);
        
        // Update URL without page reload
        const newUrl = tag === 'all' ? 
          window.location.pathname : 
          `${window.location.pathname}?tag=${tag}`;
        window.history.pushState({ tag: tag }, '', newUrl);
      }
    });

    window.filterByTag = function (event, tag) {
      event.preventDefault();
      filterPosts(tag);
      setActiveTag(tag);
      tagsBar.scrollIntoView({ behavior: 'smooth' });
    }

    // Handle browser back/forward buttons
    window.addEventListener('popstate', function(e) {
      const tag = e.state?.tag || 'all';
      filterPosts(tag);
      setActiveTag(tag);
    });

    // Initialize based on URL parameter
    const urlParams = new URLSearchParams(window.location.search);
    const initialTag = urlParams.get('tag') || 'all';
    filterPosts(initialTag);
    setActiveTag(initialTag);
    
    if (initialTag !== 'all') {
      tagsBar.scrollIntoView({ behavior: 'smooth' });
    }
  });
</script>