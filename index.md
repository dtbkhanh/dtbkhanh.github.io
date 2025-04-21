---
layout: default
title: Home
---

<div align="center">
  <img src="/assets/images/github_profilepic.png" alt="Khanh's profile photo" width="120" style="border-radius: 100%;"/>
  <h1>Hi, I’m Khanh!</h1>
  <p><em>Data Analytics Specialist</em></p>
  <p>Python | SQL | Power BI | Tableau | Looker Studio </p>
</div>


<div style="display: flex; justify-content: space-around; margin-bottom: 20px;">
  <a href="/about" style="text-decoration: none; width: 200px;">
    <div style="border: 1px solid #ccc; padding: 15px; border-radius: 5px; text-align: center; height: 150px; display: flex; flex-direction: column; justify-content: center;">
      <span style="font-size: 1.5em;">👤</span><br>
      <strong>About Me</strong><br>
      <span style="font-size: 0.9em;">Learn about my background and journey.</span>
    </div>
  </a>
  <a href="/posts/" style="text-decoration: none; width: 200px;">
    <div style="border: 1px solid #ccc; padding: 15px; border-radius: 5px; text-align: center; height: 150px; display: flex; flex-direction: column; justify-content: center;">
      <span style="font-size: 1.5em;">📝</span><br>
      <strong>Blog Posts</strong><br>
      <span style="font-size: 0.9em;">Dive into data-driven case studies and stories.</span>
    </div>
  </a>
  <a href="https://github.com/dtbkhanh/Data-Analytics-and-Reports" style="text-decoration: none; width: 200px;">
    <div style="border: 1px solid #ccc; padding: 15px; border-radius: 5px; text-align: center; height: 150px; display: flex; flex-direction: column; justify-content: center;">
      <span style="font-size: 1.5em;">📊</span><br>
      <strong>Dashboards & Reports</strong><br>
      <span style="font-size: 0.9em;">Explore my analytics projects.</span>
    </div>
  </a>
</div>

---
<div align="center" style="margin-top: 20px;">
  <h2>🆕 Latest Insights 🆕</h2>
</div>

{% assign post = site.posts.first %}
- **<span style="font-size: 1.2em;">[{{ post.title }}]({{ post.url }})</span>**
  <br><small>{{ post.date | date: "%B %d, %Y" }}</small>
  {% if post.excerpt %}
    <p><small>{{ post.excerpt | strip_html | truncatewords: 20 }}</small></p>
  {% endif %}

---

<div align="center" style="margin-top: 10px;">
  <h2>🤝 Let's Connect 🤝</h2>
  <a href="https://www.linkedin.com/in/dtbkhanh/">
    <img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn">
  </a>
  <a href="https://dtbkhanh.github.io/">
    <img src="https://img.shields.io/badge/Blog-blue?style=for-the-badge&logo=bookstack&logoColor=white" alt="Blog">
  </a>
  <a href="https://github.com/dtbkhanh">
    <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub">
  </a>
</div>

<div align="center" style="margin-top: 5px;">
  <small>Feel free to reach out and connect!</small>
</div>
