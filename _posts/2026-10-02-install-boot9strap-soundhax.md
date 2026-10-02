---
title: "安装 boot9strap（soundhax）"
date: 2026-10-02 00:05:00 +0800
categories: [3DS, 破解指南]
tags: [3DS, 开发机, boot9strap, soundhax]
author: adnini983
media_subpath: /assets/img/posts/3ds-devkit-guide/
permalink: /posts/install-boot9strap-soundhax/
toc: true
pin: false
---

## 你需要准备：

- 在[SoundHax](http://soundhax.com/)下载用于触发漏洞的M4A文件，区域和机型根据实际情况选择，系统版本可参考[这里](/assets/img/posts/3ds-devkit-guide/res/update_table.png)。
- 最新版本的 [SafeB9SInstaller](https://github.com/d0k3/SafeB9SInstaller/releases/download/v0.0.7/SafeB9SInstaller-20170605-122940.zip)
- 最新版本的 [boot9strap Devkit](https://github.com/SciresM/boot9strap/releases/download/1.4/boot9strap-1.4-devkit.zip)
- 最新版本的 [Luma3DS](https://github.com/LumaTeam/Luma3DS/releases/latest)(下载".zip"文件)
- 最新版本的 [universal-otherapp](https://github.com/TuxSH/universal-otherapp/releases/latest)(下载"otherapp.bin"文件)

## 步骤
### 一部分 - 准备工作
在本节中 你将需要复制触发soundhax所需的M4A文件和universal-otherapp所需的BIN文件

- 1 将机器关机
- 2 将机器的储存卡插入电脑中
- 3 将"soundhax-***-*3ds-post5.0.m4a"复制到储存卡的根目录内
- 4 将"otherapp.bin"复制到储存卡的根目录内
- 5 将"Luma3DS***.zip"里面的所有内容解压缩至储存卡的根目录内
- 6 新建一个名为"boot9strap"的文件夹
- 7 将"boot9strap-1.4-devkit.zip"压缩档内的所有文件解压至储存卡内的"/boot9strap/"文件夹
- 8 将"SafeB9SInstaller-20170605-122940.zip"压缩档内的"SafeB9SInstaller.bin"文件解压至储存卡根目录
- 9 将储存卡插回机器内
- 10 将主机开机
![](res/soundhax_directory_structure.jpg)
![](res/boot9strap_dev.png)

### 二部分 - 运行 SafeB9SInstaller
在本节中，你将通过3DS的音频播放器(Nintendo 3DS Sound)触发soundhax漏洞，此方法将会调用 universal-otherapp 来启动 boot9strap (自制固件)安装程序。

- 1 启动"Nintendo 3DS Sound"
	- 如果你以前从未打开过"Nintendo 3DS Sound"，会出现初次使用此应用的教程，你只需要正常走完其流程，就可以进行下一步的操作。
- 2 播放"❤️ nedwill 2016"
	- 这可能需要多次尝试(至多10次)
	- 如果你看到"Could not play(无法播放)"的消息，说明你下载到了错误版本的M4A文件，或是与你当前系统的版本不兼容。
	- 如果机器卡死了，请按住电源键以执行强制关机，然后重试。
- 3 如果漏洞触发成功，你将会看到 SafeB9SInstaller。

### 三部分 - 安装 boot9strap
在本节中，你将在机器中安装自制固件

- 1 依次输入上屏显示的组合键来安装boot9strap
- 2 完成后，按"A"键重启你的机器。
- 3 你的机器应该已经自动进入到Luma3DS的配置菜单了。在本指南中，暂时不要改动这些选项，保持默认即可。
- 4 按"Start"键保存设置并重启

**继续至[完成破解](/posts/finalizing-setup/)**
