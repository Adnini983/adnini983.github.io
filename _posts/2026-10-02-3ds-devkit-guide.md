---
title: "3DS开发机破解指南（第三版）"
date: 2026-10-02 00:00:00 +0800
categories: [3DS, 破解指南]
tags: [3DS, 开发机, 破解, boot9strap]
author: adnini983
media_subpath: /assets/img/posts/3ds-devkit-guide/
permalink: /posts/3ds-devkit-guide/
toc: true
pin: true
---

![](res/start_banner.png)

本指南的最终目的是为3DS开发机安装自制固件boot9strap，它可以让你得以在3DS开发机内做任何你想做到的事情，而不需要获得任天堂的许可。

3DS开发机仅为3DS游戏软件开发套件的其中一部分，而对于通过非任天堂官方渠道所获得的开发机来说，破解几乎是能够安装并运行3DS游戏软件的唯一办法。

**提示：建议使用PC端浏览器打开本指南，以获得最佳的阅读体验。**

## 在开始之前，我需要了解什么？

- 在开始执行破解之前，你需要了解尝试破解3DS开发机的风险：每次对系统的修改，都有可能会导致机器砖机。虽然遵循本指南操作不会砖机，但瞎搞一定会，所以请不要跳过每一个步骤。
- 本指南适用于所有地区版本的3DS开发机以及所有已知的机型。
- 如果一切都按照本指南进行，你不仅不会丢失任何你原先的数据，还会获得你想要的效果。
- 确保你的机器全程保持着插电或充电的状态，以防止因意外关机而造成的砖机或数据丢失。
- 你的储存卡的分区表格式必须为MBR格式，不能为GPT格式。
- 如果你需要格式化你的储存卡，可以使用guiformat或是SDFormatter，分配单元大小设置为32KiB。
- 2DS开发机在软件方面与3DS开发机是几乎相同的，因此用于3DS开发机的步骤也可用于2DS开发机。

## 本指南与哪些机型兼容？

### 确定可兼容的机型有：
- PANDA系列：
	- CTR(旧版3DS测试机)
	- SPR(旧版3DSLL测试机)
	- FTR(旧版2DS测试机)
	- SNAKE(New 3DS测试机)
	- CLOSER(New 3DSLL测试机)
- IS系列：
	- PARTNER-CTR系列(白盒) 包括Capture/Debugger/Capture Debugger(旧版3DS投屏机)
	- IS-CTR-DEBUGGER(绿盒) 包括SPR(旧版3DS开发机)
	- IS-SPR-DEBUGGER(绿盒) 包括CAPTURE(旧版3DSLL开发机)
	- IS-SNAKE-DevKit(橙盒) (New 3DS开发套件)

### 理论可兼容但需进一步测试的机型有：
- PANDA系列：
	- JAN(New 2DSLL测试机)
- IS系列：
	- IS-CTR-BOX 包括Expansion Kit (有开发机卡带刷写的功能 附带调试器和官方模拟器)
	- IS-SNAKE-TESTER(橙盒) (带主机的New 3DS测试机)
	- IS-SNAKE-BOX(橙盒)(有开发机卡带刷写的功能 附带调试器和New 3DS官方模拟器)
	- IS-RAY-DEBUGGER(SNAKE-BOX原型机)

## 开始

在开始破解之前，我们需要确认你手里的机器是否已经应用了某些破解方案，并确定你的机器当前的SDK版本是什么。

### 一部分 - CFW检查
1. 将机器关机
2. 按住"Select"键
3. 在按住"Select"键的同时按下电源键
4. 如果你没有看到任何自制软件/固件的设置菜单(正常情况下只会进入主菜单或测试菜单) 你可以继续往下看

### 二部分 - SDK版本检查

1. 在机器中打开"Dev Menu"
2. 你的SDK版本可在上屏中的"Firmware Ver."的右侧看到(例如"0.28.0(r62419)"
![](res/SDK_VersionCheck.jpg)

### 三部分 - 选择一个方案
要想为你的机器选择适合的破解方案，你需要根据二部分中看到的SDK版本，以及你的机型选择适合的方案
| 机型 | SDK版本 | 方案 |
| :---: | :---: | :---: |
| CTR/SPR<br>FTR<br>SNAKE/CLOSER | 0.14.24-0.25.4<br>0.19.6-0.25.4<br>0.22.16-0.25.4 | [soundhax](/posts/install-boot9strap-soundhax/) |
| CTR/SPR/FTR<br>SNAKE/CLOSER | 0.25.5-0.27.0 | [降级至0.25.4](/posts/downgrade-to-0-25-4/)<br>或<br>[升级至0.35.0](/posts/upgrade-to-0-35-0/) |
| JAN | 0.25.5-0.27.0 | [升级至0.35.0](/posts/upgrade-to-0-35-0/) |
| 全机型 | 0.28.0-0.35.0 | [MEST9-devkit](/posts/install-boot9strap-mest9-cli/) |
| 连接外部硬件 | 任意/损坏 | [ntrboot](/posts/write-ntrboot/)<br>[CTR SystemUpdater](/posts/ctr-systemupdater-ctr-008/) |

**以下是特殊机型适用的破解方案**
- [Louvre New 3DS XL](/posts/launch-devmenu-louvre-n3dsxl/)：需要确保"Dev Menu"可以正常运行
- [原型机/工程机/系统损坏](/posts/system-completely-broken/)：需要可兼容的DS烧录卡或者CTR-008开发机卡带以及对应的烧录设备
