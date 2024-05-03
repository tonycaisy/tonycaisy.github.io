---
title: Contents of Blogs
---

<ul>
  {% for blog in site.blogs %}
    <li>
      <a href="{{ blog.url }}">{{ blog.relative_path | replace: site.blogs.relative_directory, "" }}</a>
    </li>
  {% endfor %}
</ul>
