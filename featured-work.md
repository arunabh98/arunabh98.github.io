---
layout: page
title: Featured Work
permalink: /featured-work/
---

<div class="featured-work">
  {% assign featured_posts = site.posts | where: "featured", true | sort: "date" | reverse %}
  
  {% for post in featured_posts %}
    <article class="work-item">
      <header>
        <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
        {% if post.subtitle %}
          <p class="post-subtitle">{{ post.subtitle }}</p>
        {% endif %}
        <p class="post-meta">
          <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %d, %Y" }}</time>
          {% if post.feature_type %}
            <span class="feature-type">{{ post.feature_type | capitalize }}</span>
          {% endif %}
        </p>
      </header>
      
      <div class="excerpt">
        {{ post.excerpt }}
      </div>
      
      {% if post.tags.size > 0 %}
      <div class="tags">
        {% for tag in post.tags %}
          <span class="tag">{{ tag }}</span>
        {% endfor %}
      </div>
      {% endif %}
      
      <a href="{{ post.url | relative_url }}" class="read-more">Read more →</a>
    </article>
  {% endfor %}
  
  {% if featured_posts.size == 0 %}
    <p>No featured work available at the moment. Check back soon!</p>
  {% endif %}
</div>