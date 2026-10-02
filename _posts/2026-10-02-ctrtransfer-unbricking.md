---
title: "CTRTransfer（救砖）"
date: 2026-10-02 01:00:00 +0800
categories: [3DS, 破解指南]
tags: [3DS, 开发机, CTRTransfer, 救砖]
author: adnini983
media_subpath: /assets/img/posts/3ds-devkit-guide/
permalink: /posts/ctrtransfer-unbricking/
toc: true
pin: false
---

## 兼容性注意：
**本文暂不支持"New 3DS"系列开发机机型。如果你的开发机是属于SNAKE/CLOSER/JAN系列中的任何一种，请阅读CTR SystemUpdater (CTR-008)，或寻求其它的方法。**

## 在本文中：
- 备份原始NAND数据的同时，写入预制的CTRTransfer镜像，以代替本身已损坏的原始系统。

## 你需要准备：
- 最新版本的 [GodMode9](https://github.com/d0k3/GodMode9/releases/latest)
- 最新版本的 [faketik](https://github.com/ihaveamac/faketik/releases/download/v1.1.2/faketik.3dsx)
- 0.33.0 CTRTransfer镜像，尽量选择与你自己机型相同的区域；
- 如果你不知道或无法确定机器是哪一种区域，挑一个就对了：
	- CTR / SPR / FTR CTRTransfer 0.33.0 日版 [提取码：0ce0](https://cloud.189.cn/web/share?code=2IryemvUNFV3) / [备用链接：wgrc](https://pan.baidu.com/s/1ebRUXNlREdmbDCn2TIwCgQ?pwd=wgrc)
	- CTR / SPR / FTR CTRTransfer 0.33.0 美版 [提取码：3bqh](https://cloud.189.cn/web/share?code=JZBRnaNrieiy) / [备用链接：gmuq](https://pan.baidu.com/s/1h_lKurfCD8cuZMzxNwcX1Q?pwd=gmuq)
	- CTR / SPR / FTR CTRTransfer 0.33.0 欧版 [提取码：oa4b](https://cloud.189.cn/web/share?code=MfeUJfARvQja) / [备用链接：1x64](https://pan.baidu.com/s/1duqo-ZRJPO8UwQmPswQ-4w?pwd=1x64)
	- CTR / SPR / FTR CTRTransfer 0.33.0 韩版 [提取码：8idg](https://cloud.189.cn/web/share?code=a6BnIjNzIfeq) / [备用链接：fjuy](https://pan.baidu.com/s/1scTtCsERxey1gEoXCdoH3w?pwd=fjuy)
	- CTR / SPR / FTR CTRTransfer 0.33.0 港台版 [提取码：gkw2](https://cloud.189.cn/web/share?code=iMbeUzMRBFJf) / [备用链接：h63u](https://pan.baidu.com/s/1V_AdI3RNF0w3-jSUMTgHNQ?pwd=h63u)
	- CTR / SPR / FTR CTRTransfer 0.33.0 神游版 [提取码：5kic](https://cloud.189.cn/web/share?code=2u2Ezu67Jb6n) / [备用链接：2w14](https://pan.baidu.com/s/1pjEJU33_w_JyD06_Ppc54w?pwd=2w14)

## 步骤
### 一部分 - 准备工作
- 1 将机器关机
- 2 将机器的储存卡插入电脑中
- 3 在储存卡的根目录建立一个叫"3ds"的文件夹(如果没有)
- 4 复制"faketik.3dsx"到储存卡的"\3ds\"文件夹内
- 5 在储存卡的根目录建立一个叫"luma"的文件夹，然后在"luma"文件夹里再建立一个叫"payloads"的文件夹(如果没有)。
- 6 将"GodMode9-****-***********.zip"压缩档内的"GodMode9_dev.firm"文件解压至储存卡的"\luma\payloads\"文件夹内
- 7 将"GodMode9-****-***********.zip"压缩档内的"gm9"文件夹解压至储存卡根目录内
- 8 在储存卡的"\gm9\"文件夹内建立一个叫"in"的文件夹(如果没有)
- 9 将"[机型]_0.33.0_[区域]_ctrtransfer.rar"压缩档内的".bin"和".bin.sha"文件解压至储存卡的"\gm9\in\"文件夹内
- 10 将储存卡重新插回机器内
	- 此时的目录结构应为：
~~~
储存卡
├─ boot.3dsx // Homebrew Launcher
├─ boot.firm // Luma3DS
├─ Nintendo 3DS
│  └─ [ID0]
│     └─ [ID1]
│        └─ ...... // 略
├─ luma
│  └─ payload
│     └─ GodMode9_dev.firm // GodMode9 开发版本体
├─ gm9
│  ├─ support
│  │  ├─ decTitleKeys.bin.here // 占位文件
│  │  └─ seeddb.bin.here // 占位文件
│  ├─ scripts
│  │  ├─ GM9Megascript.gm9 // 扩展功能合集
│  │  └─ NANDManager.gm9 // NAND备份还原
│  ├─ languages // 新版本加入的多语言翻译字库
│  │  ├─ de.trf
│  │  ├─ en.trf
│  │  ├─ ...... // 仅列出部分文件
│  │  ├─ zh-CN.frf
│  │  ├─ zh-CN.trf
│  │  ├─ zh-TW.frf
│  │  └─ zh-TW.trf
│  └─ in // CTRTransfer镜像在这里
│     ├─ [机型]_0.33.0_[区域]_ctrtransfer.bin
│     └─ [机型]_0.33.0_[区域]_ctrtransfer.bin.sha
├─ config
│  └─ ssl
│     └─ cacert.pem // Luma3DS CA证书库
└─ 3ds // .3dsx格式自制程序目录
   └─ faketik.3dsx
~~~
### 二部分 - 备份原始NAND数据
- 1 按住START键，然后按下开机键，片刻后会进入GodMode9。
	- 如果进入的是"Luma3DS chainloader"菜单，使用十字键手动选择"GodMode9_dev"，然后按"A"运行。
		-  如果"GodMode9"提示你需要备份重要数据，按"A"执行此操作，片刻后按"A"继续。
		-  如果"GodMode9"提示RTC错误，按"A"修改机器时间，也可以按"B"暂时跳过。
- 2 按下"HOME"键以开启位于下屏的功能菜单
- 3 选择"Scripts..."
- 4 选择"NANDManager"
- 5 按"X"，然后按"A"，以备份SysNAND。
- 6 待进度条跑完后，按"A"确认，然后按十字键"↑"，再次按"A"回到主菜单。
- 7 打开"[S:] SYSNAND VIRTUAL"分区
- 8 用十字键选定文件"essential.exefs"
- 9 按"A"打开文件菜单
- 10 十字键选择"Copy to 0:/gm9/out"，然后按"A"复制。
	-  如果下屏出现"Destination already exists"，用十字键选择"Overwrite file(s)"，然后按"A"覆盖。
- 11 再次按"A"以继续
- 12 按住"R"，然后按下"START"以将机器关机。
- 13 将机器的储存卡插入电脑中
- 14 在电脑中打开储存卡的"/gm9/out/"文件夹
- 15 将以下文件复制出来：
~~~
[日期]_[序列号]_sysnand_[次数].bin
[日期]_[序列号]_sysnand_[次数].bin.sha
essential.exefs
~~~
- 16 将这些文件进行多重备份，例如自己的硬盘或是网盘里。
	-  如果后期自己机器的系统出现问题，可使用这些备份数据来恢复。
	-  以上工作都完成后，将储存卡重新插入机器，储存卡里的备份数据也可以移除。

### 三部分 - 写入CTRTransfer镜像
- 1 按住START键，然后按下开机键，片刻后会进入GodMode9。
	-  如果进入的是"Luma3DS chainloader"菜单，使用十字键手动选择"GodMode9_dev"，然后按"A"运行。
- 2 打开"[0:] SDCARD ([FAT卷标])"储存卡分区
- 3 打开"\gm9\in\"文件夹
- 4 用十字键选定CTRTransfer镜像"[机型]_0.33.0_[区域]_ctrtransfer.bin"
- 5 按"A"以呼出文件菜单
- 6 选择"Calculate SHA-256"
- 7 待进度条跑完后，如果文件未损坏，会显示"passed"，之后按"B"返回。
	-  如果显示的是"failed"，说明文件可能已损坏，请重新复制一遍镜像，或者更换你的储存卡。
- 8 再次按十字键选中"[机型]_0.33.0_[区域]_ctrtransfer.bin"，然后按"A"呼出文件菜单。
- 9 依次选择"CTRNAND options..."→"Transfer image to CTRNAND"→"Transfer to SysNAND"
- 10 再次按"A"，然后依次输入下屏给出的组合键以解锁LV1 SysNAND写入权限。
- 11 按"A"继续，然后再次按"A"关闭写入权限。
- 12 按"B"返回主界面
- 13 用十字键选中"[1:] SYSNAND CTRNAND"，按"R"+"A"键。
- 14 选择"Fix CMACs for drive"
- 15 再次按"A"，然后依次输入下屏给出的组合键以解锁LV1 SysNAND写入权限。
- 16 期间会提示解锁LV2 SysNAND写入权限，一律按"A"键，然后依次输入下屏给出的组合键。
- 17 出现提示后按"A"，然后再次按"A"关闭写入权限。
- 18 按"START"键重启机器，然后等待机器启动"Test Menu"。
- 19 按"START"键启动"Dev Menu"
- 20 在下屏的"Program"选项卡里找到"Config"
- 21 按"A"或使用触控笔轻触"Config"
- 22 再次按"A"或使用触控笔轻触"Launch (A)"以启动"Config"
- 23 使用十字键选定上屏的"Menu Setting"，然后按"A"。
- 24 使用十字键选定下屏的"Menu"，然后按"A"。
- 25 使用十字键"↑"或"↓"选定"test menu"，然后按"B"两次。
- 26 轻按电源键以重启机器
- 27 重复步骤19-24
- 28 使用十字键"↑"或"↓"选定"home menu"，然后按"B"两次。
- 29 轻按电源键以重启机器，此时机器会启动主菜单。

### 四部分 - 恢复所有已安装应用
**提示：如果你本来就没有安装任何应用，或者机器从未预装有任何应用，此步骤可以跳过**
- 1 在主菜单启动"Download Play"
- 2 当看到3DS和DS Logo的两个大按钮后，按下"L"+"十字键↓"+"SELECT"。
- 3 十字键选择"Miscellaneous options..."，然后按"A"。
- 4 十字键选择"Switch the hb. title to the current app."，然后按"A"。
- 5 出现提示后，按"B"三次，然后按"HOME"键，再按"X"关闭"Download Play"。
- 6 再次在主菜单启动"Download Play"，这时会进入"Homebrew Launcher"。
- 7 在下屏中用十字键或摇杆选定"faketik"，然后按"A"以运行。
- 8 等待代码全部跑完后，按"B"返回"Homebrew Launcher"。
- 9 按"HOME"键，再按"X"关闭"Download Play"。

### 五部分 - 修复跨区相关的问题
#### 提示：
- 如果你写入的CTRTransfer镜像的区域与机器的原始区域不一致，或者你不知道是不是写入了不同区域的CTRTransfer镜像，那就不要跳过这个步骤，这个部分用于解决部分机型无法进入Model3模式问题，以及无法启动迷你应用的问题；
- 这个部分会重置掉你的所有Mii角色数据，如果你需要保留它们，可以按照这个教程[保存每一个Mii角色的QR码](https://en-americas-support.nintendo.com/app/answers/detail/a_id/298/~/how-to-generate-a-qr-code%E2%84%A2-for-a-mii)，也可以手动使用GodMode9备份"**[1:] SYSNAND CTRNAND:/data/[ID0]/extdata/00048000/f000000b/**"文件夹里的所有文件，待此部分完成后，你可以再将这个文件夹复制回原来的位置。

#### 步骤：
- 1 将机器关机
- 2 按住START键，然后按下开机键，片刻后会进入GodMode9。
	-  如果进入的是"Luma3DS chainloader"菜单，使用十字键手动选择"GodMode9_dev"，然后按"A"运行。
- 3 打开文件夹"[1:] SYSNAND CTRNAND"→"data"→"[ID0]"→"sysdata"
	-  [ID0]是一个名字为32字节长度的非固定名字文件夹。
- 4 使用十字键选定文件夹"00010017"
- 5 按下"R"+"A"呼出下屏的文件夹菜单
- 6 用十字键选择"Copy to 0:/gm9/out"，然后按"A"。
- 7 保持选定文件夹"00010017"，然后按"X"删除。
- 8 按"A"确认删除
- 9 再次按"A"，然后输入下屏给出的组合键以解锁"SysNAND (lvl1)"写入权限。
- 10 再次按"A"以关闭写入权限
- 11 按下"START"以重启机器
- 12 机器会引导至开箱配置环节
	-  这部分是预期行为，你原本的游戏存档等数据均不会丢失。
- 13 按照机器上的指示完成所有配置项目。

**继续至[完成破解](/posts/finalizing-setup/)**
