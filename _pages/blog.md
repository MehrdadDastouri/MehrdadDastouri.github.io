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

<!-- TEST CODE -->
<h2>This is a test to check the menu.</h2>
<p>Below is a list of posts.</p>
<hr>

{% for post in paginator.posts %}
  
  {% if forloop.first and paginator.page == 1 %}
    <!-- Displaying ONLY the title of the first post -->
    <h3>FIRST POST: {{ post.title }}</h3>
    <hr>
  {% else %}
    <!-- Displaying ONLY the title of other posts -->
    <h3>{{ post.title }}</h3>
  {% endif %}

{% endfor %}

{% include pagination.html %}
