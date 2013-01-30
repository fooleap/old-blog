---
layout: default
description: "Fooleap 的个人博客，记录学习工作生活的点点滴滴，话题方向在于 Linux，跑步，旅行。"
tags: [Linux, Arch Linux, 慢跑, 徒步, 骑行]
---
{% include JB/setup %}

<div id="board">
<div class="row">
  <ul id="posts">
    <h4>技术</h4>
    {% for post in site.categories.tech limit:5 %}
      <li>
      <a href="{{ BASE_PATH }}{{ post.url }}" title="{{ post.description }}">{{ post.title }}</a>
       <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
      </li>
    {% endfor %}
    <h4>生活</h4>
    {% for post in site.categories.life limit:5 %}
      <li>
        <a href="{{ BASE_PATH }}{{ post.url }}" title="{{ post.description }}" >{{ post.title }}</a>
        <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
      </li>
    {% endfor %}
  </ul>
  <div class="sidebar">
    <h4>友情链接</h4>
    {% include JB/blogroll %}
  </div>
</div>
</div>
