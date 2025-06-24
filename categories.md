---
layout: page
title: Categories
permalink: /categories/
---

<style>
  .category-list {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    margin-top: 2rem;
  }

  .category-item {
    background-color: #4a90e2;
    color: white;
    padding: 10px 18px;
    border-radius: 20px;
    font-weight: 600;
    text-decoration: none;
    transition: background-color 0.3s ease;
  }

  .category-item:hover {
    background-color: #357ABD;
  }
</style>

<h1>Categories</h1>

<div class="category-list">
  {% assign categories = site.categories | sort %}
  {% for category in categories %}
    {% assign category_name = category[0] %}
    {% assign posts_in_category = category[1] %}
    <a href="{{ '/categories/' | append: category_name | downcase | replace: ' ', '-' }}/" class="category-item">
      {{ category_name }} ({{ posts_in_category | size }})
    </a>
  {% endfor %}
</div>