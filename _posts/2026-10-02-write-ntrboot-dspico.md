---
title: "写入 ntrboot（DSPico）"
date: 2026-10-02 00:30:00 +0800
categories: [3DS, 破解指南]
tags: [3DS, 开发机, ntrboot, DSPico]
author: adnini983
media_subpath: /assets/img/posts/3ds-devkit-guide/
permalink: /posts/write-ntrboot-dspico/
toc: true
pin: false
---

**提示：如果你已经给烧录卡写入了ntrboot开发机版的启动固件，你可以跳过这里，直接阅读[安装 boot9strap (ntrboot)](/posts/install-boot9strap-ntrboot/)**

## 你需要准备：
- 本体带有microUSB 或 USB Type-C接口的DSPico烧录卡
- microUSB数据线或USB Type-C数据线(根据烧录卡自身的接口选择)
	- 数据线不宜过长(至多80cm)，否则连接过程中可能会掉线。
- 下载 [DSpico-profi200-dev.uf2](https://github.com/coderkei/dspico-hybrid-fw/releases/download/1.4/DSpico-profi200-dev.uf2)

## 步骤
- 1 移除DSPico卡槽里的microSD卡(如果有)
- 2 使用microUSB数据线或USB Type-C数据线连接电脑
- 3 在电脑上打开卷标为"RPI-RP2"的外置磁盘分区
- 4 将文件"DSpico-profi200-dev.uf2"复制到卷标为"RPI-RP2"的外置磁盘分区内
- 5 等候2-5秒，DSPico会自动弹出并重新连接电脑。
- 6 将DSPico从数据线上移除
- 7 插回DSPico的microSD卡(如果有)

**继续至安装 [安装 boot9strap (ntrboot)](/posts/install-boot9strap-ntrboot/)**

**Louvre New 3DS XL机型请继续至 [安装 boot9strap (ntrboot)(仅限Louvre New 3DS XL)](/posts/install-boot9strap-ntrboot-louvre-n3dsxl/)**
