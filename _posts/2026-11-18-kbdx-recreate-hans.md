---
title: "「卡比检定DX」AI修复汉化版"
date: 2026-11-05 22:34:00 +0800
categories: [游戏, 汉化]
tags: [星之卡比, Flash, 修复, 汉化, 重现]
author: adnini983
media_subpath: /assets/img/posts/kbdx-recreate-hans/
toc: true
pin: false
---

## 前言

「カービィ検定DX」(卡比检定；别称：卡比问答)是一款星之卡比系列的非官方同人游戏，原作者是“正体不明（あんのうん）”，前作为「カービィ検定EX」。

游戏于2016年5月上线，之后于2021年9月因个人博客关闭而下线。虽然我在2025年3月10日发现了.swf客户端游戏本体，但服务端数据仍然无法还原。
直到今年(2026年)的11月10日，我成功用DSH尝试重写了第一版服务端……

![](QQ_2026-11-18_22-18-24.jpg)

## 说明

目前服务端的最新版本为1.1，1.0暂无已构建好的整合包。

因为服务端是我用DSH完全重写的，因此只还原了一部分题型，其它的题型暂未实现。

如果需要修改题库或活动模式的相关文案，里面也内置有相关工具。

另外我还尝试给游戏本身做了汉化，不懂日文的也可以无障碍玩耍。

### 线上游玩

这里的线上游玩仅还原了在线高分榜和在线题库特性，Web打开即玩暂无法实现。

实际游玩需要使用本地Flash播放器(例如Ruffle)来手动打开SWF链接。

※：因域名暂未对中国内地做访问优化，打开速度可能较慢，建议配合代理使用。

- 个人主域：[https://kbdx.adnini983.com/](https://kbdx.adnini983.com/)

- Cloudflare域：[https://kbdx.adnini983.workers.dev/](https://kbdx.adnini983.workers.dev/)

### 整合下载

整合用于电脑本地运行，内含运行时和Ruffle客户端，服务端则包含Java端和Python双端，均可在Windows和Linux一键运行。

※：如果你的Linux发行版没有内置Python 3.9+运行时，你可以运行Java端，也可以先安装Python 3.9+运行时。

- [百度网盘下载](https://pan.baidu.com/s/1k4Na-c6u97gNC86I1ASICw?pwd=kbdx) 提取码: kbdx 

- [移动网盘下载](https://yun.139.com/shareweb/#/w/i/2yA8J0wGLwB9d) 提取码: bd65

### 手动构建

- 在这里下载原始[main.swf](https://web.archive.org/web/20190715021340oe_/https://un-no-un.net/kbDX/main.swf)

- 在这里下载[服务端源码](https://github.com/Adnini983/kbDX-server-recreate)，然后阅读`README.md`的“快速开始”部分。

## 其它

如果有任何问题，可添加我的QQ群，欢迎理性讨论和友好交流：[1076530032](https://qm.qq.com/q/hVOKXTliWA)

## 相关链接

- [中文失传媒体Wikidot](https://lostmedia.wikidot.com/kabiwendadx)

