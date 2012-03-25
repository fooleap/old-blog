---
layout: default
description: "这是Fooleap的个人博客，记录学习生活的点点滴滴。"
---
{% include JB/setup %}

**最近的10篇日志**

  {% for npost in site.posts limit:1 %}
  <ul><li>{{ npost.date | date_to_string }} &raquo; <a href="{{ npost.url }}" title="{{ npost.title }}" rel="bookmark">{{ npost.title }}</a></li>

  <div class="home1">  {{ npost.description}}
  <a href="{{ npost.url }}" title="Read More" rel="nofollow">(More...)</a></div></ul>
  {% endfor %}
  {% for post in site.posts limit:9 offset:1  %}
* {{ post.date | date_to_string }} &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
  {% endfor %}

<hr>
**友情链接**

<div class="blogroll">
<ul>
<li><a href="http://jianyin.org" title="老A">Ageda&#039;s Blog</a></li>
<li><a href="http://www.archlinux.org" title="A simple, lightweight distribution">Arch Linux</a></li>
<li><a href="http://blog.conan06.com/" title="Conan06@北京">Conan06&#039;s blog</a></li>
<li><a href="http://www.it8421.com/" title="小Q@马鞍山">it8421</a></li>
<li><a href="http://terrychen.info/" title="陈敏@北京">Terry&#039;s Blog</a></li>
<li><a href="http://www.ubuntusoft.com/" title="灵亦rEd@肇庆">UbuntuSoft</a></li>
<li><a href="http://xunjian.net" title="陈训坚@桂林">Xunjian.net</a></li>
<li><a href="http://since1989.org/" title="王亚平@上海">上海周末</a></li>
<li><a href="http://bzdiao.com/" title="Bruse@西安">不着调软件</a></li>
<li><a href="http://lhcy.info" title=" 林海草原@锦州">以梦为马，奔向远方</a></li>
<li><a href="http://gubo.org" title="许凯@焦作">古博</a></li>
<li><a href="http://www.nenew.net/" title="奶牛@淄博">奶牛博客</a></li>
<li><a href="http://www.zhanggang.net/" title="张刚@长沙">张刚的博客</a></li>
<li><a href="http://betabone.com" title="betabone@杭州">排骨日记</a></li>
<li><a href="http://www.chenstory.com/" title="陈荣强@桂林">枯木博客</a></li>
<li><a href="http://www.makiller.com" title="马震南@桂林">贼头&#039;s Blog</a></li>
</ul>
</div>

