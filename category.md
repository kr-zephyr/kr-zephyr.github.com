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
<br/>
{% endfor %}

<!--
<h3>devops-diary 카테고리의 모든 POST들</h3>

{% for post in site.categories.devops-diary %}
    {% if post.title != nil %}
<li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endif %}
{% endfor %}

<h3>카테고리 목록을 뽑아보자</h3>

{% for category in site.categories %}
<li>{{ category | first }}</li>
{% endfor %}
-->
