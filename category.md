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


devops-diary 카테고리의 모든 POST들 (변경해봄4)
- 포스트 목록을 읽어옴
  {% for post in site.categories.devops-diary %}
  - 포스트 목록에서 포스트를 읽어옴
    {% if post.title != nil %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endif %}
  {% endfor %}
