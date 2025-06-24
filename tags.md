---
layout: page
title: Tags
permalink: /tags/
---

<style>
  .tags-bar {
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
    border-bottom: 1px solid #e0e0e0;
    padding-bottom: 1.5rem;
  }

  .post-card h3 {
    margin-top: 0;
    margin-bottom: 0.5rem;
  }

  .post-card p {
    color: #555;
    font-size: 1rem;
    line-height: 1.6;
  }
</style>

<div class="tags-bar" id="tags-bar">
  <span class="tag-pill active" data-tag="all">All</span>
  {% assign tags_sorted = site.tags | sort %}
  {% for tag in tags_sorted %}
    {% assign tag_name = tag[0] %}
    {% assign tag_slug = tag_name | downcase | replace: ' ', '-' %}
    <span class="tag-pill" data-tag="{{ tag_slug }}">
      {{ tag_name }} ({{ tag[1].size }})
    </span>
  {% endfor %}
</div>

<div class="posts-grid" id="posts-grid">
  {% for post in site.posts %}
    {% assign post_tags_raw = post.tags | join: '|' | downcase %}
    {% assign post_tags_slug = post_tags_raw | replace: ' ', '-' %}
    <div class="post-card" data-tags="{{ post_tags_slug }}">
      <h3><a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a></h3>
      <p>{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
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
          post.style.display = 'block';
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
      }
    });

    // On page load, filter by URL query ?tag=some-tag if present
    function getQueryParam(param) {
      const params = new URLSearchParams(window.location.search);
      return params.get(param);
    }

    const initialTag = getQueryParam('tag');
    if (initialTag) {
      filterPosts(initialTag);
      setActiveTag(initialTag);
      // Scroll to tags bar smoothly
      tagsBar.scrollIntoView({ behavior: 'smooth' });
    } else {
      filterPosts('all');
    }
  });
</script>