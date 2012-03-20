---
layout: default
#title: Home
#tagline: Supporting tagline
---
{% include JB/setup %}

<h3>Welcome to my home page!</h3>

----------
**最近的10篇日志**
  {% for npost in site.posts limit:1 %}
  <ul><li>{{ npost.date | date_to_string }} &raquo; <a href="{{ npost.url }}" title="{{ npost.title }}" rel="bookmark">{{ npost.title }}</a></li>

  <div class="home1">  {{ npost.description}}
  <a href="{{ npost.url }}" title="Read More" rel="nofollow">(More...)</a></div></ul>
  {% endfor %}
  {% for post in site.posts limit:9 offset:1  %}
* {{ post.date | date_to_string }} &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
  {% endfor %}
