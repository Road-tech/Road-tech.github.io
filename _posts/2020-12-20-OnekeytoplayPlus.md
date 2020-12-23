---
layout:     post   				            		# 使用的布局（不需要改）
title:      懒人升级！自动判断上下班+导航+放歌		# 标题 
subtitle:   捷径(快捷指令)简易教程              		# 副标题
date:       2020-12-20 								# 时间
author:     Road 									# 作者
header-img: img/iOSOneButtonNavigation&play-05.JPG	# 这篇文章标题背景图片
catalog: true 										# 是否归档
tags:												# 标签
    - 捷径
    - 快捷指令
    - 一键导航
    - CarPlay
 
---

## 小声明

这依旧是个很简单的小教程，初衷只是为了方便生活。
So，如果你已经是捷径（快捷指令）大神，勿喷！
如有，也感谢大家提改进建议给我。

## Q&A

Q：为什么你每天上下班还要导航？
A：我上下班每日通勤平均时间40min，不同的路径，不同的城市道路+高速组合，拥堵的时候差距可以多达20min。所以目前我很依赖导航。

Q：还是XX手机的XX助手更方便，轻轻松松就设置好了。
A：本文仅适用于iOS手机。

## 使用场景

之前已经写了一篇文章，介绍了如何设置上下班一键导航+放歌。配合NFC标签，可以做到一碰就开始导航，没有多余的操作了。

但是还是觉得不完美，毕竟上下班还是要单独点选一下；用NFC标签的话还要准备两张，还是不够懒人。

所以我们再优化一下，加入工作日和时间判断，再配合判断蓝牙或者Carplay的连接状态，做到点选都不用、更加懒人的效果。

## 总体思路

大致的思路or流程如图：

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@4.0/ShortcutGen2/ShortcutGen2-1.png?raw=true)

iOS的**快捷指令**里拥有一栏叫自动化，为我们预设了各种触发指令的场景。我会选择用**连接CarPlay车载时**或者**蓝牙**的触发场景。当手机自动连上车上的CarPlay或者中控的蓝牙时，去触发设定好的指令。

触发指令后，指令会去播放音乐，然后会去判断今日日期，如果是周末就退出。如果是工作日，就去判断是上班还是回家。

判断上班还是回家的方法有很多种，可以用判断回家的距离或者时常大于或者小于某些值来区分，也可以用判断当前时间是早上还是下午来区分。这里我选择相对简单的用时间判断上下午。

当判断出上班还是回家后，再跳转触发上篇文章教大家设定好的一键导航就好了。

## 设置捷径指令

因为iOS的快捷指令的设置界面的逻辑其实并不清晰，所以我不打算将一整套流程都设置在一个快捷指令里，而是选用套娃的方式，某一条件判断好了，就跳到下一个对应的快捷指令中。

PS. 就是我们编程时写function的逻辑 - -｜

### 设定一键导航

这里就不重复了，有劳大家去上一篇文章去查看。

上一篇文章的链接：[iOS设置下班一键导航+放歌](https://post.smzdm.com/p/ammq20rv/)

这里我会创建两个一键导航的快捷指令，分别叫“上班”，“回家”。

### 判断上班还是回家

也就是整个流程的这一部分：
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@4.0/ShortcutGen2/ShortcutGen2-2.png?raw=true)

这里我选择相对简单的用时间判断上下午。

因为快捷指令并没有提供现成的判断上下午的指令，所以换个思路，利用快捷指令的**格式化**功能。 将时间转为纯数字格式再比较数值大小，如将时间11:30转为纯数字的1130，然后比较数字大小；数字小于1200即为上午，大于1200即为下午。

