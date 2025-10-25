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

{% for post in paginator.posts %}

  {% if forloop.first and paginator.page == 1 %}
    
    <!-- 
      START: First Post (Full Content)
      We are already inside a container from "layout: page".
      So we directly output the content of the first post without an extra wrapper div.
    -->
    
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

    <!-- END: First Post (Full Content) -->


  {% else %}
    
    <!-- Other posts will be displayed as previews -->
    {% include post_preview.html post=post %}
    
  {% endif %}

{% endfor %}

{% include pagination.html %}
