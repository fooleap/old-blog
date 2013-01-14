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
    <li><span class="date">{{ post.date | date_to_string }}</span><span class="title"><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></span></li>
    {% endfor %}
    <h4>Life</h4>
    {% for post in site.categories.life limit:5 %}
    <li><span class="date">{{ post.date | date_to_string }}</span><span class="title"><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></span></li>
    {% endfor %}
    <li><span class="date"> </span><span class="title"><a href="/categories.html">更多……</a></span></li>
  </ul>
   <div class="sidebar">
    <h4>Blogroll</h4>
      <ul>
        <li><a href="http://jianyin.org" title="老A">Ageda&#039;s Blog</a></li>
        <li><a href="http://blog.conan06.com/" title="Conan06@北京">Conan06&#039;s blog</a></li>
        <li><a href="http://www.it8421.com/" title="小Q@马鞍山">it8421</a></li>
        <li><a href="http://songtl.com/" title="宋廷龙@桂林">Song's Blog</a></li>
        <li><a href="http://www.tealun.com/" title="Tealun Du@桂林">Tealun Du</a></li>
        <li><a href="http://terrychen.info/" title="陈敏@北京">Terry&#039;s Blog</a></li>
        <li><a href="http://www.ubuntusoft.com/" title="灵亦rEd@肇庆">UbuntuSoft</a></li>
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
</div>
</div>
