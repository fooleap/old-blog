---
date: '2011-05-14 11:30:16'
layout: post
slug: linux-study-4
status: publish
title: Linux学习笔记(4) - 硬盘安装Archbang
wordpress_id: '465'
categories:
- linux
tags:
- Archbang
- ArchLinux
- linux
- locale
- networkmanager
- 小小输入法
- 硬盘安装
- 笔记
---

一直以来都对ArchLinux十分向往，而ArchLinux硬盘安装是十分折腾的，此次安装栽在安装源的设置，宿舍网络情况并不好，把iso文件挂载在/src目录下，不行，也还没找到相关信息。这我想起了Archboot，而无意中却碰到了Archbang([主页](http://archbang.org))这个图形界面的live CD，和ubuntu等发行版一样，live环境都提供了安装在硬盘的快捷方式。一切只需点击Install，这给我这等菜鸟带来多大的方便啊！

Archbang的引导和ArchLinux一样：

在Windows下，提取镜像/arch/boot/i686路径的vmlinuz26和archbang.img(ArchLinux则是/boot/的vmlinuz26和archlinux.img)到c盘根目录，并把iso文件也放c盘根目录。

在grub for dos的配置文件menu.lst里添加一项

    title Install Archbang
    root   (hd0,0)
    kernel /VMLINUZ26 archisolabel=archiso
    initrd /ARCHBANG.IMG


进入引导进入后会自动检测/dev/disk/by-label/archiso，用所提供的shell：

    # mkdir /tmp_mnt
    # mount –r –t vfat /dev/sda1 /tmp_mnt
    # modprobe loop
    # losetup /dev/loop6 /tmp_mnt/ArchBang-2011.02.04-i686.iso
    # ln –s /dev/loop6 /dev/disk/by-label/archiso
    # exit

这下检测就有了，不管是在grub的命令行，还是bash，多按tab都会有好处的。对于iso文件名更是方便，不可能忘了之后去查看文件名再回来输入吧？

进入live CD环境后，右键安装

安装过程和ArchLinux差不多，而安装完的系统环境就不是一个基本的系统，而是有着图形界面的环境，SLiM+openbox+tint2+Conky的界面(如图)让鄙人倍感亲切。

[![](http://i951.photobucket.com/albums/ad353/Fooleap/Blog/Fooleap/2011-05-08--1304866398_1024x768_scrot.png)](http://i951.photobucket.com/albums/ad353/Fooleap/Blog/Fooleap/2011-05-08--1304866398_1024x768_scrot.png)

安装后的各种配置

资源占用很低，这完全符合Arch哲学极简之道。安装完中文字体和输入法之后，用起来就十分舒服了。Linux各发行版的不同，最直接的是软件包管理，debian系是deb，redhat系则是rpm，Archlinux则是pacman。pacman用着特舒服，安装软件只需pacman -S *，如果没有则可yaourt -S *，当然在此之前必须确认yaourt的安装。一般的常用软件pacman都有，而像国内的youmoney,yong这些，就需要aur。在ArchLinux下，意料之外的是，yong输入法居然不用手动安装，当然如果手动安装会比较麻烦，不是轻易就可完成。

在英文locale下,小小输入法的安装①

这方面对我来说有点复杂,我的locale.gen文件是这样的:

    en_US.UTF-8 UTF-8
    zh_CN.UTF-8 UTF-8
    zh_CN.GBK GBK

通过aur安装yong输入法

    # yaourt -S yong

修改/etc/gtk-2.0/gtk.immodules

找到"xim" "X Input Method" "gtk20" "/usr/share/locale" "ko:ja:th:zh"

在local添加en,即为:

    "xim" "X Input Method" "gtk20" "/usr/share/locale" "en:ko:ja:th:zh"

添加环境变量,鄙人添加到~/.profile文件，当然~/.xinitrc等也可以。

    export LC_CTYPE='zh_CN.utf8'
    export XMODIFIERS="@im=yong"
    export GTK_IM_MODULE="xim"
    export QT_IM_MODULE="xim"

自启动只需将"yong -d &"添加到openbox的autostart.sh即可

安装grub2

    # pacman -S grub2

自动生成配置文件

    # grub-mkconfig -o /boot/grub/grub.cfg

将grub安装到主引导记录中

    # grub-install /dev/sda

Gtk+主题的配置可以使用lxappearance来调整，可直接

    # pacman -S lxappearance

联网

ADSL连接使用pppoe-setup,pppoe-start，相对来说比起ubuntu等发行版的pppoeconf麻烦了点，不过也就手动设置了DNS服务器。

也可以使用熟悉的nm-applet，官方中文wiki关于NetworkManager的说明已不适用，gnome-network-manager已不在。可参考[英文ArchWiki](https://wiki.archlinux.org/index.php/NetworkManager)：

    # pacman -S networkmanager network-manager-applet

切记安装后修改/etc/rc.conf文件,如下

在DAEMONS这个值中的networkmanager前加@,即@networkmanager,否则nm-applet将无法启动

在添加DSL连接的时候，要撤选左下角“对所有用户可用”，要不会提示权限不足。

用NetworkManager管理连接vpn pptp②，在添加vpn连接时，在高级里勾选Point To Point，在arch用vpn的时候，连接后不用重启浏览器就能浏览网页，而ubuntu却要，这是什么原因？还是此前用lubuntu的时候的配置问题？

    # pacman -S networkmanager-pptp pptpclient

昨天在淘宝上买了本杂志,支付宝控件安装后firefox却没识别到,于是Google下

> 支付宝 控件依赖于libpng12.so.0 最新的archlinux软件包升级到了linpng14，这对依赖libpng12库的部分应用程式来讲，可能会出现linpng12.so.0无法截入的问题。 解决方法也很简单，作一个库文件的软连接即可，如下： ln -s /usr/lib/libpng14.so /usr/lib/libpng12.so.0

ArchLinux在我的小本上发挥极致，更重要的是ArchLinux有着完善的wiki，ArchLinux Wiki太强大了。软件使用有什么不懂，可直接往左侧搜索框直接搜索软件名。

2011年5月13日

下午再进入archlinux原盘的live环境,原来archlinux原盘的live也有pppoe拨号,可以直接通过pppoe-setup,pppoe-start来连接网络后,通过网络安装系统,这下子archlinux的安装搞明白了,退出后看了下arch wiki也确实记录了这一安装方式,多拜读wiki才是对的!不过也确实很想弄明白archlinux的硬盘安装方法,安装源到底挂载在哪呢?

**相关资料**

1. [硬盘安装archbang！](http://bbs.wuyou.com/viewthread.php?tid=191789)
2. [ArchLinux Wiki](https://wiki.archlinux.org/index.php/Main_Page)

**注**

1. 这个方法可能有些步骤是多余的,不过鄙人经过这样的配置之后输入法正常使用,所以也不想再折腾
<del>2. 免费vpn可参考[新民智工作室](http://samozi.com/)文章：[郭嘉的故事](http://samozi.com/internet/tenacy-vpn-free-service.html)</del>

**本文历史**

* 2011年05月09日  创建文章
* 2011年05月11日  添加NetworkManager部分
* 2011年05月12日  添加支付宝控件部分
* 2011年05月13日  添加grub2部分
* 2011年05月14日  添加yong输入法部分
