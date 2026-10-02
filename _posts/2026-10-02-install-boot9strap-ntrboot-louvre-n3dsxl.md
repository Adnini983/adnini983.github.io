---
title: "安装 boot9strap（ntrboot，仅限 Louvre New 3DS XL）"
date: 2026-10-02 00:50:00 +0800
categories: [3DS, 破解指南]
tags: [3DS, Louvre New 3DS XL, ntrboot, boot9strap]
author: adnini983
media_subpath: /assets/img/posts/3ds-devkit-guide/
permalink: /posts/install-boot9strap-ntrboot-louvre-n3dsxl/
toc: true
pin: false
---

## 在本文中：
- 使用ntrboot运行GodMode9
- 备份机器原始NAND数据
- 安装boot9strap
- 更新SDK版本至 0.35.0

## 你需要准备：
- 触发机器睡眠模式用的磁铁
- 在上文中写入了ntrboot固件的烧录卡
- 最新版本的 [GodMode9](https://github.com/d0k3/GodMode9/releases/latest)
- 最新版本的 [SafeB9SInstaller](https://github.com/d0k3/SafeB9SInstaller/releases/download/v0.0.7/SafeB9SInstaller-20170605-122940.zip)
- 最新版本的 [boot9strap Devkit](https://github.com/SciresM/boot9strap/releases/download/1.4/boot9strap-1.4-devkit.zip)
- 最新版本的 [Luma3DS](https://github.com/LumaTeam/Luma3DS/releases/latest)(下载".zip"文件)
- SNAKE / CLOSER / JAN CIAs 0.35.0 欧版 [提取码：zn1d](https://cloud.189.cn/t/rArm6vaA3Mri) / [备用链接：5d7u](https://pan.baidu.com/s/1Lr_ILQkpCZJwQf0i05WcgA?pwd=5d7u)

## 步骤
### 一部分 - 准备工作
- 1 关闭你的机器
- 2 将机器的microSD卡插入电脑(不是烧录卡的)
- 3 将"Luma3DS***.zip"压缩档内的"boot.3dsx"和"boot.firm"文件解压至储存卡根目录
- 4 将"boot.firm"更名为"boot1.firm"
- 5 将"GodMode9-v***-**********.zip"压缩档内的"GodMode9_dev.firm"文件解压至microSD卡根目录
- 6 将"GodMode9_dev.firm"更名为"boot.firm"
- 7 将"GodMode9-v***-**********.zip"压缩档内的"gm9"文件夹解压至储存卡根目录内
- 8 新建一个名为"boot9strap"的文件夹
- 9 将"boot9strap-1.4-devkit.zip"压缩档内的所有文件解压至储存卡内的"/boot9strap/"文件夹
- 10 将"SafeB9SInstaller-20170605-122940.zip"压缩档内的"SafeB9SInstaller.firm"文件解压至储存卡根目录
- 11 将"SystemUpdater_SNAKE-0_35_0-EU_cias.rar"压缩档内的"SystemUpdater_SNAKE-0_35_0-EU_cias"文件夹解压至储存卡根目录
- 12 将储存卡插回机器内，**暂时不要装回电池后盖。**
- 13 将主机开机

### 二部分 - 触发ntrboot
- 1 使用磁铁找出机器的睡眠传感器的位置
- 2 将机器关机
- 3 将烧录卡插入机器
- 4 将磁铁放在睡眠传感器的位置上或右侧
- 5 同时按住"Start"+"Select"+"X"+开机键 数秒，这可能需要多试几次。
- 6 如果后门触发成功，你将会看到 "GodMode9"。

### 三部分 - 备份原始NAND数据
- 1 按下"HOME"键以开启位于下屏的功能菜单
- 2 选择"Scripts..."
- 3 选择"NANDManager"
- 4 按"X"，然后按"A"，以备份SysNAND。
- 5 待进度条跑完后，按"A"确认，然后按十字键"↑"，再次按"A"回到主菜单。
- 6 打开"[S:] SYSNAND VIRTUAL"分区
- 7 用十字键选定文件"essential.exefs"
- 8 按"A"打开文件菜单
- 9 十字键选择"Copy to 0:/gm9/out"，然后按"A"复制。
	-  如果下屏出现"Destination already exists"，用十字键选择"Overwrite file(s)"，然后按"A"覆盖。
- 10 再次按"A"以继续
- 11 按住"R"，然后按下"B"以卸载microSD卡。
- 12 将机器的储存卡插入电脑中
- 13 在电脑中打开储存卡的"/gm9/out/"文件夹
- 14 将以下文件复制出来：
~~~
[日期]_[序列号]_sysnand_[次数].bin
[日期]_[序列号]_sysnand_[次数].bin.sha
essential.exefs
~~~
- 15 将这些文件进行多重备份，例如自己的硬盘或是网盘里。
	-  如果后期自己机器的系统出现问题，可使用这些备份数据来恢复。
	-  以上工作都完成后，将储存卡重新插入机器，储存卡里的备份数据也可以移除。
- 16 将储存卡插回机器内，**这时可以将电池后盖装回。**

### 四部分 - 安装 boot9strap
- 1 打开储存卡分区"[0:] SDCARD ([FAT卷标])"
- 2 用十字键选中"boot.firm"文件
- 3 按"X"将文件删除，**在此期间不要将机器关机。**
- 4 用十字键选中"boot1.firm"文件
- 5 按住"R"，然后按下"X"以开始给文件更名。
- 6 在下屏中将"boot1.firm"更名为"boot.firm"
- 7 用十字键选中"SafeB9SInstaller.firm"文件
- 8 按"A"打开文件菜单
- 9 依次选择"FIRM image options..."→"Boot FIRM"，出现提示后再次按"A"。
	- 如果一切正常，机器将会启动"SafeB9SInstaller"
- 10 依次输入上屏显示的组合键来安装boot9strap
- 11 完成后，按下"A"以重启机器。
	- 你的机器应该已经自动进入到Luma3DS的配置菜单了。在本指南中，暂时不要改动这些选项，保持默认即可。
- 12 按"Start"键保存设置并重启
- 13 重启完成后，按住电源键以关闭机器。

### 五部分 - 升级至 0.35.0
- 1 按照"[运行Dev Menu (Louvre New 3DS XL)](/posts/launch-devmenu-louvre-n3dsxl/)"的方法运行"Dev Menu"
- 2 在"SDMC"选项卡里找到"SystemUpdater_SNAKE-0_35_0-EU_cias"文件夹并打开它
- 3 按下L+R+A组合键自动安装所有的CIA文件
- 4 用十字键选中 CIA文件"0004013820000002.cia"
- 5 按下Start + Y组合键，然后按A确定，以更新NATIVE_FIRM。
- 6 按住电源键，将机器关机。

**继续至[完成破解](/posts/finalizing-setup/)**
