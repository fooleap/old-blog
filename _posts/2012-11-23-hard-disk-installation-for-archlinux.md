---
layout: post
title: "硬盘安装 Arch Linux"
description: "Chakra 虽稳定，KDE 臃肿，纯 QT 的环境用得别扭，没有 Arch Linux 的自由，于是切换回 Arch Linux，新版本的安装方式和以前稍有区别，下面一步一步来完成 Arch Linux 的安装。"
category: linux
tags: [Arch Linux, 硬盘安装]
---
{% include JB/setup %}
Chakra 虽稳定，KDE 臃肿，纯 QT 的环境用得别扭，没有 Arch Linux 的自由，于是切换回 Arch Linux，新版本的安装方式和以前稍有区别，下面一步一步来完成 Arch Linux 的安装。

此前使用 Chakra Linux，其启动引导器为 [BURG](https://wiki.archlinux.org/index.php/Burg)，它是基于 [GRUB2](https://wiki.archlinux.org/index.php/GRUB2) 使用 Ruby 重写而来的，所以 [GRUB 命令](http://www.gnu.org/software/grub/manual/grub.html#Commands)同样适用。

把下载而来的 [archlinux-2012.11.01-dual.iso](http://mirrors.163.com/archlinux/iso/2012.11.01/archlinux-2012.11.01-dual.iso) 复制到U盘的根目录，重启机器。

进入 BURG 引导界面，按 C 进入命令行模式。

    loopback loop (hd1,msdos1)/archlinux-2012.11.01-dual.iso
    linux (loop)/arch/boot/x86_64/vmlinuz archisolabel=ARCH2012_11
    initrd (loop)/arch/boot/x86_64/archiso.img
    boot

* loopback 把镜像挂载为 loop 设备，在此将其 iso 挂为 loop (可自定义)
* linux 指定内核，具体见 [vmlinux](http://zh.wikipedia.org/zh-cn/Vmlinux)
* initrd 指定临时文件系统，具体见 [initrd](http://zh.wikipedia.org/zh-cn/initrd)
* boot 启动

启动过程提示找不到，得到一个 Shell，进行下面的操作

    # mkdir/udisk
    # mount -r -t vfat /dev/sdb1 /udisk
    # modprobe loop
    # losetup /dev/loop6 /udisk/archlinux-2012.11.01-dual.iso
    # ln -s /dev/loop6 /dev/disk/by-label/ARCH2012_11
    # exit

* 创建 /udisk 目录
* 把 U 盘挂载到 /udisk 目录
* 载入 loop 模块
* 把 ISO 映射为 loop 设备
* 把 /dev/disk/by-label/ARCH2012\_11 软链接到刚创建的 loop 设备
* 退出 Shell

一切没有问题将会自动以 root 登录，目前 Arch Linux 的安装方式和 Gentoo 差不多，都通过 Change Root。

*配置网络*

我使用的是无线路由，比较方便，通过自带的 Netcfg 连接网络。

    # wifi-menu wlan0

搜索 Wifi 热点，并进行认证连接

*硬盘分区*

鄙人认为，个人计算机硬盘分区个数越少越好，最好只有一个，这也是微软和苹果所提倡的。

由于还有换系统的可能，除了根目录，我把 /home 独立出来成为一个分区，内存够用，就没考虑到 Swap 分区，沿用以前的分区设置。

    # mkfs.ext4 /dev/sda1
    # mount /dev/sda1 /mnt
    # mkdir /mnt/home
    # mount /dev/sda2 /mnt/home

<ul>
<li>格式化根分区</li>
<li>挂载根分区到 /mnt 目录</li>
<li>创建 /mnt/home 目录</li>
<li>挂载 home 分区到 /mnt/home 目录</li>
</ul>

*安装系统*

选择 pacman 的首选镜像

<pre style="margin-bottom: 0; border-bottom:none; padding-bottom:8px;"><code># vi /etc/pacman.d/mirrorlist</code></pre>
<pre style="margin-top: 0; border-top-style:dashed; padding-top:8px;"><code>Server = http://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch
Server = http://mirrors.163.com/archlinux/$repo/os/$arch</code></pre>

通过 pacstrap 安装基本系统

    # pacstrap -i /mnt base base-devel

生成 fstab 配置

    # genfstab -U -p /mnt >> /mnt/etc/fstab

chroot 到刚安装的新系统

    # arch-chroot /mnt

现在已经根目录已经更改到硬盘上刚安装的系统，所进行的一切操作也即是对新系统的，下面进行配置。

*配置系统*

修改 Locale，定义用户所使用的语言及字符集。

<pre style="margin-bottom: 0; border-bottom:none; padding-bottom:8px;"><code># vi /etc/locale.gen</code></pre>
<pre style="margin-top: 0; border-top-style:dashed; padding-top:8px;"><code>en_US.UTF-8 UTF-8
zh_CN.GB18030 GB18030
zh_CN.GBK GBK
zh_CN.UTF-8 UTF-8
zh_CN GB2312</code></pre>

    # locale-gen
    # echo LANG=en_US.UTF-8 > /etc/locale.conf
    # export LANG=en_US.UTF-8

配置时区及硬件时间

    # ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
    # hwclock --systohc --utc

设置 hostname

    # echo arch.fooleap.org > /etc/hostname

配置网络

    # pacman -S wireless_tools wpa_supplicant wpa_actiond dialog
    # wifi-menu wlan0
    # systemctl enable net-auto-wireless.service

配置 pacman，启用 multilib 源，此源可在 Arch Linux 64 位系统上运行 32 位的程序

<pre style="margin-bottom: 0; border-bottom:none; padding-bottom:8px;"><code># vi /etc/pacman.conf</code></pre>
<pre style="margin-top: 0; border-top-style:dashed; padding-top:8px;"><code>[multilib]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist</code></pre>

修改 root 密码

    # passwd

创建用户，并设置密码

    # useradd -m -g users -s /bin/bash fooleap
    # passwd fooleap

安装配置 Grub

    # pacman -S grub-bios
    # grub-install --recheck /dev/sda
    # cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo
    # grub-mkconfig -o /boot/grub/grub.cfg

到此基本系统已完成安装，可以重启进入新系统

安装使用顺手的 sudo, vim

    # pacman -S sudo vim

配置 sudo

<pre style="margin-bottom: 0; border-bottom:none; padding-bottom:8px;"><code># visudo</code></pre>
<pre style="margin-top: 0; border-top-style:dashed; padding-top:8px;"><code>root ALL=(ALL)ALL
fooleap ALL=(ALL)ALL</code></pre>

安装 ALSA，驱动声卡

    # pacman -S alsa-utils

使用 alsamixer 调整声音或通过下面命令来取消静音

    # amixer sset Master unmute

测试以判断声卡是否工作

    # speaker-test -c 2

把用户添加到 audio 组

    # gpasswd -a fooleap audio

安装 Xorg

    # pacman -S xorg-server xorg-xinit xorg-utils xorg-server-utils
    # pacman -S mesa
    # pacman -S xf86-video-intel  lib32-intel-dri  xf86-video-vesa

配置触摸板

    # pacman -S xf86-input-synaptics

<pre style="margin-bottom: 0; border-bottom:none; padding-bottom:8px;"><code># vim /etc/X11/xorg.conf.d/10-synaptics.conf</code></pre>
<pre style="margin-top: 0; border-top-style:dashed; padding-top:8px;"><code>Section "InputClass"
        ...
        Option "TouchpadOff" "1"
EndSection</code></pre>

添加 Option \"TouchpadOff\" \"1\" 以禁用触摸板

测试启动 X

    # pacman -S xorg-twm xorg-xclock xterm
    # startx

把用户添加到 video 组

    # gpasswd -a fooleap video

安装字体

    # pacman -S wqy-bitmapfont wqy-zenhei

字体配置可以通过文泉驿的 [Fontconfig Designer](http://wenq.org/cloud/fcdesigner.html) 生成 fonts.conf 文件

安装 i3 窗口管理器及 dmenu 软件启动器，并配置

    # pacman -S i3 dmenu
    $ cp /etc/i3/config ~/.i3/config

<pre style="margin-bottom: 0; border-bottom:none; padding-bottom:8px;"><code>$ vim ~/.i3/config</code></pre>
<pre style="margin-top: 0; border-top-style:dashed; padding-top:8px;"><code>font xft:WenQuanYi Bitmap Song 10</code></pre>

使用 Windows 徽标键作为 i3 的 Mod 键

    :%s/Mod1/Mod4/g

安装 fcitx 输入法，并配置

    # pacman -S fcitx

<pre style="margin-bottom: 0; border-bottom:none; padding-bottom:8px;"><code># vim ~/.xinitrc</code></pre>
<pre style="margin-top: 0; border-top-style:dashed; padding-top:8px;"><code>export XMODIFIERS="@im=fcitx"
export QT_IM_MODULE=xim
export GTK_IM_MODULE=xim
fcitx&#38;</code></pre>

安装 firefox 及 flash 插件

    # pacman -S firefox flashplugin

安装 zathura

    # pacman -S zathura zathura-pdf-mupdf

**本文历史**

* 2011年09月25日  创建文章
* 2011年11月14日  添加修改配置以识别声卡及取消滴滴声
* 2012年02月17日  重新整理
* 2012年11月23日  重写完成初稿

