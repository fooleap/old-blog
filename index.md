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
      <li>
        <a href="{{ BASE_PATH }}{{ post.url }}" title="{{ post.description }}">{{ post.title }}</a>
        <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
      </li>
    {% endfor %}
    <h4>Life</h4>
    {% for post in site.categories.life limit:5 %}
      <li>
        <a href="{{ BASE_PATH }}{{ post.url }}" title="{{ post.description }}" altbg="red" altcolor="yellow" altborder="yellow">{{ post.title }}</a>
        <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
      </li>
    {% endfor %}
    <li><a href="/categories.html" title="分类">更多……</a></li>
  </ul>
  <div class="sidebar">
    <h4>Blogroll</h4>
    {% include JB/blogroll %}
  </div>
</div>
</div>
