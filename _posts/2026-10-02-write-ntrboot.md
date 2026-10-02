---
title: "写入 ntrboot"
date: 2026-10-02 00:25:00 +0800
categories: [3DS, 破解指南]
tags: [3DS, 开发机, ntrboot, 烧录卡]
author: adnini983
media_subpath: /assets/img/posts/3ds-devkit-guide/
permalink: /posts/write-ntrboot/
toc: true
pin: false
---

**提示：如果你已经给烧录卡写入了ntrboot开发机版的启动固件，你可以跳过这里，直接阅读[安装 boot9strap (ntrboot)](/posts/install-boot9strap-ntrboot/)**

## 前言
利用ntrboot后门来安装 boot9strap 需要一张可兼容的DS烧录卡。请注意，虽然部分烧录卡也集成了ntrboot功能，但它们仅适用于3DS零售机，在3DS开发机上无效。

尽管ntrboot后门可以无视系统SDK版本(甚至不需要机器要有一个正常可用的系统)，但 ntrboot flasher 仅支持部分DS烧录卡。这意味着，根据你当前的SDK版本以及你已拥有的DS烧录卡的情况下，可能只有某个方案才适合你。

部分烧录卡具有"时间炸弹"的机制，当烧录卡检测到当前的系统时间超过了预设的值，烧录卡会拒绝启动，解决方法则是手动把系统时间改到较早的值。

推荐的烧录卡：

| 烧录卡名称 | 说明 |
| --- | --- |
| DSPico | 开源烧录卡，可通过混合固件实现支持开发机ntrboot引导和游戏卡双模式。 |
| Acekard 2i | 同样支持开发机ntrboot引导和游戏卡双模式，但仅有HW44和HW81批次才可以，且只能在DS和已破解的DSi/3DS中作为游戏卡使用。<br>兼容的SDK版本：≤0.17.21 / 兼容的DSi系统版本：≤1.4.4 |

其它种类的烧录卡：

| 烧录卡名称 | 时间炸弹 | 兼容的SDK版本 | 兼容的DSi系统版本 | 备注 |
| --- | --- | --- | --- | --- |
| DSTT | 无 | 不支持 | 不支持 | 只有部分使用了特定的闪存芯片才可以支持ntrboot，且需要一台DS才可以启动DSTT。 |
| Gateway Blue | 无 | 0.17.17-<br>0.17.48 | 1.4.5 | 仅有部分批次的卡才可以支持ntrboot |
| R4i-SDHC 3DS RTS<br>(r4i-sdhc.com) | 1.85b内核：<br>2024/9/3 | 全部 | 全部 | —— |
| R4iSDHC GOLD Pro 20XX<br>(r4isdhc.com) | 4.0b内核：<br>2024/9/3 | 全部 | 全部 | 只有标注为2014年或以后的年份才支持 |
| R4iSDHC RTS LITE 20XX<br>(r4isdhc.com) | 4.0b内核：<br>2024/9/3 | 全部 | 全部 | 只有标注为2014年或以后的年份才支持 |
| R4iSDHC Dual-Core 20XX<br>(r4isdhc.com) | 4.0b内核：<br>2024/9/3 | 全部 | 全部 | 只有标注为2014年或以后的年份才支持 |
| Infinity 3 R4i<br>(r4infinity.com) | 无 | 全部 | 全部 | —— |
| R4i Gold 3DS<br>(r4ids.cn) | 无 | 全部 | 全部 | 所有批次都支持 |
| R4i-SDHC 3DS RTS Deluxe Edition | 未知 | 全部 | 全部 | 只有蓝色贴纸的豪华版支持 |

在开始之前，请确保你的烧录卡符合上述列表中的一个，且可以正常运行NDS文件。以上的烧录卡都需要将对应的烧录卡固件或内核给复制到烧录卡使用的microSD卡里，才可以正常使用。有关于DS烧录卡的固件或内核问题，请自行查阅相关的使用说明，这里不单独列出。

如果你的机器是翻盖式的(所有没有2DS的独立睡眠开关的3DS机型)，要想使用ntrboot后门，那必须要准备一块磁铁。这是因为触发ntrboot后门需要机器处于睡眠模式状态下的同时也能按下机器上的按键。

要测试磁铁是否能使用，请在机器开机状态时将其放在 ABXY按键上方或右侧，以判断它是否可以让机器进入睡眠模式。正常情况下，只要磁铁放置在该位置，上下屏都会变黑。

请注意，当ntrboot固件被刷写到DS烧录卡内时，它们的原有功能是无法使用的(DSPico与Acekard 2i除外，它们仍然能够在DS与已破解的3DS上使用。)。这意味着，大多数的烧录卡都是不会在主菜单上显示任何图标的。关于如何恢复烧录卡的原有功能，本文文末中会详细说明。

## 提示：

- 在某些情况下，刷写过程可能会使假冒烧录卡变砖并使其永久无法使用，虽然几率较低。但尽管如此，请仅使用上文列出的烧录卡。为了减少买到假卡的几率，建议你寻找信誉良好的卖家或网站来购买烧录卡(这里不做推荐)。

- 你可以使用DS或其它已破解的DSi/3DS机器来执行写入ntrboot的操作，在此条件下可以不用考虑烧录卡对机器兼容性的问题。

- 如果你要为DSTT写入ntrboot，你需要使用DS来操作，并[在此查看](https://gist.github.com/aspargas2/fa2a70aed3a7fe33f1f10bc264d9fab6)你手里的DSTT的闪存是否符合要求。

- 如果你要为DSPico写入ntrboot，请前往[写入ntrboot(DSPico)](/posts/write-ntrboot-dspico/)。

## 你需要准备：
- 与DS/DSi/3DS兼容的烧录卡
- 最新版本的[ds_ntrboot_flasher_dsi.nds](https://github.com/ntrteam/ds_ntrboot_flasher/releases/download/v4.0/ds_ntrboot_flasher_dsi.nds)

## 步骤
### 一部分 - 准备工作
- 1 将机器关机
- 2 将烧录卡的microSD卡插入电脑
- 3 复制"ds_ntrboot_flasher_dsi.nds"文件至你的microSD卡里(烧录卡的)。
- 4 将microSD卡重新插入烧录卡内
- 5 将烧录卡插入机器的卡槽内

### 二部分 - 写入ntrboot
- 1 启动烧录卡，在烧录卡内核里运行"ds_ntrboot_flasher_dsi.nds"。
- 2 按"A"键继续
- 3 使用十字键↑和↓找到你的烧录卡信息
- 4 按"A"键继续
- 5 按"A"键执行"inject ntrboothax"
- 6 按"X"键选择"DEV"模式
- 7 按"A"键继续
- 8 选择"EXIT"以退出

**继续至[安装 boot9strap (ntrboot)](/posts/install-boot9strap-ntrboot/)**

**Louvre New 3DS XL机型请继续至[安装 boot9strap (ntrboot)(仅限Louvre New 3DS XL)](/posts/install-boot9strap-ntrboot-louvre-n3dsxl/)**
