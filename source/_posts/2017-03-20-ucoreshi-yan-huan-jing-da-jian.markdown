---
layout: post
title: "UCore实验环境搭建"
date: 2017-03-20 16:36:52 +0800
comments: true
categories: Operating Systems
---

​       清华大学的UCore和MIT的xv6比较类似，都需要用到i386-elf-gcc来编译，但在Mac上安装比较麻烦，所以我选择安装Ubuntu虚拟机。

​	这个虚拟机只做编译时使用，需要coding和qemu运行时，仍在Mac主机上进行，这就需要为Ubuntu虚拟机和主机设置共享文件夹。步骤如下：

- 在VirtualBox中安装增强插件
- 开机前设置，共享文件夹名称、位置，❗️不要勾选自动挂载
- 开机后terminal，sudo mount -t vboxsf (共享文件夹名) /mnt/(挂载点名)

完成😀