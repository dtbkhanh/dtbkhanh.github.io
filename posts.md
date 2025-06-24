---
layout: page
title: Blog
permalink: /posts/
---

<style>
  .categories-bar {
    margin-bottom: 2rem;
    display: flex;
    flex-wrap: wrap;
  }

  .category-pill {
    display: inline-block;
    background-color: #ff6f61;
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

  .category-pill:hover,
  .category-pill.active {
    background-color: #e65a4f;
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

<!-- Category Filter Pills -->
<h1 class="page-heading">Categories</h1>
<div class="categories-bar" id="categories-bar">
  <span class="category-pill active" data-category="all">All</span>
  {% assign categories = site.categories | sort %}
  {% for category in categories %}
    {% assign cat_name = category[0] %}
    <span class="category-pill" data-category="{{ cat_name | downcase | replace: ' ', '-' }}">
      {{ cat_name }} ({{ category[1].size }})
    </span>
  {% endfor %}
</div>

<!-- Posts Grid -->
<h1 class="page-heading">All Posts</h1>
<div class="posts-grid" id="posts-grid">
  {% for post in site.posts %}
    <div class="post-card" data-categories="{{ post.categories | map: 'downcase' | map: 'replace', ' ', '-' | join: '|' }}">

      {% if post.cover %}
        <div class="post-card-image">
          <a href="{{ post.url | relative_url }}">
            <img src="{{ post.cover | relative_url }}" alt="Cover image for {{ post.title }}">
          </a>
        </div>
      {% endif %}

      <div class="post-card-content">
        <span class="post-meta">{{ post.date | date: "%B %d, %Y" }}</span>

        {% if post.categories %}
          <div class="post-categories">
            {% for cat in post.categories %}
              <span class="post-category" onclick="filterByCategory(event, '{{ cat | downcase | replace: ' ', '-' }}')">
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
    const categoriesBar = document.getElementById('categories-bar');
    const postsGrid = document.getElementById('posts-grid');
    const posts = postsGrid.querySelectorAll('.post-card');
    const categoryPills = categoriesBar.querySelectorAll('.category-pill');

    function filterPosts(category) {
      posts.forEach(post => {
        const cats = post.dataset.categories;
        if (category === 'all' || (cats && cats.split('|').includes(category))) {
          post.style.display = 'flex';
        } else {
          post.style.display = 'none';
        }
      });
    }

    function setActiveCategory(selectedCategory) {
      categoryPills.forEach(pill => {
        pill.classList.toggle('active', pill.dataset.category === selectedCategory);
      });
    }

    categoriesBar.addEventListener('click', function (e) {
      if (e.target.classList.contains('category-pill')) {
        const category = e.target.dataset.category;
        filterPosts(category);
        setActiveCategory(category);
      }
    });

    window.filterByCategory = function (event, category) {
      event.preventDefault();
      filterPosts(category);
      setActiveCategory(category);
      categoriesBar.scrollIntoView({ behavior: 'smooth' });
    }

    filterPosts('all'); // Show all by default
  });
</script>