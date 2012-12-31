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

<a href="http://www.scanv.com" id="scanv_verify_link">互联网安全</a><script src="http://static.scanv.com/static/js/scanv_verify.js" scanv_id="50e1cd14ca8e0b6e2304831e" charset="utf-8" type="text/javascript"></script>

