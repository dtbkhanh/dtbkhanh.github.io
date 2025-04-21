---
layout: default
title: Home
---

<div align="center">
  <img src="https://github.com/dtbkhanh.png" alt="Khanh's profile photo" width="120" style="border-radius: 50%;"/>
  <h1>Hi, I’m Khanh!</h1>
  <p><em>Data Analytics Specialist | Data Science Enthusiast | Lifetime Learner</em></p>
  <p>Python | SQL | Power BI | Tableau | Looker Studio </p>
</div>

---

## 📌 Explore

<div style="display: flex; justify-content: space-around; margin-bottom: 20px;">
  <a href="about.md" style="text-decoration: none;">
    <div style="border: 1px solid #ccc; padding: 15px; border-radius: 5px; text-align: center;">
      <span style="font-size: 1.5em;">👤</span><br>
      <strong>About Me</strong><br>
      Learn about my background and journey.
    </div>
  </a>
  <a href="/posts/" style="text-decoration: none;">
    <div style="border: 1px solid #ccc; padding: 15px; border-radius: 5px; text-align: center;">
      <span style="font-size: 1.5em;">📝</span><br>
      <strong>Blog Posts</strong><br>
      Dive into data-driven case studies and stories.
    </div>
  </a>
  <a href="https://github.com/dtbkhanh/Data-Analytics-and-Reports" style="text-decoration: none;">
    <div style="border: 1px solid #ccc; padding: 15px; border-radius: 5px; text-align: center;">
      <span style="font-size: 1.5em;">📊</span><br>
      <strong>Dashboards & Reports</strong><br>
      Explore my interactive analytics projects.
    </div>
  </a>
</div>

---

## 🆕 Latest Insights

{% assign post = site.posts.first %}
- **<span style="font-size: 1.2em;">[{{ post.title }}]({{ post.url }})</span>**
  <br><small>{{ post.date | date: "%B %d, %Y" }}</small>
  {% if post.excerpt %}
    <p><small>{{ post.excerpt | strip_html | truncatewords: 20 }}</small></p>
  {% endif %}

---

## 🤝 Let's Connect

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/dtbkhanh/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white)](https://github.com/dtbkhanh)

<div align="center" style="margin-top: 20px;">
  <small>Feel free to reach out and connect!</small>
</div>
