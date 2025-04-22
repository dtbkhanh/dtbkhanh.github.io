---
layout: default
title: Home
---
<!-- Introduction -->
<div align="center">
  <img src="/assets/images/github_profilepic.png" alt="Khanh's profile photo" width="120" style="border-radius: 100%;"/>
  <h1>Hi, I’m Khanh!</h1>
  <p><em>Data Analytics Specialist</em></p>
  <p>Python | SQL | Power BI | Tableau | Looker Studio </p>
</div>

<!-- Highlight containers -->
<div class="card-container">
  <a href="/about" class="card">
    <div class="card-content">
      <span class="card-icon"><i class="fas fa-user"></i></span>
      <strong>About Me</strong>
      <span class="card-description">Learn about my background and journey.</span>
    </div>
  </a>
  <a href="/posts/" class="card">
    <div class="card-content">
      <span class="card-icon"><i class="fas fa-pen-nib"></i></span>
      <strong>Blog Posts</strong>
      <span class="card-description">Dive into data-driven case studies and stories.</span>
    </div>
  </a>
  <a href="https://github.com/dtbkhanh/Data-Analytics-and-Reports" class="card">
    <div class="card-content">
      <span class="card-icon"><i class="fas fa-chart-bar"></i></span>
      <strong>Dashboards & Reports</strong>
      <span class="card-description">Explore my analytics projects on GitHub.</span>
    </div>
  </a>
</div>

<style>
  .card-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    gap: 20px;
    margin-bottom: 20px;
  }
  
  .card {
    text-decoration: none;
    color: inherit;
    width: 300px;
    flex-grow: 1;
    min-width: 250px;
    max-width: 100%;
  }
  
  .card-content {
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 5px;
    text-align: center;
    height: 150px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    transition: all 0.3s ease;
  }
  
  .card-content:hover {
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    transform: translateY(-2px);
    border-color: #999;
  }
  
  .card-icon {
    font-size: 1.5em;
    margin-bottom: 5px;
  }
  
  .card-description {
    font-size: 0.9em;
    margin-top: 5px;
  }
  
  /* Mobile-specific styles */
  @media (max-width: 768px) {
    .card-container {
      flex-direction: column;
      align-items: center;
    }
    
    .card {
      width: 90%;
      max-width: 400px;
    }
    
    .card-content {
      height: auto;
      padding: 20px 10px;
    }
  }
</style>

---
<!-- Latest Blogs -->
<div align="center" style="margin-top: 20px;">
  <h2><i class="fas fa-lightbulb"></i> Latest Insights <i class="fas fa-lightbulb"></i></h2>
</div>

{% assign post = site.posts.first %}
- **<span style="font-size: 1.2em;">[{{ post.title }}]({{ post.url }})</span>**
  <br><small>{{ post.date | date: "%B %d, %Y" }}</small>
  {% if post.excerpt %}
    <p><small>{{ post.excerpt | strip_html | truncatewords: 20 }}</small></p>
  {% endif %}

---
<!-- Let's connect -->
<div align="center" style="margin-top: 10px;">
  <h2><i class="fas fa-handshake"></i> Let's Connect <i class="fas fa-handshake"></i></h2>
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
