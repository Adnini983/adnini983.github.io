---
title: "安装 boot9strap（MEST9 CLI）"
date: 2026-10-02 00:20:00 +0800
categories: [3DS, 破解指南]
tags: [3DS, 开发机, boot9strap, MEST9]
author: adnini983
media_subpath: /assets/img/posts/3ds-devkit-guide/
permalink: /posts/install-boot9strap-mest9-cli/
toc: true
pin: false
---

## 兼容性注意：
此方法需要一台搭载Windows/Linux/MacOS操作系统的电脑，它们可以是任何种类的CPU架构。如果你没有电脑，可以寻找公用电脑来操作，也可以退回本指南首章，以选择其它的方案。

## 你需要准备：
- 最新版本的[MSET9-devkit](https://github.com/Adnini983/MSET9-devkit/releases/download/2.0_dev/mset9-V2.0_dev.zip)
- 任意版本的[Python 3.x 运行库](https://www.python.org/downloads/)
	- 如果你使用的是Linux或MacOS操作系统，你可能已经拥有了Python运行库。打开终端窗口，并输入命令"python3 -V"。如果终端能够返回Python的版本号，则可以继续使用本文方法。
### 提示：
在本文中，你将运行用于触发MEST9漏洞的脚本。在操作过程中，用户数据将会暂时消失，不过本文结尾会指导你恢复原先的数据。如果你在运行脚本时弹出了错误，请添加QQ群聊以联系本指南的作者：[1076530032](https://qm.qq.com/q/W6Pp7jzd6u)。

## 一部分 - 准备工作
在本节中，你将准备触发MEST9漏洞的所需数据，方法是临时建立一个不包含任何用户数据的主菜单配置文件，然后修改其配置文件，其中将会包含触发MEST9漏洞的部分。你原本的用户数据将会暂时消失，但当你做完本文的所有步骤后，这些数据将会恢复。

- 1 将机器关机
- 2 将机器的储存卡插入电脑中
- 3 将"mset9-V2.0_dev"压缩档内的所有文件解压至储存卡根目录内(如有提示则选择"覆盖")
- 4 将储存卡根目录的"Nintendo 3DS"文件夹改名为"Nintendo 3DS_backup"
- 5 将储存卡插回机器
- 6 将机器开机
- 7 待主菜单加载完成后，将机器关机
- 8 将机器的储存卡插入电脑中
- 9 根据你电脑的操作系统，运行MEST9脚本。
	-  Windows：双击运行"MSET9-Windows.bat"
	-  MacOS：运行"MSET9-macOS.command" 如果出现提示，请输入你的登陆密码。
	-  Linux：打开终端窗口，先用"cd"命令进入你的储存卡根目录，然后键入"python3 mset9.py"命令并回车。
- 10 在键盘上输入与你机器型号和系统SDK版本号对应的数字，然后按Enter键继续。
- 11 在键盘上输入数字"1"，然后按Enter建。
- 12 查看免责声明后，再次输入数字"1"并按Enter建。
- 13 如果看到消息"Created hacked ID1."，请按Enter键并关闭MEST9脚本。
- 14 将储存卡插回机器内
- 15 将机器开机
- 16 在机器内运行"Mii Maker"
- 17 等待机器显示"[欢迎来到Mii Maker](res/mii-welcome.png)"窗口，然后退出Mii Maker并返回主菜单。
	-  你会看到此[画面](res/mii-extdata.png)，这代表着正在创建所需数据。
	-  如果看到的只是[Mii Maker的菜单](res/mii-existing.png)，则代表数据已经存在，退出Mii Maker并返回主菜单。
- 18 运行系统设置(System Settings)，依次选择"数据管理(Data Management)"→"任天堂3DS(Nintendo 3DS)"→"软件(Software)"，然后点击"重置(Reset)"([图片步骤](res/database-reset.jpg))。
	- 这不会清空你的任何数据
- 19 按住电源键，然后点击下屏的"Power Off"以将机器关机。
- 20 将机器的储存卡插入电脑中
- 21 运行MEST9脚本
- 22 在键盘上输入与你机器型号和系统SDK版本号对应的数字，然后按Enter键继续。
- 23 如果上述的步骤全部正常执行，你可以看到窗口出现绿色的"Ready"字样。
	-  如果窗口显示的是黄色的"Not ready - check MSET9 status for more details"字样，输入数字"2"，并按照窗口给出的指示来操作。
	-  问题解决后，返回步骤"20."
- 24 在键盘上输入数字"0"回车，以关闭当前窗口。
- 25 将储存卡重新插入机器

## 二部分 - 触发漏洞
在本节中，你将触发MEST9漏洞以执行 boot9strap 安装程序。

**重点：必须严格执行以下的步骤，请再三确认你的每一个操作都是正确的，以防止机器出现意料之外的错误。**

- 1 将主机开机，确保光标已选定"系统设置(System Settings)"
	- 如果开机后光标没有自动选定"系统设置(System Settings)"，请使用十字键或摇杆重新选中它，然后将主机关机，并重新开机。
- 2 按"A"键启动"系统设置(System Settings)"
- 3 依次选择"数据管理(Data Management)"→"任天堂3DS(Nintendo 3DS)"→"额外数据(Extra Data)"
- 4 在此期间，**请勿按下任何按钮或触摸屏幕。**
- 5 在机器仍处于"步骤4"的状态下，直接拔出机器的储存卡(此时机器会自动刷新并显示未插入储存卡)。
- 6 将机器的储存卡插入电脑中
- 7 运行MEST9脚本
- 8 在键盘上输入与你机器型号和系统SDK版本号对应的数字，然后按Enter键继续。
- 9 在MEST9脚本窗口中，输入"3"并回车，以注入MEST9触发数据。
- 10 按"Enter"键关闭MEST9脚本
- 11 将储存卡重新插入机器，**不要按下任何按键或触摸屏幕。**
- 12 片刻后，机器将会自动启动 SafeB9SInstaller。

## 三部分 - 安装 boot9strap
在本节中，你将在机器中安装自制固件。

- 1 依次输入上屏显示的组合键来安装boot9strap
- 2 完成后，按"A"键重启你的机器。
- 3 你的机器应该已经自动进入到Luma3DS的配置菜单了。在本指南中，暂时不要改动这些选项，保持默认即可。
- 4 按"Start"键保存设置并重启

## 四部分 - 移除MEST9
在本节中，你将移除MEST9漏洞的触发数据，以防止系统出现更多不可预料的BUG，同时将会恢复你原先的用户数据。

**重要：不要跳过本节！如果跳过它，其它的游戏软件可能无法正常运行，且无法进行"完成破解"部分的操作。**
- 1 将机器关机
- 2 将机器的储存卡插入电脑中
- 3 运行MEST9脚本
- 4 在键盘上输入与你机器型号和系统SDK版本号对应的数字，然后按Enter键继续。
	- 当前窗口应该会显示Injected
	- 如果你已经删除了相关文件(或从一开始就未注入)，则当前状态将显示"Ready"，请跳至第6步。
- 5 输入数字"5"，然后按Enter键以删除漏洞数据。
	-  执行完毕后，你应该会看到"Removed trigger file"文本。
- 6 输入数字"5"，然后按Enter键以删除所有MEST9相关的数据。
	- 你应该会看到"Successfully removed MSET9!"
- 7 移除储存卡根目录内的"Nintendo 3DS"文件夹
- 8 将"Nintendo 3DS_backup"文件夹改名为"Nintendo 3DS"
- 9 将储存卡重新插入机器

此时，你的机器将默认启动至Luma3DS。在下一章中，你将会开始执行完成破解的收尾工作。

**重要：你是否执行了"四部分(移除MEST9)"中的所有步骤？此部分是不可以跳过的！**

**继续至[完成破解](/posts/finalizing-setup/)**
