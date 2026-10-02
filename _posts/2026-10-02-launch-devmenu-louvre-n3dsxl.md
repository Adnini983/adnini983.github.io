---
title: "运行 Dev Menu（Louvre New 3DS XL）"
date: 2026-10-02 00:45:00 +0800
categories: [3DS, 破解指南]
tags: [3DS, Louvre New 3DS XL, Dev Menu]
author: adnini983
media_subpath: /assets/img/posts/3ds-devkit-guide/
permalink: /posts/launch-devmenu-louvre-n3dsxl/
toc: true
pin: false
---

## 兼容性注意：
- 此方法需要确保你拥有的Louvre New 3DS XL可以通过下列方式启动"Dev Menu"。如果在反复尝试后仍无法运行，那你可能拥有的机型不是Louvre New 3DS XL，或是已经破解过的机器。
- 原装的Louvre New 3DS XL的D面壳(不是电池盖)遮挡了机器的游戏卡带卡槽，这意味着你需要临时拆除整个D面壳，或是手动更换机器的D面壳，才能够为机器插入DS/3DS开发卡带。

## 前言：
Louvre New 3DS使用的是定制的SDK版本，在机器运行后会自动运行预装在机器内置microSD卡的引导程序。它会自动与卢浮宫场馆内的内网Wi-Fi进行通信，并自动运行"Audioguide Louvre 3DS"导览软件。

正常情况下"HOME"键早已被导览软件软屏蔽处理，因此无法通过"HOME"键退回至主菜单或调试菜单。然而，仍然有一种方法可以启动内置的"Dev Menu"，并以此为跳板将SDK版本升级至正常的0.35.0。

## 你需要准备：
- 一台按键正常且拥有原装microSD卡的"Louvre New 3DS XL"

## 步骤
### 一部分 - 准备工作
在本节中，你将通过删减机器原装microSD卡的文件和文件夹，以为下一节中的启动"Dev Menu"做准备

- 1 将机器关机
- 2 将机身的microSD卡插入电脑中
- 3 将microSD卡内的所有文件和文件夹全部备份到电脑中
- 4 删减microSD卡内的文件和文件夹，确保microSD卡内只剩下这些：

~~~
microSD
|-- Nintendo 3DS
|   `-- <ID0>
|       `-- <ID1>
|           |-- dbs
|           |   |-- import.db
|           |   `-- title.db
|           `-- title
|               `-- 00040000
|                   |-- 0006a000
|                   |   `-- content
|                   |       |-- 00000002.tmd
|                   |       |-- cmd
|                   |       |   `-- 00000003.cmd
|                   |       `-- d85f5a6e.app
|                   `-- 0006a100
|                       `-- content
|                           |-- 00000002.tmd
|                           |-- cmd
|                           |   `-- 00000003.cmd
|                           `-- e2bc49ec.app
|-- cgbl2.cia
|-- lguide2.cia
|-- tmp_allFileList.txt
|-- uniqueId.dat
`-- x
    |-- chn.arc
    |-- cmn
    |   |-- Estimate
    |   |-- Floor
    |   |-- SearchRoute
    |   |-- co
    |   `-- config
    |       `-- Versioncode.dat
    |-- cmn.arc
    |-- eng.arc
    |-- fre.arc
    |-- ger.arc
    |-- ita.arc
    |-- jpn.arc
    |-- kor.arc
    |-- por.arc
    |-- spa.arc
    `-- tmp.arc
~~~
- 5 打开microSD卡根目录中的"x"文件夹，然后移除文件夹内的所有文件。
- 6 打开microSD卡根目录中的"tmp_allFileList.txt"文件，然后手动清空里面的所有内容并保存。
- 7 将microSD卡重新插入机器，暂时不要重新装回机器的电池后盖。

### 二部分 - 运行"Dev Menu"
在本节中，你将开始测试"Dev Menu"是否可以被运行

- 1 将机器开机
- 2 上屏出现提示，拔出机身的microSD卡。
- 3 下屏出现提示，按下HOME键，然后尽快按下START键。
	-  如果在按下HOME键后停留过久，请按住电源键将机器关机，然后重新执行上述步骤。
- 4 如果一切顺利，你将会看到"Dev Menu"被成功启动。

**继续至[升级至0.35.0](/posts/upgrade-to-0-35-0/)**

**如果你想在破解前备份NAND数据 请前往[写入ntrboot](/posts/write-ntrboot/)(需要兼容的DS烧录卡)**
