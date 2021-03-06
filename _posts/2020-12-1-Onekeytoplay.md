---
layout:     post   				    # 使用的布局（不需要改）
title:      iOS设置下班一键导航+放歌 # 标题 
subtitle:   捷径(快捷指令)简易教程   #副标题
date:       2020-12-1 				# 时间
author:     Road 						# 作者
header-img: img/iOSOneButtonNavigation&play-05.JPG	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - 捷径
    - 快捷指令
    - 一键导航
    - CarPlay
---

## 小声明

这只是个很简单的小教程，初衷只是为了方便生活。
So，如果你已经是捷径（快捷指令）大神，轻喷。
如果能顺便提点改进建议给我就更好了。

## 使用场景

在成为一枚社畜之后，每天必备的操作就是：

> 上车 -> 打开高德地图导航 -> 打开网易云放歌 -> 家or公司   

虽然用时不久，但是上班~~归家~~心切，必定是操作步骤越少越好。
所以就用上iOS的捷径（快捷指令）。

## 设置捷径指令
### 网易云
1. 首先你需要在网易云音乐的设置里添加Siri捷径

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@3.0/iOSOneButtonNavigation&play/iOSOneButtonNavigation&play-01.jpg?raw=true)

2. 这样你才能能在**快捷指令**里找到有关网易云音乐的指令。

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@3.0/iOSOneButtonNavigation&play/iOSOneButtonNavigation&play-02.jpg?raw=true)

### 获取高德地图跳转接口
我们去到高德地图的[高德开放平台](https://lbs.amap.com/api/amap-mobile/guide/ios/ios-uri-information)，去查看iOS的URL调用说明。

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@3.0/iOSOneButtonNavigation&play/iOSOneButtonNavigation&play-03.png?raw=true)

然后我们能得到一个URL的范例：    

``` iosamap://navi?sourceApplication=applicationName&poiname=fangheng &poiid=BGVIS&lat=36.547901 &lon=104.258354&dev=1&style=2 ```

！！方便排版留了空格，请自行删除所有空格！！

还有具体的参数说明：

|-----------------------+---------------------------------------------------------------------------------------------------|-------|
| 参数                	| 说明                                                                                            	| 必填 	|
|:---------------------:|:-------------------------------------------------------------------------------------------------:|:----:	|
| navi              	| 服务类型                                                                                         	| 是   	|
| sourceApplication 	| 第三方调用应用名称。如applicationName                                                             	| 是   	|
| poiname           	| POI名称                                                                                        	| 否   	|
| poiid             	| 对应sourceApplication 的POI ID                                                                 	| 否   	|
| lat               	| 纬度                                                                                            	| 是   	|
| lon               	| 经度                                                                                            	| 是   	|
| dev               	| 是否偏移(0:lat和lon是已经加密后的,不需要国测加密;1:需要国测加密)                                      	| 是   	|
| style             	| 导航方式（0 速度快；1 费用少；2路程短；3 不走高速；4 躲避拥堵；5 不走高速且避免收费；6 不走高速且躲避拥堵；7；躲避收费和拥堵；8 不走高速躲避收费和拥堵） *由于与用户本地设置冲突，iOS平台7.7.4版本起不支持该参数，偏好设置将以用户本地设置为准  	                          | 是  	|
|-----------------------+---------------------------------------------------------------------------------------------------|-------|

可以看到我们主要需要关注三个参数

* **lat**  纬度
* **lon**  经度
* **POI** POI名称

POI名称可以理解为你自定义的目的地名称，比如说“家”，“公司”。

也就是说我们只要填好这个URL的经纬度，就能自动跳转到高德地图并导航好设定的坐标。

那接下来就要获取我们目的地的坐标了。

### 获取目的地坐标
这一步很简单，打开任一地图网页，比如我选择回高德的[网页地图](https://lbs.amap.com/console/show/picker)。慢慢找到你的目的地，鼠标放上去就能获得。
比如我随便找的一家医院的某一入口。
因为是很精细的一个点，所以只要你愿意，你甚至能精确导航到你的停车位。

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@3.0/iOSOneButtonNavigation&play/iOSOneButtonNavigation&play-04.png?raw=true)

举个例子，我们要导航到经度113.29752，纬度为23.070164，并且目的地名称设置为家，那将参数填入URL范例将会得到：

``` iosamap://navi?sourceApplication=applicationName&poiname=家 &poiid=BGVIS&lat=113.29752 &lon=23.070164&dev=1&style=2 ```

！！方便排版留了空格，请自行删除所有空格！！

### 串联两个指令
很简单就像图片这样逐一添加就好了。
高德导航的URL需要单独添加并且设定Safari打开url，还能顺遍添加一个拉高屏幕亮度和手机音量的设定更加方便。

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@3.0/iOSOneButtonNavigation&play/iOSOneButtonNavigation&play-05.JPG?raw=true)

最后将指令放到桌面或者桌面插件就可以一键运行了。

##结合NFC标签一碰导航

TB上买几个NFC标签， 我选的是```TAG213```，一个应该不到2块钱。

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@3.0/iOSOneButtonNavigation&play/iOSOneButtonNavigation&play-06.jpg?raw=true)

点选```创建个人自动化``` -> 点选```NFC``` -> 点选```扫描``` -> 手机扫描NFC标签 -> 命名刚扫描的标签 -> 点选```添加操作``` -> 选择```APP``` -> 选择```快捷指令``` -> 点选 ```运行指令```

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@3.0/iOSOneButtonNavigation&play/iOSOneButtonNavigation&play-07.JPG?raw=true)

再选择刚刚设置好的指令

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@3.0/iOSOneButtonNavigation&play/iOSOneButtonNavigation&play-08.PNG?raw=true)

最后记得将```运行前询问```关掉，这样扫描标签后就可以直接开始导航，不用再确认一遍。

最后把标签贴在车上，上车一碰出发！
 