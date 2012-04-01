---
layout: default
description: "这是Fooleap的个人博客，记录学习生活的点点滴滴。"
---
{% include JB/setup %}

<div id="board">
  <ul id="posts">
    {% for post in site.posts limit:1 %}
    <li><span class="date">{{ post.date | date_to_string }}</span><span class="title"><a href="{{ post.url }}" title="{{ post.title }}" rel="bookmark">{{ post.title }}</a></span></li>
    <li><span class="date"> </span><span class="title">{{ post.description}}</span></li>
    {% endfor %}
    {% for post in site.posts limit:9 offset:1  %}
    <li><span class="date">{{ post.date | date_to_string }}</span><span class="title"><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></span></li>
    {% endfor %}
    <li><span class="date"> </span><span class="title"><a href="http://blog.fooleap.org/archive.html">更多……</a></span></li>
  </ul>
</div>
