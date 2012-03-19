---
layout: default
#title: Home
#tagline: Supporting tagline
---
{% include JB/setup %}

最近的10篇日志

  {% for post in site.posts limit:10  %}
* {{ post.date | date_to_string }} &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
  {% endfor %}
