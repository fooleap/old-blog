---
date: '2012-02-17 17:03:53'
layout: post
slug: hard-disk-installation-for-archlinux
status: publish
title: 硬盘安装Archlinux 2011.08
wordpress_id: '932'
categories:
- linux
post_format:
- 标准
tags:
- ArchLinux
- grub4dos
- 硬盘安装
---

﻿Archlinux新日期的CD镜像2011.08.19[发布](http://www.archlinux.org/news/20110819-installation-media/)到现在已经一个月了，Archlinux是滚动更新，系统同步到最新只需一条命令，新CD镜像发布时间没有规律，使用Archlinux的Linuxer一般都没留意到关注新CD的发布，发布后过了好些天才知道。此前用2010.05的镜像硬盘安装了几次皆失败，既然新版本出来了，想尝下鲜，加上Win7在小本上显驱安装的失败，让我更坚定了，xp+arch才是我x30的最佳拍档，xp用于看半高清，满足课程需要；arch则用于除上面两项外的日常使用。
﻿新版本安装镜像与此前版本还是有差异的，编辑配置文件的文本编辑器有vi可选，对于用习惯vi的童鞋来说还是方便了不少。
﻿archlinux官方文档有[关于硬盘安装的文章](https://wiki.archlinux.org/index.php/Hard_Disk_Installation_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))，而最近网上出现的archlinux硬盘安装的文章也层出不穷，如[ArchLinux 2011.8 基于grub的硬盘安装简易指南](http://flanker017.sinaapp.com/?p=102)，这是使用grub2引导的文章。在Windows下，设置好grub4dos，做好引导，一路跟着官方文档，安装个archlinux还是很简单的。2011.08版硬盘安装和此前版本相似，当然[Archlang引导硬盘安装](http://fooleap.org/linux-study-4.html)与之亦相似，安装过程中的cfdisk分区工具还是令我头疼，所以提前分好区。

**引导进入Live环境**
﻿首先，在已存在的Windows里设置使用grub for dos，引导启动安装程序，下载[grub4dos](http://sourceforge.net/projects/grub4dos/),提取grldr(Vista/7上还需要grldr.mbr)，及menu.lst置于系统分区根目录下，并编辑boot.ini文件，添加

    c:\grldr="Grub4Dos"

Vista/7系统上则新建boot.ini文件

    C:\boot.ini
    [boot loader]
    [operating systems]
    c:\grldr.mbr="Grub4Dos"


提取archlinux-2011.08.19-core-i686.iso中/arch/boot/i686目录下的vmlinuz和archiso.img以及archlinux-2011.08.19-core-i686.iso本身置于系统分区根目录，并在menu.lst中添加（假设Windows的系统分区位于第一块硬盘的第一个分区）

    C:\menu.lst
    title  Install Arch Linux
    root   (hd0,0)
    kernel /vmlinuz archisolabel=archiso
    initrd /archiso.img

重启选择进入后，根据官方wiki

>
注意这里增加了参数archisolabel=archiso，archisolabel参数用于指定在引导安装环境时所选安装源的标签（label）
若是用2011.08的ISO，在启动过程中会查找/dev/disk/by-label/archiso文件，如果找不到（因为使用的硬盘ISO方式），会得到一个shell，通过这个shell可以手动使用losetup将ISO挂到某个loop设备上，最后将这个loop设备ln到/dev/disk/by-label/archiso。
注意这里的archiso即grub引导时内核参数archisolabel的值，如果在grub引导内核时未指定参数，那么这里将无法读取到光盘镜像。

>
>     #mkdir /win
>     #mkdir -p /dev/disk/by-label
>     #mount -r -t ntfs /dev/sda1 /win
>     #modprobe loop
>     #losetup /dev/loop6 /win/archlinux-2011.08.19-core-i686.iso
>     #ln -s /dev/loop6 /dev/disk/by-label/archiso
>     #exit
>
>

注意：这句#mount -r -t ntfs /dev/sda1 /win中的ntfs,如果你用到的分区是fat32格式，请将其改为vfat。
使用exit退出shell，就可以进入安装环境。

**安装基本系统**
接下来的安装就和光盘安装一样了，输入以下命令进行安装：

    # /arch/setup

可根据[官方安装指南](https://wiki.archlinux.org/index.php/Official_Installation_Guide_(简体中文))、[新手指南](https://wiki.archlinux.org/index.php/Beginners%27_Guide_%28%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87%29)或[快速安装](https://wiki.archlinux.org/index.php/Quick_Arch_Linux_Install)进行安装。
我是在安装之前就把分区分好，安装的时候直接用提供的工具选择格式及挂载点就可以了。在选择包的时候，很多包不知道干嘛用的，按默认的选择，只添加sudo这个包，更改配置那一步也就配置了root密码，其他的先不进行修改。
安装时，最后安装grub的时候居然出错了，记下启动archlinux的命令，即查看/boot/grub/menu.lst这个文件或者直接复制下来，然后在win下对grub4dos的menu.lst进行修改或直接使用grub提供的命令行。

**添加用户**
安装完成进入base系统之后，首先添加用户，可用adduser命令，根据向导完成创建用户，即

    # adduser fooleap

提供可使用sudo的权限，可用visudo，也可直接修改/etc/sudoers这个文件。

    /etc/sudoers
    # 添加如下
    fooleap ALL=(ALL) NOPASSWD:ALL

这是我自己的配置，懒得输密码，所以加上了NOPASSWD:
还可将用户添加到wheel组，设置wheel组权限。
可参考官方Wiki：https://wiki.archlinux.org/index.php/Sudo

**配置网络**
基本系统安装后，先配置下网络，若使用有线路由，插上网线直接

    # dhcpcd

若使用PPPoE或者无线等，可参考官方Wiki：
https://wiki.archlinux.org/index.php/Configuring_Network
https://wiki.archlinux.org/index.php/Wireless_Setup
联网后，添加源后更新一下，即


    /etc/pacman.conf
    [archlinuxfr]
    Server = http://repo.archlinux.fr/x86_64
    # 使用这个源后即可安装yaourt，后面提到的awesome也在其中，32位的把x86_64改为i686

    /etc/pacman.d/mirrorlist
    ## China 取消国内源的井号
    Server = http://mirrors.163.com/archlinux/$repo/os/$arch
    Server = http://mirror.bjtu.edu.cn/archlinux/$repo/os/$arch
    Server = http://mirror6.bjtu.edu.cn/archlinux/$repo/os/$arch
    Server = ftp://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch
    Server = http://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch


    # pacman -Syu

以前基本上使用NetworkManager管理网络，最近一直通过无线路由上网，使用WPA个人版加密，发现通过Netcfg联网也是个不错的选择。

    # pacman -S netcfg

    # cp /etc/network.d/examples/wireless-wpa /etc/network.d/fooleap
    /etc/network.d/fooleap
    # 如下一般修改ESSID及KEY即可
    CONNECTION='wireless'
    DESCRIPTION='A simple WPA encrypted wireless connection'
    INTERFACE='wlan0'
    SECURITY='wpa'
    ESSID='Fooleap'
    KEY='fooleapchen'
    IP='dhcp'
    # Uncomment this if your ssid is hidden
    # HIDDEN=yes



可使用netcfg2命令连接网络


    netcfg2 fooleap


也可加载到系统自启的[守护进程](https://wiki.archlinux.org/index.php/Daemon)


    /etc/rc.conf
    NETWORKS=(fooleap)
    DAEMONS=(...!network...net-profiles)
    # 即把连接名添加至NETWORKS里，添加net-profiles作为服务并停用network。



可参考官方Wiki：https://wiki.archlinux.org/index.php/Netcfg

**配置Alsa**


    # pacman -S alsa-utils


使用alsaconf自动配置


    # alsaconf


若无法识别声卡，以我本子为例，可进行如下操作后再进行alsaconf


    $ lspci -nn | grep Audio
    00:1b.0 Audio device [0403]: Intel Corporation 5 Series/3400 Series Chipset High Definition Audio [8086:3b56] (rev 06)
    /var/tmp/alsaconf.cards
    # 照葫芦画瓢补上，若为空白就添加如下
    snd-hda-intel.o
    PCI: 0x8086=0x3b56

把用户添加到audio组

    # gpasswd -a fooleap audio

可参考官方Wiki：https://wiki.archlinux.org/index.php/Alsa
终端的滴滴声很讨厌，取消掉，vim配置也跟上

    # echo "set bell-style none">>/etc/inputrc
    $ echo "set vb">>~/.vimrc

可参考官方Wiki：https://wiki.archlinux.org/index.php/Disable_PC_Speaker_Beep

**安装图形界面**
在安装X的时候，根据官方新手指南之[图形用户界面](https://wiki.archlinux.org/index.php/Beginners%27_Guide_%28%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87%29#.E5.9B.BE.E5.BD.A2.E7.94.A8.E6.88.B7.E7.95.8C.E9.9D.A2)进行安装

    # pacman -S xorg-server xorg-xinit xorg-utils xorg-server-utils

安装完后startx出现如下错误，缺少哪个模块就补上那个


> Failed to load module "intel" (module does not exist,0)
Failed to load module "vesa" (module does not exist,0)
Failed to load module "fbdev" (module does not exist,0)

    # pacman -S xf86-video-intel xf86-video-vesa xf86-video-fbdev


把用户添加到video组


    # gpasswd -a fooleap video


可参考官方Wiki：https://wiki.archlinux.org/index.php/Xorg
安装D-Bus


    # pacman -S dbus


添加到守护进程


    /etc/rc.conf
    DAEMONS=(... dbus ...)


可参考官方Wiki：https://wiki.archlinux.org/index.php/Dbus
鄙人已习惯于awesome，强大的Mod键，Mod+Shift+c按得爽，安装awesome


    # pacman -S awesome


往~/.xinitrc添加exec awesome后，执行startx，即可启动awesome。
可参考官方Wiki：https://wiki.archlinux.org/index.php/Awesome
你可能需要登录管理器，那么可能需要ConsoleKit


    # pacman -S consolekit


可参考官方Wiki：https://wiki.archlinux.org/index.php/ConsoleKit
如果你和我一样也讨厌摸板，那我们一起把它关了吧！
安装驱动


    # pacman -S xf86-input-synaptics


修改配置，也可以添加启动项synclient TouchpadOff=1


    /etc/X11/xorg.conf.d/10-synaptics.conf
    Section "InputClass"
            Identifier "touchpad catchall"
            Driver "synaptics"
            MatchIsTouchpad "on"
            MatchDevicePath "/dev/input/event*"
            Option "TapButton1" "1"
            Option "TapButton2" "2"
            Option "TapButton3" "3"
            Option "TouchpadOff" "1"
    EndSection
    # 添加 Option "TouchpadOff" "1"



可参考官方Wiki：https://wiki.archlinux.org/index.php/Touchpad_Synaptics
安装输入法

    # pacman -S fcitx

    ~/.xinitrc
    export XMODIFIERS="@im=fcitx"
    export QT_IM_MODULE=xim
    export GTK_IM_MODULE=xim
    fcitx&

可参考官方Wiki：https://wiki.archlinux.org/index.php/Fcitx
如果你和我一样，使用yong输入法，可通过yaourt安装，添加到.xinitrc文件为如下

    ~/.xinitrc
    export XMODIFIERS="@im=yong"
    export QT_IM_MODULE=xim
    export GTK_IM_MODULE=xim
    yong -d&

    使用过程中可能还会碰到权限问题，可参考官方Wiki：https://wiki.archlinux.org/index.php/Users_and_Groups
    此后要安装软件一般通过pacman和yaourt即可，aur更新极快，所以日常使用一般都不需要手动编译。
    本文较不完善，很多常见的问题都没提到，安装arch的过程可能是新手所畏惧的，官方文档较完善，很多问题在那都能找到答案，只要连上了网，一切问题都不是问题，因为我们还有Google！
    待续。。。
**本文历史**
2011年09月25日  创建文章
2011年11月14日  添加修改配置以识别声卡及取消滴滴声
2012年02月17日  重新整理
