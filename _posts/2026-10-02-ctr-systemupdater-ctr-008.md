---
title: "CTR SystemUpdater（CTR-008）"
date: 2026-10-02 00:40:00 +0800
categories: [3DS, 破解指南]
tags: [3DS, 开发机, CTR-008, 刷机]
author: adnini983
media_subpath: /assets/img/posts/3ds-devkit-guide/
permalink: /posts/ctr-systemupdater-ctr-008/
toc: true
pin: false
---

## 前言：
在本文中，你将需要3DS开发套件中的指定设备为开发机烧录卡CTR-008写入"CTR SystemUpdater"更新程序，并为目标机器执行刷机程序。

在IS系列开发机中，已知仅有部分后缀为"Debugger"或"BOX"的子型号(例如Partner-CTR Debugger)以及专用的"PARTNER-CTR Writer"烧录器具备此功能。如果你没有上述的所有设备，请寻求其它替代方案，或等候下一次重大更新。

## 你需要准备：
- IS-***-Debugger 或 Partner-CTR Debugger开发机
	- 也可以使用 PARTNER-CTR Writer烧录器 它可以实现至多8张卡带同时烧录
- CTR-008开发机卡带(长条状16Gbit储存空间 贴纸不能有"Prototype"字样)
- 电脑端相关控制软件(可在Gigaleak中找到 这里不提供)
- 根据你自己需要刷机的3DS开发机系统的区域版本，下载对应的系统包。
	- SNAKE / CLOSER / JAN CSU 0.35.0 日版 [提取码：6l3e](https://cloud.189.cn/t/aMjE7be26Zbi) / [备用链接：rxu5](https://pan.baidu.com/s/12Z4aTdRu243ZWa7zQ4dPjg?pwd=rxu5)
	- SNAKE / CLOSER / JAN CSU 0.35.0 美版 [提取码：xe4a](https://cloud.189.cn/t/vAF3EfArA7fe) / [备用链接：884w](https://pan.baidu.com/s/1O4vW0LT6VPW6jKvh_sFcDw?pwd=884w)
	- SNAKE / CLOSER / JAN CSU 0.35.0 欧版 [提取码：hs8l](https://cloud.189.cn/t/InEjiaRNZviu) / [备用链接：pttz](https://pan.baidu.com/s/19YU6mKnWsp04nIOU_kA4-Q?pwd=pttz)
	- SNAKE / CLOSER / JAN CSU 0.35.0 韩版 [提取码：5xgp](https://cloud.189.cn/t/6jqqiiER3iYz) / [备用链接：h5j3](https://pan.baidu.com/s/1ggGET4Of_9qXkxwvRkB2XQ?pwd=h5j3)
	- 
	- CTR / SPR / FTR CSU 0.35.0 日版 [提取码：8xoy](https://cloud.189.cn/t/V7nMbaYRzeei) / [备用链接：u2mk](https://pan.baidu.com/s/1WPTSK530nQMmwnV7an1hnw?pwd=u2mk)
	- CTR / SPR / FTR CSU 0.35.0 美版 [提取码：knz8](https://cloud.189.cn/t/rmqyyyArAVfm) / [备用链接：eue3](https://pan.baidu.com/s/1KTzm6cKGcZ7mpuPyYfrC5Q?pwd=eue3)
	- CTR / SPR / FTR CSU 0.35.0 欧版 [提取码：l848](https://cloud.189.cn/t/QFviqu2EVFFr) / [备用链接：qcx8](https://pan.baidu.com/s/13mHiCyB_EPVxoYLBjejixQ?pwd=qcx8)
	- CTR / SPR / FTR CSU 0.35.0 韩版 [提取码：v5de](https://cloud.189.cn/t/MN7NBfyQfeAr) / [备用链接：gd7c](https://pan.baidu.com/s/1o5rN7qWgid3l6NjZ551Jkw?pwd=gd7c)
	- CTR / SPR / FTR CSU 0.35.0 港台版 [提取码：3edr](https://cloud.189.cn/t/Uvu22uNBfEvq) / [备用链接：mqx7](https://pan.baidu.com/s/1AXcrJ3fDyHYzI08q-ef1Lw?pwd=mqx7)
	- CTR / SPR / FTR CSU 0.35.0 神游版 [提取码：x7nx](https://cloud.189.cn/t/YjU7niziMbuy) / [备用链接：av7v](https://pan.baidu.com/s/1UnmxrJFakhvE04JN5g5y1Q?pwd=av7v)

## 步骤(由于技术限制 部分操作细节暂无法写明)
### 一部分 - 写入"CTR SystemUpdater"更新程序 (在IS开发机中操作)
- 1 将机器开机
- 2 将开发机卡带插入机器上的卡槽
- 3 使用USB连接线连接电脑与机器
- 4 启动电脑上的控制软件
- 5 在软件中打开"SystemUpdater_***-0_35_0-**.csu"文件
- 6 在软件中使用烧录功能将文件写入之开发机卡带内
- 7 待进度条跑完，可在机器中测试已经写入完成的卡带。

### 二部分 - 执行刷机(在目标机中操作)
- 1 将机器开机
- 2 将开发机卡带插入机器上的卡槽
- 3 运行卡带
- 4 按照[官方指南](https://adnini983.lanzouq.com/iCM8N4ao814h)执行刷机程序

**继续至[安装boot9strap(MEST9 CLI)](/posts/install-boot9strap-mest9-cli/)**

**如果你是给已破解的3DS开发机执行系统更新/区域变更操作，那么所有的工作都已完成。**
