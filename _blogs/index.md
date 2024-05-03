---
title: Contents of Blogs
---

<ul>
  {% assign cur_dir = "" %}
  {% for blog in site.blogs %}
    {% if blog.name != "index" %}
      <li>
        {% assign dir = blog.relative_path | replace: "_blogs/", "" | split: "/" | first %}
        {% if dir != cur_dir %}
          <h2>{{ dir }}:</h2>
          {% assign cur_dir = dir %}
        {% endif %}
        <a href="{{ blog.url }}">{{ blog.title | replace: "-", " " }}</a>
      </li>
    {% endif %}
  {% endfor %}
</ul>
