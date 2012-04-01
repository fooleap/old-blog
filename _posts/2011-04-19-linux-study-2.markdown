---
date: '2011-04-19 08:14:08'
layout: post
slug: linux-study-2
status: publish
wordpress_id: '384'
title: Linux学习笔记(2)
categories:
- linux
tags:
- linux
- pidgin
- 初学
- 学习
- 小小输入法
- 小鹤
- 笔记
- 超级玛莉
---

用了十天左右的Fedora14-lxde，感觉比Ubuntu要更加舒服，只不过它在我这小机子上表现不是很好。某天不觉进了一下xp，感觉它比Fedora14要轻巧得多，于是又想起了debian。装了下debian，debian自带的东西很少，要装的很多，没想到配置好了一半重启进入图形界面的时候花屏了，我在想，这机子如果要正常使用linux的话，不想麻烦应该还是lubuntu比较适合，于是乎，又装了个lubuntu。确实，比Fedora轻巧了好多，不过Fedora的使用还是挺有帮助的，现在已经可以感觉到码命令的速度越来越快了，起码比前段时间使用lubuntu快。

下面把自己装lubuntu之后所安装配置的软件等大致说一遍。

**神器在手，天下任我走**

自带vi，还没有vim，于是

    sudo apt-get install vim

中文乱码解决：

    vim ~/.vimrc

`set encoding=utf-8 set termencoding=utf-8 set fencs=ucs-bom,utf-8,gb18030,gbk,gb2312,big5,euc-jp,euc-kr,latin1,cp936`

 源于http://www.nonozone.net/solve-vim-chinese-garbled.html

 关于神器的配置，更多请Google

**输入法，作为一个中国人，必须的**

由于安装使用英文，所以先在Preferences-Language Support添加语言Chinese(simplified)

然后安装输入法，我使用的是小小输入法(http://yong.uueasy.com)，并挂载小鹤双拼配置

下载后发现是7z压缩包，于是

    sudo apt-get install p7zip-full

解压

    7za e * yong

解压后把文件夹复制到/opt目录

    sudo cp -r yong /opt

进入目录

    cd /opt/yong

安装

    sudo ./yong-tool.sh --install      //安装需要root权限

设置默认

    ./yong-tool.sh --select            //平时使用还是普通权限

配置小鹤双拼，这里只配置音码部分
 .yong目录如果没有mb文件夹

    sudo cp -r /opt/yong/mb home/yourname/.yong

记得第一次安装的时候我是在这一步出错的，因为使用的是root管理员账户，复制后文件夹属于root的，我们登录的用户无权访问此文件夹的配置文件，所以输入法会出错。可以使用chown命令来修改此文件夹的主人：

    sudo chown -R fooleap:fooleap /home/fooleap/.yong/mb

亦可以复制先前解压的得到的mb文件夹而不使用已复制到/opt目录下的文件夹。

在~/.yong下创建文件xiaohe.sp，内容可参考[这里](http://yong.uueasy.com/read-htm-tid-1475.html)

    vim ~/.yong/yong.ini

`...... [IM] default=8 0=yong 1=wubi 2=zhengma 3=erbi 4=english 5=gbk 6=pinyin 7=wbpy 8=xiaohe ....... [xiaohe] name=小鹤 engine=libmb.so arg=mb/pinyin.txt overlay=mb/sp.ini sp=xiaohe`

如果overlay=mb/pinyin.ini而不是sp.ini的话，必须修改pinyin.ini，屏蔽掉u,v快捷键，即在其前加”!”就可以了。
 配置完毕注销即可，即重启进程生效。

**安装LibreOffice**
 此前先安装java，下载[Linux
（自解压文件）](http://javadl.sun.com/webapps/download/AutoDL?BundleId=47143)，[安装说明](http://www.java.com/zh_CN/download/help/linux_install.xml#selfextracting)

然后在[LibreOffice官网](http://www.libreoffice.org/)下载相关的安装包，语言包，sudo
dpkg -i .deb 进行安装

**安装pidgin插件**

使其支持QQ，飞信，新浪微博，对应的插件为[libqq](http://code.google.com/p/libqq-pidgin/).[libopenfetion](http://code.google.com/p/ofetion/).[libtsina](http://code.google.com/p/libpurple-microblog-sina/)，还有发送图片的插件[Send
Srceenshot](http://code.google.com/p/pidgin-sendscreenshot/)，显示视频图片的插件Pidgin
Embedded Video

提供libqq，openfetion，tsina的so文件[下载点我](http://dl.dbank.com/c0oxhxdivc)
 复制至/usr/lib/purple-2或~/.purple/plugins即可，没有文件夹请新建

**使用下载工具**
 现在一般的下载我用Firefox自带的下载
 自用的Firefox有两个插件，一个是Pentadactyl，用上就离不开了，一个是ABP
 还有axel备用，BT用rtorrent，benliud，相对来说benliud的下载速度快且稳定

附上benliud的deb包（[下载](http://dl.dbank.com/c0167dei9g)），中文语言文件不全，有些地方显示fail，可往/usr/local/share/benliud/language删除语言文件以回归英文界面

**在英文环境下要配置gimp显示中文，则可运行**

  LANGUAGE=zh\_CN.utf8 gimp\
 
可新建个Shell脚本，扩展名为sh，内容为

 `#/bin/bash LANGUAGE=zh_CN.utf8 gimp`

并往/usr/share/applications修改菜单的快捷方式指向它就可以了，类似的软件亦可通过此方法解决

**影音我用mplayer**

 没什么追求，能放即可
 有时候想家也可

    mplayer mms://chdt.hepan.net.cn/chdt

个人配置文件为~/.mplayer/config

**关于游戏**

有时候放松一下也没什么不可，于是

    sudo apt-get install gfceu

再下个SuperMario.nes（[下载](http://dl.dbank.com/c0ubzkgcib)）

[![SuperMario](http://i951.photobucket.com/albums/ad353/Fooleap/Blog/Fooleap/supermario.png)](http://i951.photobucket.com/albums/ad353/Fooleap/Blog/Fooleap/supermario.png "SuperMario")

啊哈，小霸王其乐无穷啊~

嘘，“小霸王”可是敏感词=。=

作为一个新手，让我感觉最深刻的还是chown和chmod这两个命令，没有了权限，什么都是扯淡。

就先说到这里吧，相信大多数新手都和鄙人一样，学习Linux的也是其乐无穷的~

**解决问题三步走**

 1.根据提示自己解决
 2.Google
 3.论坛发帖求助

 一般问题到第二步的时候已经解决了

**本文历史**

*  2011年04月19日 创建文章

