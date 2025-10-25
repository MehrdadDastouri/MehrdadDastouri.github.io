---
layout: page
permalink: /blog/
title: Blog
description: "Daily notes, tips, and insights on AI, technology, and more."
nav: true
nav_order: 1
pagination:
  enabled: true
  collection: posts
  permalink: /page/:num/
  per_page: 5
  sort_field: date
  sort_reverse: true
  trail:
    before: 2
    after: 2
---

<!-- 
  START: Mobile-only Fallback Menu for the Blog Page.
  This menu appears only on mobile screens because the main hamburger menu breaks here.
-->
<style>
  .fallback-menu {
    display: none; /* Hidden by default on large screens */
    background-color: #333;
    padding: 10px 0;
    text-align: center;
    margin-bottom: 2rem;
    border-radius: 5px;
  }
  .fallback-menu a {
    color: white;
    padding: 10px 15px;
    text-decoration: none;
    font-size: 1rem;
    font-weight: bold;
  }
  @media (max-width: 768px) {
    .fallback-menu {
      display: block; /* Visible only on screens smaller than 768px */
    }
  }
</style>

<div class="fallback-menu">
  <a href="{{ '/' | relative_url }}">Home</a>
  <a href="{{ '/about/' | relative_url }}">About</a>
  <a href="{{ '/projects/' | relative_url }}">Projects</a>
  <a href="{{ '/publications/' | relative_url }}">Publications</a>
</div>
<!-- END: Mobile-only Fallback Menu -->


{% for post in paginator.posts %}
  {% if forloop.first and paginator.page == 1 %}
    
    <!-- Display the first post with FULL content -->
    <h2 class="post-title" style="margin-bottom: 0.5rem;">
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    </h2>
    <p class="post-meta">
      <span>
        <i class="fa-solid fa-calendar-days"></i>
        {% assign date_format = site.date_format | default: "%B %-d, %Y" %}
        {{ post.date | date: date_format }}
      </span>
      {% if post.tags and post.tags.size > 0 %}
      &nbsp; &middot; &nbsp;
        <span>
          <i class="fa-solid fa-hashtag"></i>
          {% for tag in post.tags %}
            <a href="{{ '/blog/tag/' | append: tag | relative_url }}">{{ tag }}</a>
            {% unless forloop.last %}&nbsp;{% endunless %}
          {% endfor %}
        </span>
      {% endif %}
    </p>

    <div class="post-content-full" style="margin-top: 1.5rem;">
      {{ post.content }}
    </div>
    <hr style="margin-top: 2rem; margin-bottom: 2rem;">

  {% else %}
    
    <!-- Other posts will be displayed as previews -->
    {% include post_preview.html post=post %}
    
  {% endif %}
{% endfor %}

{% include pagination.html %}
