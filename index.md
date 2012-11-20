---
layout: default
description: "A foolish man could not always lose!"
---
{% include JB/setup %}

<div id="board">
  <ul id="posts">
    {% for post in site.posts limit:1 %}
    <li><span class="date">{{ post.date | date_to_string }}</span><span class="title"><a href="{{ post.url }}" title="{{ post.title }}" rel="bookmark">{{ post.title }}</a></span></li>
    <li><span class="date"> </span><span class="title">{{ post.description}}</span></li>
    {% endfor %}
    {% for post in site.posts limit:11 offset:1  %}
    <li><span class="date">{{ post.date | date_to_string }}</span><span class="title"><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></span></li>
    {% endfor %}
    <li><span class="date"> </span><span class="title"><a href="/archive.html">更多……</a></span></li>
  </ul>
</div>