查看Apple官方的快捷指令使用手册，找到关于[自定日期格式](https://support.apple.com/zh-cn/guide/shortcuts/apd8d9b19184/4.0/ios/14.0)的内容，可以看到快捷指令采用了[Unicode Technical Standard #35](https://unicode.org/reports/tr35/tr35-dates.html#Date_Format_Patterns)的格式标准。

|-----------------------------------+---------------------------------------|
|              模式              	|                 结果                 	|
|:------------------------------:	|:------------------------------------:	|
| yyyy.MM.dd G 'at' HH:mm:ss zzz 	| 1996.07.10 AD at 15:08:56 PDT        	|
| EEE, MMM d, ''yy               	| Wed, July 10, '96                    	|
| h:mm a                         	| 12:08 PM                             	|
| hh 'o''clock' a, zzzz          	| 12 o'clock PM, Pacific Daylight Time 	|
| K:mm a, z                      	| 0:00 PM, PST                         	|
|-----------------------------------+---------------------------------------|

其中我们关注的小时就是字母H
HH代表的是24小时制的小时，hh代表的是12小时制的小时
mm代表的是分钟，个位数的时候补零。m则不补零。

这一部分的捷径可以设置为

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@4.0/ShortcutGen2/ShortcutGen2-3.JPG?raw=true)

具体流程就是：

获取当前时间-> 时间格式转为自定格式、HHmm-> 用转换后的数字-1130-> 条件判断、计算结果小于0则为上午，大于0则为下午-> 跳转到对应的快捷指令“上班”or“下班”

1130对应就是11点30分，这个判断时间可以按照你的需求自己设定。

设定**如果**这个脚本的时候，判断条件可能无法设定为**小于**，而是只能设定为包含、有任何值等条件。需要将**计算的结果**从文本改变为数字，就可以设定为大于or小于了。

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@4.0/ShortcutGen2/ShortcutGen2-4.png?raw=true)

### 判断工作日

也就是整个流程的这一部分：
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@4.0/ShortcutGen2/ShortcutGen2-5.png?raw=true)

依旧是利用快捷指令的**格式化**功能。 将周几格式转为纯数字格式再比较数值区间，如将周二转为纯数字的2，然后比较得出2在范围1-5之间，则为工作日；否则即为周末。

查看[Unicode Technical Standard #35](https://unicode.org/reports/tr35/tr35-dates.html#Date_Format_Patterns)的格式标准，星期的定义为：

|------	|------------------	|----------	|------------------------------	|
| Sym. 	| Field Patterns 	| Examples 	| Description                  	|
|------	|----------------	|----------	|------------------------------	|
| E    	| E..EEE         	| Tue      	| Abbreviated                  	|
| 　   	| EEEE           	| Tuesday  	| Wide                         	|
| 　   	| EEEEE          	| T        	| Narrow                       	|
| 　   	| EEEEEE         	| Tu       	| Short                        	|
| e    	| e              	| 2        	| Numeric: 1 digit             	|
| 　   	| ee             	| 2        	| Numeric: 2 digits + zero pad 	|
| 　   	| eee            	| Tue      	| Abbreviated                  	|
| 　   	| eeee           	| Tuesday  	| Wide                         	|
| 　   	| eeeee          	| T        	| Narrow                       	|
| 　   	| eeeeee         	| Tu       	| Short                        	|
| c    	| c..cc          	| 2        	| Numeric: 1 digit             	|
| 　   	| ccc            	| Tue      	| Abbreviated                  	|
| 　   	| cccc           	| Tuesday  	| Wide                         	|
| 　   	| ccccc          	| T        	| Narrow                       	|
| 　   	| cccccc         	| Tu       	| Short                        	|
|------	|------------------	|----------	|------------------------------	|

我们需要的就是```e```，即星期二输出```2```.

测试一下：
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@4.0/ShortcutGen2/ShortcutGen2-6.png?raw=true)

可以看到虽然是星期一，但是输出的数字居然是2。这里应该是根据手机的地区设置，一周的开始是周日，所以周一到周五的数字范围就是2-6。大家要依据自己的实际情况做调整。

这一部分的捷径可以设置为

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@4.0/ShortcutGen2/ShortcutGen2-7.JPG?raw=true)

具体流程就是：

