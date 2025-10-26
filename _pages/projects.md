---
layout: page
title: projects
permalink: /projects/
description: "A collection of my research and personal projects in AI, Machine Learning, and DeFi."
nav: true
nav_order: 3
---

<!-- _pages/projects.md -->
<div class="projects-list">
  {% assign sorted_projects = site.projects | sort: "importance" %}
  {% if sorted_projects.size > 0 %}
    {% for project in sorted_projects %}
      {% include project_preview.liquid project=project %}
    {% endfor %}
  {% else %}
    <p>No projects have been added yet. Please check back later.</p>
  {% endif %}
</div>
