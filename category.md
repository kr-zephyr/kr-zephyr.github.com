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

###devops-diary 카테고리의 모든 POST들###

{% for post in site.categories.devops-diary %}
    {% if post.title != nil %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endif %}
{% endfor %}

###카테고리 목록을 뽑아보자...###

{% for category in site.categories %}
<li>{{ category | first }}</li>
{% endfor %}

###태그도 뽑아보자###

{% for tag in page.tags %}
<li>{{ tag | first }}</li>
{% endfor %}
