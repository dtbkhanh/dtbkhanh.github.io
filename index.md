---
layout: default
title: Home
---
<!-------------------------------------------------------------------------------------------------------------------------->
<!------------------------------------------------------ Introduction ------------------------------------------------------>
<!-------------------------------------------------------------------------------------------------------------------------->
<style>
.intro-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  margin-top: 40px;
  margin-bottom: 60px;
}

.intro-image {
  width: 140px;
  height: 140px;
  border-radius: 50%;
  overflow: hidden;
  margin-bottom: 20px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.intro-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.intro-title {
  font-size: 2.4em;
  font-weight: bold;
  margin-bottom: 10px;
  color: #333;
}

.intro-subtitle {
  font-size: 1.5em;
  font-style: italic;
  color: #666;
  margin-bottom: 10px;
}

.intro-skills {
  font-size: 1em;
  color: #444;
  margin-top: 10px;
}

@media (max-width: 600px) {
  .intro-title {
    font-size: 2em;
  }
  .intro-subtitle {
    font-size: 1.2em;
  }
}
</style>

<div class="intro-container">
  <div class="intro-image">
    <img src="/assets/images/github_profilepic.png" alt="Khanh's profile photo">
  </div>
  <div class="intro-title">Hi, I’m Khanh!</div>
  <div class="intro-subtitle">Data Analytics Specialist</div>
  <div class="intro-skills">
    Python &nbsp;|&nbsp; SQL &nbsp;|&nbsp; Power BI &nbsp;|&nbsp; Tableau &nbsp;|&nbsp; Looker Studio
  </div>
</div>

<div style="height: 2px; background-color: transparent; margin: 40px 0;"></div>

<!-------------------------------------------------------------------------------------------------------------------------->
<!-------------------------------------------------- Highlight containers -------------------------------------------------->
<!-------------------------------------------------------------------------------------------------------------------------->

<head>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
</head>

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

<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>


<!-------------------------------------------------------------------------------------------------------------------------->
<!------------------------------------------------------ Latest Blogs ------------------------------------------------------>
<!-------------------------------------------------------------------------------------------------------------------------->

<div align="center" style="margin-top: 20px;">
  <h2>LATEST INSIGHTS</h2>
</div>

<div style="display: flex; flex-wrap: wrap; align-items: flex-start; gap: 1.5rem; margin-top: 2rem;">
  {% assign latest_posts = site.posts | slice: 0, 3 %}  <!-- Get the latest 3 posts -->

  {% for post in latest_posts %}
    <div style="flex: 1 1 300px; max-width: 400px; margin: 0 auto;">
      {% if post.cover %}
        <a href="{{ post.url | relative_url }}">
          <img src="{{ post.cover | relative_url }}" alt="Cover for {{ post.title }}" style="width: 100%; height: auto; border-radius: 8px; object-fit: cover;">
        </a>
      {% endif %}
    </div>
    <div style="flex: 2 1 400px; min-width: 280px; text-align: justify; margin: 0 auto;">
      <h3 style="margin-top: 0;">
        <a href="{{ post.url | relative_url }}" style="text-decoration: none; color: inherit;">
          {{ post.title }}
        </a>
      </h3>
      <p style="margin: 0; color: gray; font-size: 0.9em;">{{ post.date | date: "%B %d, %Y" }}</p>
      {% if post.excerpt %}
        <p style="margin-top: 0.8rem; font-size: 1rem; line-height: 1.6;">{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
      {% endif %}
    </div>
  {% endfor %}
</div>

<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>


<!-------------------------------------------------------------------------------------------------------------------------->
<!------------------------------------------------------ Let's connect ----------------------------------------------------->
<!-------------------------------------------------------------------------------------------------------------------------->

<div align="center" style="margin-top: 10px;">
  <h2> LET'S CONNECT </h2>
  <a href="https://www.linkedin.com/in/dtbkhanh/">
    <img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn">
  </a>
  <a href="https://github.com/dtbkhanh">
    <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub">
  </a>
  <a href="https://sites.google.com/view/dtbkhanh">
    <img src="https://img.shields.io/badge/Creative%20Portfolio-FF5722?style=for-the-badge&logo=google&logoColor=white" alt="Creative Portfolio">
  </a>
</div>

<div align="center" style="margin-top: 5px;">
  <small>Feel free to reach out and connect!</small>
</div>
