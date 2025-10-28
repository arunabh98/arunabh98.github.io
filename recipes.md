---
layout: page
title: Recipes
permalink: /recipes/
---

A collection of recipes I enjoy cooking and wanted to share. From quick weeknight meals to weekend experiments.

<div class="featured-work">
  {% assign recipe_posts = site.posts | where_exp: "post", "post.categories contains 'recipes'" | sort: "date" | reverse %}

  {% for post in recipe_posts %}
    <article class="work-item">
      <header>
        <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
        {% if post.subtitle %}
          <p class="post-subtitle">{{ post.subtitle }}</p>
        {% endif %}
        <p class="post-meta">
          <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %d, %Y" }}</time>
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

  {% if recipe_posts.size == 0 %}
    <p>No recipes yet. Check back soon for delicious content!</p>
  {% endif %}
</div>
