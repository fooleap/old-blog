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
       <span id="title"><a href="{{ BASE_PATH }}{{ post.url }}" title="{{ post.description }}">{{ post.title }}</a></span>
       <span id="comment"><a href="{{ post.url }}#disqus_thread">Link</a></span>
       <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time> 
      </li>
    {% endfor %}
    <h4>生活</h4>
    {% for post in site.categories.life limit:5 %}
      <li>
        <a href="{{ BASE_PATH }}{{ post.url }}" title="{{ post.description }}" altbg="red" altcolor="yellow" altborder="yellow">{{ post.title }}</a>
        <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
      </li>
    {% endfor %}
    <li><a href="/categories.html" title="分类">更多……</a></li>
  </ul>
  <div class="sidebar">
    <h4>友情链接</h4>
    {% include JB/blogroll %}
  </div>
</div>
</div>
<script type="text/javascript">
/* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
var disqus_shortname = 'fooleap1'; // required: replace example with your forum shortname

/* * * DON'T EDIT BELOW THIS LINE * * */
(function () {
    var s = document.createElement('script'); s.async = true;
    s.type = 'text/javascript';
    s.src = 'http://' + disqus_shortname + '.disqus.com/count.js';
    (document.getElementsByTagName('HEAD')[0] || document.getElementsByTagName('BODY')[0]).appendChild(s);
}());
</script>
