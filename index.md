---
layout: default
description: "A foolish man could not always lose!"
---
{% include JB/setup %}

<div id="board">
<div class="row">
  <ul id="posts">
      <h4>Tech</h4>
      {% for post in site.categories.tech limit:5 %}
      <li><span class="title"><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></span><span class="date">{{ post.date | date:"%Y-%m-%d" }}</span></li>
      {% endfor %}
      <h4>Life</h4>
      {% for post in site.categories.life limit:5 %}
      <li><span class="title"><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></span><span class="date">{{ post.date | date:"%Y-%m-%d" }}</span></li>
      {% endfor %}
      <li><span class="title"><a href="/categories.html">更多……</a></span></li>
  </ul>
  <div class="sidebar">
    <h4>Blogroll</h4>
    {% include JB/blogroll %}
  </div>
</div>
</div>
