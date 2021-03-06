---
layout:     post   				    # 使用的布局（不需要改）
title:      捋一捋2019捡的垃圾：华硕H110S1+QL2X+黑苹果(OC+Catalina) # 标题 
subtitle:   Hackintosh for Asus-H110s1, QL2X, DW1820A, using Opencore and Support macOS Catalina   #副标题
date:       2020-01-27 				# 时间
author:     Road 						# 作者
header-img: img/Asus-H110s1.jpeg	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - 装机
    - 迷你主机
    - STX
    - QL2X
    - Opencore
    - Hackintosh
---

## BB两句

19年底几位大佬掀起了一波1L小主机的热潮，作为一名沉迷捡垃圾多年的垃圾佬，再加上不爱打游戏，喜欢小主机多年，这股热潮自然也是不会错过的。19年捡了不少二手硬件：HP 800 G1 DM，华硕H110t，精英H110S2p，还有今天的主角——华硕H110S1。过年宅在家不能出门，也正好捋一捋自己捡的一堆硬件。把机子装起来，写文章记录一下。

下面来讲讲这些硬件的故事：

主板和机箱是逛闲鱼无意刷到的，因为之前虽然也想装stx主机，但是我已经收到了一块精英H110s2p了。但是感觉卖家价格挺合理的，单买机箱也要200了，那算下来主板400。虽然没有很便宜，但是考虑到这类stx主板很小众，也没砍价就直接下单了。

散热器是看卖家的拍的照片，发现用的是这个猫头鹰散热，问他愿不愿意搭车卖，卖家很爽快，加100就好了。愉快下单捋一捋2019捡的垃圾：华硕H110S1+QL2X+黑苹果（OC+Catalina）

内存，玖合，16g单条279很便宜了，虽然大家都知道颗粒的来源。但是内存嘛，又不超频，而且jd自营，便宜大碗，真香。

硬盘，C2000 pro 512g 听闻固态要涨价才赶紧囤的，不是什么好价。后悔没上699 1tr的车。

网卡，D1820A，原价50左右的卡，自从黑果小兵说可以用之后就一直被炒，到现在要80了，js啊捋一捋2019捡的垃圾：华硕H110S1+QL2X+黑苹果（OC+Catalina） 。这张无线卡其实水很深，尤其是笔记本，但是主机平台感觉还好。选这张卡主要是因为便宜，而且如果上拆机卡的话要用转接板，stx主板这种布局我怕会顶到ssd，就没用了。（但是其实我有看到有人是能用了装接板+拆机卡后还能放下ssd的，不清楚，带测试）

电源，卖家附赠的90w电源，虽然说目前用在没什么问题，其实不太够。看说明书90w电源只能带35w的u，而QL2X是45w的u。我怀疑我装系统的时候出现鼠标键盘不灵敏之类的情况很有可能是供电不足。待测试，以后换一个。

CPU，当时选CPU主要是基于一个原则，集显要是630的，感觉跑黑果会比较方便。当时看上了几款：

- 8100，4c4t，45w，价格650左右；

- QL2X，4c8t，45w，价格500；

- QN8J(8700T es)，6c12t，35w，850左右；

8100性价比太低了，QN8J有点超预算，最后就选了QL2X，

其实都怪intel挤牙膏，cpu更新了那么多代，旧的cpu价格一点都没掉，甚至弄到4代u价格也高得不合理。

AMD yes！

## 硬件

|-----------+---------------------------------------+-------------------------------------------|
|         	|                 型号                	|                    备注                 	|
|:---------:|:-------------------------------------:|:----------------------------------------:	|
| 主板      	|            Asus H110s1            	|               (mini STX)               	|
| 处理器   	|                QL2X               	|     (7820HK modify from BGA to LGA)    	|
| 散热器    	|           NOCTUA NH-L9i           	|                                        	|
| 硬盘     	|      Hikvision C2000pro 512gb     	|                                        	|
| 内存      	|     JUHOR 16G DDR4 2666MHz X2     	|                                        	|
| 无线网卡  	|            BCM94350ZAE            	|                (DW1820A)               	|
| 机箱     	|          SilverStone VT02         	|                                        	|
| 电源     	|   55/25mm 19v 120w DC power adapter 	|   Dell 74/50mm 19v 130w DC power adapter 	|
|-----------+---------------------------------------+-------------------------------------------|

