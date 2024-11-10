---
layout:     post
title:      3DS开发机系统更新教程
subtitle:   教你不依赖开发套件也能为开发机更新系统
date:       2024-11-10
author:     Adnini983
header-img: img/post-bg-ios9-web.jpg
catalog: 	 true
tags:
    - 3DS
    - 开发机
    - CTR
    - SNAKE
    - Devkit
    - CSU
    - SystemUpdater
---
## 技术细节(选看)
本文直接使用toiry921编写的[CupTheCnt](https://github.com/toiry921/CupTheCnt)工具来实现直接对"CTR SystemUpdater"系列系统包的内容的提取，全程不需要依赖开发机卡带和对应的烧录设备。在过程中你需要准备一台已破解的3DS开发机，以及搭载Linux操作系统的电脑。对于Windows系统用户，可以使用Arch WSL替代([微软商店](https://www.microsoft.com/store/productId/9MZNMNKSM73X?ocid=pdpshare)/[Github](https://github.com/VSWSL/Arch-WSL))

## 你需要准备点啥？
- 一台已破解的3DS开发机 它可以是任何一种机型
- 最新版本的[Arch Linux](https://archlinux.org/download/)操作系统 
 - 如果你是Windows操作系统，在"控制面板\所有控制面板项\程序和功能"里找到"启用或关闭Windows功能"，勾选"适用于Windows的Linux子系统"，点击确定。重启完成后，下载安装最新版本的"[Arch WSL](https://github.com/VSWSL/Arch-WSL)"
 - 如果"Arch WSL"无法启动，请确保你的PC的BIOS已开启虚拟化支持。
 - 如果你是第一次使用"Arch WSL"，窗口可能会提示你建立一个用户名与登录密码，那么你需要先完成用户名的配置，才能展开下一步的工作。
![](img/Screenshot/2024-11-10-3DSDevkit-SystemUpdater/01-ArchWSL-Fistboot.PNG)
(施工中)
