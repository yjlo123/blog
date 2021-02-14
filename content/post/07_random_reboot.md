---
title: "装机问题总结"
date: 2021-01-15T00:00:00+08:00
draft: false
tags: ["pc"]
---

满怀期待地配了一台台式机，却要经受电脑各种各种的问题。这次装机也让我认识到了硬件的不可靠。

总结一下遇到的闹心问题：
1. Cooler Master的电源（Cooler Master Gold 550 Full Modular）风扇做工极差。开启和关闭时会发出类似风扇被卡到的噪音。（闹心指数：**）
2. Asus主板（ASUS TUF Gaming B550M-PLUS）有很严重的兼容性问题，导致装好的电脑随机断电重启。（闹心指数：*****）
3. Zotac显卡（ZOTAC Gaming GTX 1660 Super）闪屏问题。每隔几分钟屏幕的上半部分就会闪烁一下。（闹心指数：****）

下面详细介绍下每个问题

---
### 电源问题（风扇噪音）
装机前还很看好全模组（Full Modular）的电源，感觉是个很让处女座舒心的设计。然而装机后却觉得全模组对于我是没必要的。因为电源一定是要有两个线分别给主板和CPU供电，而且我也没有定制机箱内电源线的需求。

但这也不是重点。严重的问题是买的这个Cooler Master的电源风扇在启动和断电时有很明显的噪音。

找售后换了一个全新的后，在关机时风扇仍有很明显的停转噪音，但算是在一个能忍的范围了。

---
### 主板问题（自动重启）
千挑万选的主板，却给我带来了最大的麻烦。从装好机的第一天开始，电脑就会在轻工作量的时候突然断电重启，在运行大型游戏或者软件时反倒没有重启过。寻找问题的四个多月几乎让人生无可恋。

重启几乎毫无规律，有时一天重启多次，有时却能够保持一天不出问题。这也导致了每次验证尝试解决问题的周期很长。

#### - 怀疑软件的问题
Google搜索一下random reboot问题，大量的视频和文章介绍怎么更改Windows的某些系统设置或者关闭屏幕保护来解决，然而这些方法一点作用没有。

然后我卸载掉了一系列软件和驱动，包括AutoHotkey，CPU chipset驱动，Ryzen Master，Nvidia显卡驱动等等，每次都要待机个一两天来验证，但是每次都以失败和沮丧告终。

我也曾想要重装Windows系统或者安装Ubuntu系统，但是因为重装系统很麻烦而且也觉得不太可能是系统的问题，也就没有尝试。

#### - 怀疑机箱部件没插好
把CPU风扇，内存，电源，显卡和机箱按钮的连线全都重新插了一遍，折腾一番后，问题依旧。

#### - 怀疑电压不稳
电脑突然断电重启是在我小的时候偶尔遇到过的，那时家乡的电压很不稳定，每次伴随着电灯忽暗忽明，电脑就跟着重启。而我能做的只有换个插线板和电源插座来排除一下是连接的问题。

#### - 怀疑电源的问题
在Windows的Event Viewer里可以查看每次重启的系统日志。每次重启的记录里都标记着：
> Event ID 41
> The system has rebooted without cleanly shutting down first. This error could be caused if the system stopped responding, crashed, or lost power unexpectedly.

相应的Details里所有EventData都是0，根据Windows的文档
https://docs.microsoft.com/en-us/windows/client-management/troubleshoot-event-id-41-restart#scen3，是系统突然断电重启时根本来不及记录任何参数。

这就让我不得不怀疑是电源的问题，加上电源启动和断电时的风扇噪音，越想越觉得这个很可能是断电的原因。找售后换了新的电源后，神奇般地一周没有再重启。

本以为找到了问题所在，然后就在一周后，再一次的突然重启让我又开始怀疑人生。

#### - 最终：BIOS
在Asus的论坛上的一个用户描述了和我很类似的问题

https://rog.asus.com/forum/showthread.php?119670-B550-Semi-random-hard-reboots-with-DOCP-enabled-Don-t-know-what-to-else-to-try

这个帖子的讨论最终止于BIOS更新，这让我又看到新的光明，马上去Asus官网下载刷BIOS的工具和最新的BIOS稳定版本。同时也发现在最近一年里，Asus给这版主板更新了十余次，并且多次改善系统稳定性和硬件兼容性。

Asus提供了EZ Update工具，可以方便地刷BIOS。
https://www.asus.com/support/FAQ/1012152/

即使官方工具仍在推荐使用`Version 0603 2020/06/11`的BIOS版本，我刷到了`Version 1401 2020/12/08`.

从此电脑就不再随机重启，终于。

---
### 显卡问题（屏幕闪烁）
装机的烦恼并没结束，最后一个明显的问题仍然让人头痛，屏幕的上半部分会随机地闪烁一下。

把显卡拿到售后服务中心，在他们的电脑上也复现了一样的问题，于是他们给了我一个临时的1650 Super用来等新的货。在用1650 Super时并没有遇到类似闪烁的问题，然而拿到新的1660 Super后，问题依旧。难道这个型号都有问题？或者我倒霉地拿到了两个次品？

（To be continued）