## EFI下载地址

跳转至Github  [下载地址](https://github.com/Road-tech/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC)

**使用EFI前请务必修改三码(SSN,UUID,ROM)**    
**Please change three system codes (SSN,UUID,ROM) before using this EFI**  


## macOS完善情况

### 支持：
- 1080p display support one HDMI port (close to DP port)  
- Audio output on HDMI  
- All USB ports  
- Wi-Fi & Bluetooth  
- 3.5mm Audio Output & Mic Input
- Airdrop  
- AirPlay  
- Continuity  

### 不支持:
- Sleep  

### 未测试:
- DP port  
- 4k display  

## BIOS设定：

### Disable/禁用：
- Fast Boot  
- CFG Lock   
- VT-d  
- CSM  
- Intel SGX  

### Enable/启用：
- VT-x  
- Above 4G decoding  
- Hyper Threading  

## 关于QL2X的更多细节

QL2X 是 7820HK 的ES版本CPU， 核显为HD630。 7820HK是个笔记本平台的CPU，大佬通过魔改接口让它可以工作在桌面平台。这很自然会带来一些问题在黑苹果的时候。

首先，7820HK 曾经被用在 Macbook pro 14,3 (15 inch,2017) 平台上。

为了驱动这块 QL2X 的核显，我尝试了3个ig-platform-id：  
- 0x19120000 (skylake平台 核显为HD530  原生驱动3个DP接口)  
- 0x59120000 (kabylake 平台 核显为HD630 原生驱动3个DP接口, 用于iMac18,2)  
- 0x591b0000 (kabylake 平台 核显为HD630 原生驱动 1个LVDS接口 和 2个DP接口, 用于MacBookPro14,3)    

对应了3个结果：

- 0x19120000: 主板上的3个接口 (1 DP, 2 HDMI) 都正常工作，但是**不支持HEVC硬解**
- 0x59120000: 主板上的2个接口 (2 HDMI) 都工作, 可是2个HDMI接口输出都有问题(紫屏)。不过**支持HEVC硬解**
- 0x591b0000: 主板上的1个接口(1 HDMI 靠近DP那个) 工作正常, 剩下那个HDMI接口无输出。**支持HEVC硬解**

**另外很重要的是：**

为了让QL2X可以在桌面平台上使用，我们需要关闭BIOS中的ME。这会导致macOS系统无法在睡眠后唤醒显卡。导致这套系统无法睡眠。

同时，因为 BIOS 中的 ME 被关掉了, 我们需要在 ```boot-arg``` 中添加 ```-disablegfxfirmware``` 

我以后会尝试解决这些问题。

## 更新日志

#### 2020-05-10 更新：

很抱歉这是我最后一次为这个配置更新EFI，因为我已经改用i3-8100. [点击跳转](https://github.com/Road-tech/Hackintosh_Asus-H110s1_I3-8100_DW1820A_OC)        

但是我还是找到了一些解决紫屏的方法，如果你想把 ig-platform-id 设置为```0x59120000```:

1. 尝试用Hackintosh注入显示器
2. 尝试设置强制RBG模式

*参考链接:*

- [MacOS強制外接螢幕輸出RGB](https://blog.driftking.tw/2018/10/MacOS%E5%BC%B7%E5%88%B6%E5%A4%96%E6%8E%A5%E8%9E%A2%E5%B9%95%E8%BC%B8%E5%87%BARGB/)
- [Force RGB mode in Mac OS X to fix the picture quality of an external monitor](https://www.mathewinkson.com/2013/03/force-rgb-mode-in-mac-os-x-to-fix-the-picture-quality-of-an-external-monitor)
- [Dell U2713H on Mac: forcing RGB mode instead of YCbCr](https://embdev.net/topic/284710)

#### 2020-04-17 更新：

- Update LiLu to 1.4.3    
- Update Whatevergreen to 1.3.9     
- Update AppleALC to 1.4.8     
- Update CPUFriend to 1.2.0    
- Update NVMeFix to 1.0.2
- Update VirtualSMC to 1.1.2

---

#### 2020-04-01 更新：

- Already support to Catalina 10.15.4    
- Update Whatevergreen to 1.3.8-DEBUG-t3 (Fix HDMI bug)     
- Update Opencore to 0.5.6     

---

Already supported to Catalina 10.15.3

---

#### 2020-02-20 更新：

- 修复USB3.0接口， 现在USB-C和两个USB3.0速率正常了。

---

#### 2020-02-18 更新：  

- 显卡ID改为 0x193b0005 ｜ MacBookPro13,1 ｜ Intel HD Graphics 530/4K  

	牺牲HEVC硬解，但是所有视频输出接口工作正常  

- 增加 **LogoutHook** 文件用于模拟NVRAM，请在安装完系统后将该文件夹放置在任意位置。并且在终端输入 ```sudo defaults write com.apple.loginwindow LogoutHook /path/to/LogoutHook.command```

	比如你放在**下载**文件夹内： ```sudo defaults write com.apple.loginwindow LogoutHook /Users/xjn/Documents/LogoutHook/LogoutHook.command```

	重启后，你会在/EFI/下看到nvram.plist，代表已经成功模拟了。

	**！运行后不要删除补丁包 ！**

- 如果认为支持HEVC硬解更重要，可以下载 [EFI-630.zip](https://github.com/Road-tech/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/raw/master/EFI-630.zip)。 此EFI显卡ID设置为 0x59120000 ｜iMac18,2 ｜	Intel HD Graphics HD630  

	**！ 此EFI仅中间的HDMI接口可以使用 ！**
	
- 定制USB接口，修复USB-C接口（现在可以正反插），修复USB充电（现支持苹果快充）   

- 地区代码从```HK```改为```#a```, 修复Wi-Fi只能到300m的bug  

## 成品展示

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/13EE6E89-9978-4196-BB65-22C892472BAA_1_105_c.jpeg?raw=true)
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/8CB768EC-7D4C-49EA-9FDE-12661C0B0B63_1_105_c.jpeg?raw=true)
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/截屏2020-01-27下午4.12.45.png?raw=true)
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/截屏2020-01-27下午4.40.26.png?raw=true)
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/%E6%88%AA%E5%B1%8F2020-02-18%E4%B8%8B%E5%8D%886.58.19.png?raw=true)
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/截屏2020-01-27下午4.58.51.png?raw=true)
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/截屏2020-01-27下午4.54.32.png?raw=true)
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/截屏2020-01-27下午5.00.46.png?raw=true)
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/截屏2020-01-27下午5.01.24.png?raw=true)

## 参考链接

[精解OpenCore](https://blog.daliansky.net/OpenCore-BootLoader.html) - [黑果小兵的部落阁 ](https://blog.daliansky.net/)

[使用OpenCore引导黑苹果](https://blog.xjn819.com/?p=543) - [XJN](https://blog.xjn819.com/) 

[Asrock deskmini 310-com hackintosh 10.14-10.15 EFI](https://blog.xjn819.com/?p=7) - [XJN](https://blog.xjn819.com/)

[分享EFI 华硕H110S1 STX主板 i3-8100 UHD630](http://bbs.pcbeta.com/viewthread-1801615-1-1.html) - [mike20080924](http://i.pcbeta.com/space-uid-3336274.html)

[DW1820A/BCM94350ZAE/BCM94356ZEPA50DX插入的正确姿势](https://blog.daliansky.net/DW1820A_BCM94350ZAE-driver-inserts-the-correct-posture.html) - [黑果小兵的部落阁](https://blog.daliansky.net/)
