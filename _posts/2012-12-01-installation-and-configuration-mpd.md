---
layout: post
title: "安装和配置 MPD"
description: "使用 i3 窗口管理器，感觉很舒服，更有帅帅的 i3status 点缀之，在 GitHub 搜了下，发现有个 i3status 修改版，可以显示 MPD 的播放状态，于是又用起 MPD。"
category: linux
tags: [MPD, MPC, 播放器]
---
{% include JB/setup %}

使用 i3 窗口管理器，感觉很舒服，更有帅帅的 i3status 点缀之，在 GitHub 搜了下，发现有个 [i3status 修改版](https://github.com/Gravemind/i3status)，可以显示 MPD 的播放状态，于是又用起 MPD。

MPD ([Music Player Daemon](https://wiki.archlinux.org/index.php/Music_Player_Daemon)) 是一个实用的音乐播放器，以其独特的 C/S 结构获得人们的喜爱。充其量 MPD 只是作为一个守护进程（或者可以说服务）运行于后台，想要控制它的播放，还需要一个客户端，一般只选用 MPC， MPC 虽为命令行客户端，但已够用。

下面一起来安装配置 MPD，获得恰到好处的使用体验

*MPD*

安装 MPD, MPC

    # pacman -S mpd mpc

创建 MPD 的配置文件

<pre style="margin-bottom: 0; border-bottom:none; padding-bottom:8px;"><code>vim ~/.mpdconf</code></pre>
<pre style="margin-top: 0; border-top-style:dashed; padding-top:8px;"><code>music_directory         "~/Music/"
playlist_directory      "~/.mpd/playlists"
db_file                 "~/.mpd/database"
log_file                "~/.mpd/log"
pid_file                "~/.mpd/pid"
state_file              "~/.mpd/state"
user                    "fooleap"
group                   "users"
bind_to_address         "localhost"
port                    "6600"
audio_output {
	type            "alsa"
	name            "My ALSA Device"
	mixer_control   "Master"
}</code></pre>

更多配置可参考 /usr/share/mpd/mpd.conf.example

    $ mkdir -p ~/.mpd/playlists
    $ touch ~/.mpd/{database,log,pid,state}

至此，可直接运行 mpd 命令，启动 mpd 服务

*MPC*

    $ mpc listall | mpc add
    $ mpc play

<ul>
<li>添加所有音乐到当前播放列表</li>
<li>播放</li>
</ul>

播放列表

通过 MPC 创建的是 \*.m3u 格式的 Playlist

假设 ~/Music 文件夹里有多个文件夹，创建播放列表，包含某目录（或多目录）下所有音乐

    $ mpc clear
    $ mpc ls
    $ mpc listall Beyond* | mpc add
    $ mpc save Beyond
    $ mpc load Beyond

<ul>
<li>清空当前播放列表</li>
<li>列出文件夹</li>
<li>显示名字为 Beyond* 文件夹下的所有音乐并添加到当前播放列表</li>
<li>保存当前播放列表为 Beyond</li>
<li>读取播放列表 Beyond</li>
</ul>

也可以通过类似下面的命令来创建播放列表，萝卜青菜

    $ cd ~/Music
    $ find * -iname "*.mp3" | sort | grep Beyond > ~/.mpd/playlist/Beyond.m3u

更多使用可以参考 man mpc

*多媒体键*

使用 Thinkpad 多媒体键来代替常用的 mpc 命令再合适不过，这里通过 [Xbindkeys](https://wiki.archlinux.org/index.php/Xbindkeys) 来绑定

安装 Xbindkeys

    # pacman -S xbindkeys

配置 Xbindkeys

<pre style="margin-bottom: 0; border-bottom:none; padding-bottom:8px;"><code>vim ~/.xbindkeysrc</code></pre>
<pre style="margin-top: 0; border-top-style:dashed; padding-top:8px;"><code>"mpc toggle"
XF86AudioPlay

"mpc stop"
XF86AudioStop

"mpc prev"
XF86AudioPrev

"mpc next"
XF86AudioNext

"amixer sset Master 2-"
XF86AudioLowerVolume

"amixer sset Master 2+"
XF86AudioRaiseVolume

"amixer sset Master toggle"
XF86AudioMute</code></pre>

将 xbindkeys & 添加到 ~/.xinitrc 随 X 启动

*键映射*

在此之前，可能需要通过 [Xmodmap](https://wiki.archlinux.org/index.php/Xmodmap) 修改键映射

<pre style="margin-bottom: 0; border-bottom:none; padding-bottom:8px;"><code>vim ~/.Xmodmap</code></pre>
<pre style="margin-top: 0; border-top-style:dashed; padding-top:8px;"><code>!Media
keycode 173 = XF86AudioPrev
keycode 172 = XF86AudioPlay
keycode 171 = XF86AudioNext
keycode 174 = XF86AudioStop

!Volume
keycode 121 = XF86AudioMute
keycode 122 = XF86AudioLowerVolume
keycode 123 = XF86AudioRaiseVolume</code></pre>

将 xmodmap ~/.Xmodmap & 添加到 ~/.xinitrc 使其随 X 启动

![i3status with mpd](http://pic.yupoo.com/fooleap_v/CsoTzarg/pbFZZ.png)

**本文历史**

* 2012年12月01日 创建文章
