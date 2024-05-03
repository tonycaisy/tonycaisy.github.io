# Contents of Blogs

<ul>
  {% for blog in site.blogs %}
    <li>
      <a href="{{ blog.url }}">{{ blog.title }}</a>
    </li>
  {% endfor %}
</ul>
