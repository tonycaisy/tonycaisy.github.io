---
title: Contents of Blogs
---

<ul>
  {% for blog in site.blogs %}
  {% if blog.name == "index.md" %}
    {% continue %}
  {% endif %}
    <li>
      <a href="{{ blog.url }}">{{ blog.relative_path | replace: "_blogs/", ""}}</a>
    </li>
  {% endfor %}
</ul>
