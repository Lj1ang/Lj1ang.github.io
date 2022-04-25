---
title: "LinuxStartup"
date: 2022-03-25T22:58:10+08:00
slug: ""
description: ""
keywords: []
draft: false
tags: []
math: false
toc: ture

---

## Preface  

写这篇帖子的起因是前几天给ubnubtu装了个KDE，于是我的linux有了GNOME和KDE两套GUI，紧接着出现了各种问题。直到今天中午我的linux在recovery模式下彻底卡死，我打算重新装一个ubuntu。这篇帖子旨在帮助初学者快速装上双系统并解决linux的网络和中文输入法等问题，不必花大量时间看一些无效的解决方案。

 ## Part1  

[win11+ubuntu20.04.4LTS双系统](https://zhuanlan.zhihu.com/p/362092786)这个教程是完全可行的，解释一下里面没有细讲的一些步骤 #### 安装类型的选择 为什么**不选择** “安装ubuntu与windows manager共存”？ ubuntu与windows manager共存意味着 把ubuntu的引导程序安装在windows的系统盘（即C盘），这样如果你的ubuntu除了问题可能会连带这windows[一起出问题。](https://www.quora.com/What-does-installing-Ubuntu-alongside-Windows-mean#:~:text=In%20short%2C%20it%20means%20to,case%20after%20you%20are%20done. )

### 分区类型 

分为[primary partition 和logical partition](https://www.differencebetween.com/difference-between-primary-partition-and-vs-logical-partition/#:~:text=Primary%20partition%20is%20a%20bootable,data%20in%20an%20organized%20manner. )

- primary partition: 是一个可引导分区，上面的教程把该分区用于efi引导 
- logical partition：非引导分区，用于存放数据 

## Part2 如何魔法上网 



### VPS

首先你需要一个vps，然后你需要一个代理客户端。 

贴一个[腐竹写的帖子](https://bbs.scumaker.org/t/topic/198 )

以及[yxh 写的帖子](https://bbs.scumaker.org/t/topic/197) 

我自己选择了搬瓦共的vps 

### 代理客户端 

首先，在linux下运行一个可执行文件的方法不一定是双击。右键打开终端，进到当前目录， chmod +x ./你的文件名 目前了解到的代理客户端种类

- qv2ray
- v2raya
- clash

我自己使用的是[qv2ray.v1.99.6-linux.AppleImage客户端以及v2ray-core作为核心文件](https://www.zsxcool.com/7137.html) 

这篇可以了解一下[如何配置qv2ray](https://github.com/233boy/v2ray/wiki/V2Ray%E6%90%AD%E5%BB%BA%E8%AF%A6%E7%BB%86%E5%9B%BE%E6%96%87%E6%95%99%E7%A8%8B)

这篇讲是实操。需要自己缝合一下两篇教程，把vmess贴到qv2ray里去（比较新版的qv2ray似乎不支持vmess了？） 

到现在可以实现浏览器的科学上网了。但是shell还不行，所以会用不了git 

### 配置shell代理

export https_proxy=127.0.0.1:你主机的https代理端口

那么这个代理端口去哪里找？ 

查看代理客户端或者系统设置里的代理，通常是代理客户端有一个默认值



## Part3 输入法 

ubuntu自带的输入法没有中文输入（反正我没找到） 

解决方案

[这一篇讲的是如何下载输入法](https://askubuntu.com/questions/59356/how-do-i-get-chinese-input-to-work)

[然后借鉴这一篇的配置方法](https://www.linkedin.com/pulse/installing-pinyin-input-method-ubuntu-2004-chinese-post-ron-li/) 



## Part4 一些常见软件

[Twitter](https://vitux.com/how-to-use-twitter-lite-app-on-ubuntu/#:~:text=Click%20on%20the%20three%20vertical,button%20to%20install%20the%20app.)

[QQ](https://github.com/xiaozhangup/Icalingua/actions/runs/1859799770) 

[UxPlay](https://github.com/FDH2/UxPlay)



## Part5 Ubuntu下的Nvidia driver

在CLI

```bash
$sudo nvidia-settings
```

[PRIME Profiles --> NVIDIA(Performance Mode)](https://forums.developer.nvidia.com/t/cant-install-nvidia-driver-in-ubuntu-20-04-2-kernel-version-5-8-0-55/180785/11)

开启电脑和显示器的高刷

## Part6 各种环境问题

### conda

#### 创建环境

```bash
$ conda create -n new --clone base
```

or

```bash
$ conda list --export > requirements.txt
$ conda create -n new --file requirements.txt
```

[原帖](https://stackoverflow.com/questions/58513745/create-virtual-environment-with-all-packages-shown-in-conda-list)

### Linux 环境变量

`export $D2L=/...`

写入~/.profile 并 re-login

### PlatformIO get-platformio.py httperror

solution:

```bash
$export https_proxy="https://127.0.0.1:8888"
$export http_proxy="http://127.0.0.1:8888"
```



## Part7 客制化之路

### shell

zsh

### extension

```bash
$sudo apt install gnome-tweaks
$ sudo apt install dconf-editor
$ gsettings set org.gnome.shell.extensions.dash-to-dock extend-height false
$ gsettings set org.gnome.shell.extensions.dash-to-dock dock-position BOTTOM

```

### shell

[What is shell and How to change shell](https://itsfoss.com/install-switch-themes-gnome-shell/)

### theme

- whiteSur-gtk-theme and icon
- McMojave

### icon

- mkos-big-sur
- 

### wallpaper 

- art blocks
- 

## 一些小坑

### git

`git remote set-url origin https://github.com/Lj1ang/convert2bitmap.git`

`git push -uf origin main`

