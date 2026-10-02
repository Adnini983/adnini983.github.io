---
title: "系统完全损坏"
date: 2026-10-02 00:55:00 +0800
categories: [3DS, 破解指南]
tags: [3DS, 开发机, 救砖]
author: adnini983
media_subpath: /assets/img/posts/3ds-devkit-guide/
permalink: /posts/system-completely-broken/
toc: true
pin: false
---

## 提示：
- 如果你的机器不属于任何一种定制机型，且仍然可以通过某种方式运行"Dev Menu"，可以跳过这里，直接阅读[升级至0.35.0](/posts/upgrade-to-0-35-0/)。
- 如果你的机器不但可以运行零售3DS卡带，还可以使用零售机ntrboot方案以及刷机方案，说明你的机器不属于开发机，不适用这里的指南。

## 前言：
目前市面上正在流通的开发机里，除了正常提供给开发者使用的PANDA系列与IS系列，以及专供给大客户的定制机型(例如"Louvre New 3DS XL")以外，有小批量的，是从内部管道流出的原型机或工程机机型。它们普遍存在一个或多个问题：

- 仅可运行开发机卡带(CTR-008系列)或DS卡带，无法运行零售DSi/3DS卡带
	- 如果可以运行，那就说明**是零售机机型，不适用这里的指南。**
- 机身外观与量产机型/开发机型差异极大
- 机身外观与量产机型/开发机型几乎没有差异，但外观可能存在划痕或破损。
- 外壳使用从未大量出现过的配色方案。
- 没有锂电池触点，或者没有D壳，只能通过连接电源适配器持续供电。
- 机身存在一些量产机型/开发机型出厂时没有的贴纸，例如"质检"等相关字样。
- 机器没有序列号贴纸，或是贴纸上的序列号是一串无意义的连续字符，例如"000000000000"。
- 机器无法被启动，或是可以启动(指示灯可以亮)，但显示屏不会显示任何画面。
- 机器可以被启动，显示开发机的测试菜单(Test Menu)，但无法启动"Dev Menu"和系统设置(System Settings)。

现阶段，针对旧版3DS系列开发机机型的CTRTransfer恢复镜像已有可用版本，然而New 3DS系列开发机机型的CTRTransfer恢复镜像仍然存在空缺。原因是"GodMode9"至今无法正确解密"New 3DS"系列开发机的"ctrnand_full.bin"文件，这也就意味着给"New 3DS"系列开发机机型刷机只能使用传统的方式。即使用特定的IS系列开发机为CTR-008开发机卡带写入"CTR SystemUpdater"更新程序，并在需要刷机的机器上运行。

**CTR/SPR/FTR 系列机型请阅读[ntrboot指南](/posts/write-ntrboot/)**

**SNAKE/CLOSER/JAN 系列机型请阅读[CTR SystemUpdater (CTR-008)](/posts/ctr-systemupdater-ctr-008/)**

**如果你的机器存在物理上的故障(例如蓝屏错误)或损毁且影响到了屏幕/SD卡槽/十字键/ABXYLR键/START键的正常使用，请维修你的机器。**
