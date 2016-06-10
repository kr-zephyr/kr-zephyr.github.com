---
layout: page
title: Category
permalink: /category/
---

{% for category in site.categories %}
<li><a name="{{ category | first }}">{{ category | first }}</a>
  <ul>
  {% for posts in category %}
    {% for post in posts %}
      {% if post.title != nil %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
      {% endif %}
    {% endfor %}
  {% endfor %}
  </ul>
</li>
{% endfor %}


devops-diary 카테고리의 모든 POST들 (변경해봄)
{% for category in site.categories.devops-diary %}
<li><a href="{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
