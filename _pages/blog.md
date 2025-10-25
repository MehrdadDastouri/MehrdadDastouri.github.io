    ---
    layout: blog
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
        <article class="post-preview">
          <h2 class="post-title">
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
    
          <div class="post-content-full">
            {{ post.content }}
          </div>
        </article>
        <hr>
      {% else %}
        {% include post_preview.html post=post %}
      {% endif %}
    
    {% endfor %}
    
    {% include pagination.html %}
