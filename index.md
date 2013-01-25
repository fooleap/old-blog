---
layout: default
description: "Fooleap 的个人博客，记录学习工作生活的点点滴滴，话题方向在于 Linux，跑步，旅行。"
tags: [Linux, Arch Linux, 慢跑, 徒步, 骑行]
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
<div id="post-pagination" class="pagination">
  <p class="previous disabled">
    <span>Previous</span>
  </p>
  <ul class="pages">
    <li class="page">
      <a href="/">1</a>
    </li>
  </ul>
  <p class="next disabled">
    <span>Next</span>
  </p>
</div>
  <div class="sidebar">
    <h4>Blogroll</h4>
    {% include JB/blogroll %}
  </div>
</div>
</div>
