---
layout: default
description: "这是Fooleap的个人博客，记录学习生活的点点滴滴。"
---
{% include JB/setup %}

**最近的10篇日志**

  {% for npost in site.posts limit:1 %}
  <ul><li>{{ npost.date | date_to_string }} &raquo; <a href="{{ npost.url }}" title="{{ npost.title }}" rel="bookmark">{{ npost.title }}</a></li>

  <div class="home1">  {{ npost.description}}
  <a href="{{ npost.url }}" title="Read More" rel="nofollow">(More...)</a></div></ul>
  {% endfor %}
  {% for post in site.posts limit:9 offset:1  %}
* {{ post.date | date_to_string }} &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
  {% endfor %}
