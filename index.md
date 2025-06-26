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
  <div class="intro-title">Hi, I'm Khanh!</div>
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

  /* Blog grid styles - matching posts/tags pages */
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

  .post-card-content h3 a {
    text-decoration: none;
    color: inherit;
  }

  .post-card-content h3 a:hover {
    color: #4a90e2;
  }

  .post-card-content p {
    margin: 0.5rem 0 0;
    color: #555;
    font-size: 1rem;
    line-height: 1.6;
  }

  .post-meta {
    color: gray;
    font-size: 0.9em;
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

  .section-title {
    text-align: center;
    margin-top: 20px;
    margin-bottom: 0;
  }
</style>

<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>

<!-------------------------------------------------------------------------------------------------------------------------->
<!------------------------------------------------------ Featured Blogs ----------------------------------------------------->
<!-------------------------------------------------------------------------------------------------------------------------->

<h2 class="section-title">FEATURED BLOGS</h2>

<div class="posts-grid">
  {% assign featured_posts = site.posts | where_exp: "post", "post.featured == true" | slice: 0, 3 %}

  {% for post in featured_posts %}
    <div class="post-card">
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
              <span class="post-category">
                {{ cat }}
              </span>
            {% endfor %}
          </div>
        {% endif %}

        <h3>
          <a href="{{ post.url | relative_url }}">
            {{ post.title | escape }}
          </a>
        </h3>

        {% if post.excerpt %}
          <p>{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
        {% endif %}
      </div>
    </div>
  {% endfor %}
</div>

<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>

<!-------------------------------------------------------------------------------------------------------------------------->
<!------------------------------------------------------ Latest Blogs ------------------------------------------------------>
<!-------------------------------------------------------------------------------------------------------------------------->

<h2 class="section-title">LATEST INSIGHTS</h2>

<div class="posts-grid">
  {% assign latest_posts = site.posts | slice: 0, 3 %}

  {% for post in latest_posts %}
    <div class="post-card">
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
              <span class="post-category">
                {{ cat }}
              </span>
            {% endfor %}
          </div>
        {% endif %}

        <h3>
          <a href="{{ post.url | relative_url }}">
            {{ post.title | escape }}
          </a>
        </h3>

        {% if post.excerpt %}
          <p>{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
        {% endif %}
      </div>
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