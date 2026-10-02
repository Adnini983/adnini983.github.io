---
title: "完成破解"
date: 2026-10-02 01:05:00 +0800
categories: [3DS, 破解指南]
tags: [3DS, 开发机, Luma3DS, 自制软件]
author: adnini983
media_subpath: /assets/img/posts/3ds-devkit-guide/
permalink: /posts/finalizing-setup/
toc: true
pin: false
---

## 前言
"boot.firm"文件是boot9strap在机器的内部储存(NAND)加载完成后启动的第一个引导程序。在本文中，我们将使用GodMode9来执行固化破解的操作。这么做可以让机器摆脱对虚拟系统(EmuNAND)的依赖，同时也可以在未插入储存卡的情况下正常开机。

另外在本文中，还将需要安装以下的自制软件：
- [GodMode9(必需)](https://github.com/d0k3/GodMode9/releases/latest)：可以对机器的原始系统(NAND)执行备份恢复操作的多功能程序
- [FBI](https://github.com/nh-server/FBI-NH/releases/latest)：安装CIA文件的应用程序，同时也具备一些Dev Menu没有的功能。
- [Homebrew Launcher Loader](https://github.com/PabloMK7/homebrew_launcher_dummy/releases/download/v1.0/Homebrew_Launcher.cia)：Homebrew Launcher的启动器
- [Anemone3DS](https://github.com/astronautlevel2/Anemone3DS/releases/latest)：自制主题安装器
- [Checkpoint](https://github.com/BernardoGiordano/Checkpoint/releases/latest)：比SaveDataFiler更易用的游戏存档管理器
- [ftpd](https://github.com/mtheall/ftpd/releases/latest)：可以使用Wi-Fi管理机器储存卡内的文件
- [Universal-Updater](https://github.com/Universal-Team/Universal-Updater/releases/latest)：提供更多自制软件下载的非官方应用商店

以上的自制软件里，除了GodMode9以外，其它的自制软件可根据自身需求选择性的下载和安装它们的.cia文件。不过如果你全部都安装上的话，它们可以有效改善你后期的使用体验。

## 一部分 - 准备工作
- 1 下载"前言"部分中列出的自制软件；
- 2 将机器关机；
- 3 将机器的储存卡插入电脑中；
- 4 在储存卡内建立一个名为"cias"的文件夹(如果没有)；
- 5 在储存卡的根目录建立一个叫"luma"的文件夹，然后在"luma"文件夹里再建立一个叫"payloads"的文件夹(如果没有)；
	- 如果在此前的破解过程中机器已安装有GodMode9，步骤5-7可以跳过。
- 6 将"GodMode9-v***-**********.zip"压缩档内的"GodMode9_dev.firm"文件解压至储存卡的"\luma\payloads\"文件夹内；
- 7 将"GodMode9-v***-**********.zip"压缩档内的"gm9"文件夹解压至储存卡根目录内；
- 8 将"FBI.cia"复制到储存卡的"cias"文件夹内；
- 9 将"Homebrew_Launcher.cia"复制到储存卡的"cias"文件夹内；
- 10 将"Anemone3DS.cia"复制到储存卡的"cias"文件夹内；
- 11 将"Checkpoint.cia"复制到储存卡的"cias"文件夹内；
- 12 将"ftpd.cia"复制到储存卡的"cias"文件夹内；
- 13 将"Universal-Updater.cia"复制到储存卡的"cias"文件夹内；
- 14 将储存卡插回机器内；
- 15 将机器开机。

## 二部分 - 更新系统
**提示：此部分不是必需的，只有你在使用过程中发现系统缺少了某些功能，或是某些游戏无法运行时，才需要考虑更新系统SDK版本。**

### 你需要准备：
- 根据你自己的3DS开发机系统的区域版本，下载对应的系统包。
- 如果需要解压密码请尝试：86stpAawc3BMPKx
	- SNAKE / CLOSER / JAN CIAs 0.35.0 日版 [提取码：itt9](https://cloud.189.cn/t/Qz2mu2YVZJ3y) / [备用链接：qaun](https://pan.baidu.com/s/1gHeIDqB8GPb-umiXdDr5Yw?pwd=qaun)
	- SNAKE / CLOSER / JAN CIAs 0.35.0 美版 [提取码：s8tm](https://cloud.189.cn/t/Qvii2eamMFBb) / [备用链接：qcy8](https://pan.baidu.com/s/1bXzHLhe62uvtu6jPP6X2og?pwd=qcy8)
	- SNAKE / CLOSER / JAN CIAs 0.35.0 欧版 [提取码：zn1d](https://cloud.189.cn/t/rArm6vaA3Mri) / [备用链接：5d7u](https://pan.baidu.com/s/1Lr_ILQkpCZJwQf0i05WcgA?pwd=5d7u)
	- SNAKE / CLOSER / JAN CIAs 0.35.0 韩版 [提取码：zcv3](https://cloud.189.cn/t/6NvIZvjQRZfm) / [备用链接：6xrq](https://pan.baidu.com/s/1_lGcCCDbKqop3bYC1iV8lg?pwd=6xrq)
	- 
	- CTR / SPR / FTR CIAs 0.35.0 日版 [​提取码：0tdb](http://cloud.189.cn/t/6FreeyzeiUNr) / [​备用链接：b72c](https://pan.baidu.com/s/1rDeHT2oKXXgxKocuY-5GzA?pwd=b72c)
	- CTR / SPR / FTR CIAs 0.35.0 美版 [​提取码：jk4x](http://cloud.189.cn/t/aeIRZvJV7bMf) / ​[备用链接：ni65](https://pan.baidu.com/s/1FhYcZfkOBWjKjn2rG9veJg?pwd=ni65)
	- CTR / SPR / FTR CIAs 0.35.0 欧版 [​提取码：1r61](https://cloud.189.cn/t/Yz63qeE77jEz) / ​[备用链接：1m7p](https://pan.baidu.com/s/1a4pPgw2bKfWIbZ40PMjEeg?pwd=1m7p)
	- CTR / SPR / FTR CIAs 0.35.0 韩版 [​提取码：2dkb](https://cloud.189.cn/t/aYnMzmzaAbai) / ​[备用链接：bins](https://pan.baidu.com/s/1L2GK29IJ25kEde6kHQaBDA?pwd=bins)
	- CTR / SPR / FTR CIAs 0.35.0 港台版 [​提取码：pj33](https://cloud.189.cn/t/6j2uQfBV3Yfm) / ​[备用链接：hgei](https://pan.baidu.com/s/1EnfPeEqvTBuG0ZNlSNnAzw?pwd=hgei)
	- CTR / SPR / FTR CIAs 0.35.0 神游版 [​提取码：8uxh](https://cloud.189.cn/t/3I3ANrBBf2mq) / ​[备用链接：373j](https://pan.baidu.com/s/1sX0Y1qgS3NA0zWiCz5Xb1w?pwd=373j)

### 步骤
- 1 将压缩档内的"SystemUpdater_[机型]-0_35_0-[区域]_cias"文件夹解压至机器的储存卡里
- 2 将储存卡重新插入机器内
- 3 运行"Dev Menu" 在"SDMC"选项卡里找到"SystemUpdater_[机型]-0_35_0-[区域]_cias"文件夹并打开它
- 4 按下L+R+A组合键自动安装所有的CIA文件
- 5 找到对应自己机型的NATIVE_FIRM CIA文件：
	- CTR / SPR / FTR 机型，用十字键选中"0004013800000002.cia"文件。
	- SNAKE / CLOSER / JAN 机型，用十字键选中"0004013820000002.cia"文件。
- 6 按下Start + Y组合键，然后按A确定，以更新NATIVE_FIRM。
- 7 按住电源键将主机关机

## 三部分 - 安装自制软件
- 1 将机器开机，运行"Dev Menu"。
- 2 在"SDMC"选项卡里找到"cias"文件夹并打开它。
- 3 按下L+R+A组合键自动安装所有的CIA文件
- 4 关闭"Dev Menu"，然后将机器关机。

## 四部分 - 破解固化
- 1 按住机器的"Start"键开机，选择"GodMode9_dev"。
	 - 如果"GodMode9"提示你需要备份重要数据，按"A"执行此操作，片刻后按"A"继续，
- 2 按"HOME"键打开主菜单
- 3 依次选择"Scripts"→"GM9Megascript"→"Scripts from Plailect's Guide"→"Setup Luma3DS to CTRNAND"
- 4 出现提示时按"A"
- 5 再次按"A"，然后依次输入下屏给出的组合键以解锁LV1 SysNAND写入权限。
- 6 按"A"继续，然后再次按"A"关闭写入权限。

## 五部分 - 备份内部存储(NAND)数据
- 1 按住START键，然后按下开机键，片刻后会进入GodMode9；
	- 如果进入的是"Luma3DS chainloader"菜单，使用十字键手动选择"GodMode9_dev"，然后按"A"运行；
		- 如果"GodMode9"提示你需要备份重要数据，按"A"执行此操作，片刻后按"A"继续。
		- 如果"GodMode9"提示RTC错误，按"A"修改机器时间，也可以按"B"暂时跳过。
- 2 按下"HOME"键以开启位于下屏的功能菜单；
- 3 选择"Scripts..."；
- 4 选择"NANDManager"；
- 5 按"X"，然后按"A"，以备份SysNAND；
- 6 待进度条跑完后，按"A"确认，然后按十字键"↑"，再次按"A"回到主菜单；
- 7 打开"[S:] SYSNAND VIRTUAL"分区；
- 8 用十字键选定文件"essential.exefs"；
- 9 按"A"呼出文件菜单；
- 10 十字键选择"Copy to 0:/gm9/out"，然后按"A"复制；
	-  如果下屏出现"Destination already exists"，用十字键选择"Overwrite file(s)"，然后按"A"覆盖。
- 11 再次按"A"以继续；
- 12 按住"R"，然后按下"START"以将机器关机；
- 13 将机器的储存卡插入电脑中；
- 14 在电脑中打开储存卡的"/gm9/out/"文件夹；
- 15 将以下文件复制出来：
~~~
[日期]_[序列号]_sysnand_[次数].bin
[日期]_[序列号]_sysnand_[次数].bin.sha
essential.exefs
~~~
- 16 将这些文件进行多重备份，例如自己的硬盘或是网盘里。
	-  如果后期自己机器的系统出现问题，可使用这些备份数据来恢复。
	-  以上工作都完成后，将储存卡重新插入机器，储存卡里的备份数据也可以移除。

**至此，3DS开发机已完成破解。**

## 感谢：
- heiyu04
- d0k3
- toiry921
- shijimasoft
- 3DSGuy
- jakcron
- ihaveamac
- soarqin
- rohithvishaal
- R-YaTian
- zoogie
- LumaTeam
- MrNbaYoh
- TuxSH
- nedwill
- hacks.guide
- 博van小哥哥
- 其他为3DS编写自制软件以及参与测试的人们
