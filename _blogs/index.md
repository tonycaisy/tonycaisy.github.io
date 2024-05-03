---
title: Contents of Blogs
---

<ul>
  {% assign cur_dir = "" %}
  {% for blog in site.blogs %}
    {% assign dirs = blog.relative_path | replace: "_blogs/", "" | split: "/" %}
    {% if dirs.last == "index.md" %}
      {% continue %}
    {% endif %}
    <li>
      {% if cur_dir != dirs.first %}
        <h2>{{ dirs.first }}:</h2>
        {% assign cur_dir = dirs.first %}
      {% endif %}
      <a href="{{ blog.url }}">{{ blog.title | replace: "-", " " }}</a>
    </li>
  {% endfor %}
</ul>
