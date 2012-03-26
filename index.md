---
layout: default
description: "这是Fooleap的个人博客，记录学习生活的点点滴滴。"
---
{% include JB/setup %}

  <ul class="posts">
    {% for post in site.posts limit:1 %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}" title="{{ post.title }}" rel="bookmark">{{ post.title }}</a></li>
   <div class="lastpost">
    {{ post.description}}
    <a href="{{ post.url }}" title="Read More" rel="nofollow">(More...)</a>
   </div>
    {% endfor %}

    {% for post in site.posts limit:9 offset:1  %}
    <li><span>{{ post.date | date_to_string }}</span>&raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
