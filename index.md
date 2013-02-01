---
layout: default
tagline: "你若安好，便是晴天"
description: "Fooleap 的个人博客，记录学习工作生活的点点滴滴，话题方向在于 Linux，跑步，旅行。"
tags: [Linux, Arch Linux, 慢跑, 徒步, 骑行]
---
{% include JB/setup %}

<div class="page-header">
  <h1>{{ page.tagline }}</h1>
</div>

<div class="row">
<div id="posts">
  <ul>
    {% for post in site.posts limit:1 %}
      <li>
        <div id="first">
          <a href="{{ BASE_PATH }}{{ post.url }}" title="{{ post.title }}" >{{ post.title }}</a>
          <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
        </div>
        <div id="description"><span id="img"><img src="{{ post.image }}" /></span><a class="btn btn-large disabled" id="more" href="{{ post.url }}">阅读全文</a><p>{{ post.description}}</p></div>
      </li>
    {% endfor %}
    {% for post in site.posts limit:9 offset:1 %} 
    <li>
      <a href="{{ BASE_PATH }}{{ post.url }}" title="{{ post.description }}" >{{ post.title }}</a>
      <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
    </li>
    {% endfor %}
  </ul>
  <p id="remind">更多文章请查看 <a href="archive.html">存档</a> 或 <a href="categories.html">分类</a></p>
</div>
  <div class="span4 sidebar">
    <h4>友情链接</h4>
    {% include JB/blogroll %}
  </div>
</div>