获取当前时间-> 时间格式转为自定格式、e-> 数字大于等于2，是下一步，否则提示今天不上班-> 数字小于等于6，是下一步，否则提示今天不上班-> 跳转到对应的快捷指令“判断上下班”。

依旧要注意设定**如果**这个脚本的时候，需要将**计算的结果**从文本改变为数字，才可以设定为大于or小于。

### 设定自动化场景

如图：

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@4.0/ShortcutGen2/ShortcutGen2-8.png?raw=true)
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@4.0/ShortcutGen2/ShortcutGen2-9.png?raw=true)

具体流程就是：

手机连接到CarPlay-> 播放网易云-> 判断工作日

### 附加内容

其实目前为止的自动化场景也足够满足大多数情况了，但是如果小伙伴们有更高的要求，希望连法定节假日和补班也算上，那就继续看下面的附加内容吧。

为什么判断法定节假日和补班是附加内容呢？因为法定节假日和补班每年都不一样，这就需要每年至少要更新一次放假安排。为了方便--懒--，这个时候我们就要去依托别人的服务。这个时候就会有不稳定的因素产生了，别人提供的服务，或者因为网络因素，或者服务器的承受能力，或者经济原因。很有可能突然就因为各种原因就失效了，然后影响我们的捷径自动化判断。

当然，在了解完上述这些不稳定因素，你仍然认为这是可以接受并且想要更完善的体验，我推荐你几个思路：

1. 直接调用别人的节假日判断的API接口，如```http://timor.tech/api/holiday/info/2018-3-2``` 具体API内容内容可以[参考这里](https://timor.tech/api/holiday/)。这个方法优点是简单，直接传递日期过去，传回的信息连星期几，是否节假日都有了。缺点是开发者用爱发电，服务容易遭受攻击导致不稳定。
2. 直接下载别人维护好，放在公共平台的假日列表，如gameboyLV的[ChineseHoliday项目](https://github.com/gameboyLV/ChineseHoliday/commits/master)。优点是服务器相对稳定（文件存放在GitHub并且可以配合CDN保证网络访问质量），缺点是大佬可能哪年就不更新了。不过我看大佬从16年开始一直有更新到21年，还是很稳定的。实在不行我们可以fork过来自己更新嘛。
3. 订阅公共日历，也就是别人维护的法定假期的公共日历。如[这个地址](https://zhuanlan.zhihu.com/p/136669675)内提供的订阅日历，大家也可以自己找。优点依旧是服务器相对稳定（日历依托在iCloud），缺点依然是可能哪年就不更新了。

加入节假日和补班日的判断后的大致的思路or流程如图：
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@4.0/ShortcutGen2/ShortcutGen2-10.png?raw=true)

我这里演示方法二。

我先fork了的gameboyLV项目，然后release发布了一个1.0版方便蹭免费的CDN加速。

然后公众假日的链接为

```https://cdn.jsdelivr.net/gh/Road-tech/ChineseHoliday@1.0/data/XXXX.txt```

补假的链接为

```https://cdn.jsdelivr.net/gh/Road-tech/ChineseHoliday@1.0/data/XXXX_w.txt```

链接里```XXXX```代表当前年份。

举个例子关于节假日判断，也就是这部分：

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@4.0/ShortcutGen2/ShortcutGen2-11.png?raw=true)

这一部分的捷径可以设置为

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@4.0/ShortcutGen2/ShortcutGen2-12.JPG?raw=true)

判断打定工作日的具体流程就是：

获取当前日期-> 日期格式转为两个格式化后的日期，MMdd和yyyy-> 设定URL```https://c...1.0/data/[格式化后的日期yyyy].txt```-> 获取URL内容-> 如果URL内容里有[格式化后的日期MMdd]，也就是当前日期-> 如果URL内容里含有当前日期就放假，否则上班

判断补假的流程类似，只是要将URL换成```https://c...1.0/data/[格式化后的日期yyyy]_w.txt```
