---
title: CTF入门练习：ctfshow（misc 入门）WriteUp
description: 众所周知，CTF有不同种类的题目，分别为misc，crypto，web，pwn，re，随着技术的更迭发展，区块链与AI题目也不断出现，但是从入门的角度来说，最容易获得成就感的就是misc与web了，让你有继续下去的动力，博主在写这篇文章的也是CTF小白，刚刚入门。CTF好的教程特别多，我主要写自己练习的WriteUp，各位师傅可以跟着我的博客由浅入深的练习，因为这是我正在走的路，如果之后有幸能够精通CTF，我的博客就是我成长的足迹，有写的不好的地方，请各位师傅多多指教。我选择从misc入门ctf，因为只要知道flag是什么就可以做题，成就感相较于枯燥的crypto，技术门槛高的pwn和re来的更快。本文为ctfshow平台 misc入门 题目的WriteUp。
author: jingwei
date: 2025-11-28 21:18:53 +0800
categories: [CTF, Misc]
tags: [Misc]
math: true
mermaid: true
comment: true
image:
  path: /assets/img/blog/20251128/ctfshow.png
  alt: ctfshow官方网站
---
### 1. 工欲利其事，必先利其器
打CTF如果不用任何工具单纯使用python脚本编写，效率会很慢，每种题型都有其适合的解题辅助工具，甚至还有大佬根据题型写的一把梭工具，但是入门时不推荐使用一把梭，因为很容易忽略知识点，太过依赖工具，万一出了套娃题就死哈一只了（特指死掉的蟹），在做CTFshow网站中的misc 入门题（全为图片题）主要用到以下工具，以后做到图片题时可以回来看看噢！本文题目来源于[**CTFShow**](https://ctf.show/)，作为misc入门非常友好。
| 序号  |             本节所需工具             |                                            用途                                            |          平台           |
| :---: | :----------------------------------: | :----------------------------------------------------------------------------------------: | :---------------------: |
|   1   |               tweakpng               |                                  png图片数据块查看，编辑                                   |         windows         |
|   2   |                WinHex                |                                查看、编辑文件16进制串的工具                                |         windows         |
|   3   |              010Editor               |                            查看、编辑文件16进制串的工具（推荐）                            |         windows         |
|   4   |              StegSolve               |                                        查看图像通道                                        | jar包，需java -jar 运行 |
|   5   |             apngdis_gui              |                           将 APNG 文件分解为一系列独立的 PNG 帧                            |         windows         |
|   6   |               binwalk                |                        分析和提取二进制文件（包括固件映像）中的数据                        |          linux          |
|   7   |               foremost               |                        依据文件内的文件头和文件尾对一个文件进行分离                        |          linux          |
|   8   |               exiftool               |                      查看文件属性信息，类似于windows鼠标右键查看属性                       |          linux          |
|   9   | honeyview(free) or bandiview(bought) |                              bandi公司出品的多格式图片查看器                               |         windows         |
|  10   |                Python                | 编写脚本解题的关键语言，简单库多，解题的不二语言，推荐使用pycharm中的jupyterbook，代码补全 |       python env        |
### 2. WriteUp
#### 2.1 Misc1.png
**锐评：** 不是每道题都有锐评，但是如果ctf竞赛也出这种题是不是就拼手速抢分了，恭喜您拿到了新手福利，下载后直接两眼一瞪，这不是我苦苦寻觅的flag吗，怎么直接就出来了，一定是假的，一定是假的！  
![misc1](/assets/img/blog/20251128/misc1.png)  
**logic:** 毫无logic，解压后直接看到flag，送分题，毫无成就感！  
**flag：** <kbd>ctfshow{22f1fb91fc4169f1c9411ce632a0ed8d}</kbd>
#### 2.2 Misc2.txt
**logic:** 是骡子是马拉出来溜溜，首先扔到010Editor或者winhex中看看是骡子是马，看看文件开头16进制魔数是啥~~诶喂不是魔术~~ ，参考[**文件签名**](https://jingwei1205.github.io/posts/file-signatures/)对比看看真实的扩展名应该为什么，我们根据89 50 4E 47可知，该文件真实格式为png非txt，只要修改扩展名打开即可。
![010Editor](/assets/img/blog/20251128/misc2-1.png)   
![flag](/assets/img/blog/20251128/misc2.png)  
**flag：** <kbd>ctfshow{6f66202f21ad22a2a19520cdd3f69e7b}</kbd>
#### 2.3 Misc3.bpg
**锐评：** 什么！还有我打不开的图片格式？你别激动，智能看图，我说的不是你！你个流氓软件！  
**logic:** 直接使用honeyview bandiview打开图片查看      
**flag：** <kbd>ctfshow{aade771916df7cde3009c0e631f9910d}</kbd>
#### 2.4 Misc4.txt
**锐评：** 同样的技能我要放六次，你接住喽！甭管什么妖怪，先进我的010炼丹炉，道生一，一生二，二生万物！  
**logic:** 打开一看6个txt，全部丢进010过一遍，对比魔数，改成相应的文件扩展名即可看到flag，然后将6张图片的信息串起来就是flag。  
**flag：** <kbd>ctfshow{4314e2b15ad9a960e7d9d8fcff902da}</kbd>
#### 2.5 Misc5.png
**锐评：** 什么！there is no flag！你说no就no？继续炼丹！  
**logic:** 扔进010中搜索ascii字符中是否包含flag的关键字（ctfshow的关键字当然是ctfshow，也有可能c*t*f，f*l*a*g，出题人就是那么喜欢跳格子），本题直接搜到ctfshow在文件末尾（当然各位师傅眼力好直接就能看到）  
![](/assets/img/blog/20251128/misc5.png)  
**flag：** <kbd>ctfshow{2a476b4011805f1a8e4b906c8f84083e}</kbd>
#### 2.6 Misc6.png
**锐评：** 什么！看不起我？一样的题出两遍？  
**logic:** 扔进010中搜索ascii字符中是否包含flag的关键字（ctfshow的关键字当然是ctfshow，也有可能c*t*f，f*l*a*g，出题人就是那么喜欢跳格子），本题直接搜到ctfshow在文件中间（当然各位师傅眼力好也得看花了这次，真到中间了）
![](/assets/img/blog/20251128/misc6.png)  
**flag：** <kbd>ctfshow{d5e937aefb091d38e70d927b80e1e2ea}</kbd>
#### 2.7 Misc7.jpg
**锐评：** 这知识点出三遍？质疑我们智商吗，其实这个让我们加深了肌肉记忆，拿进来先扔010，看文件格式魔数是否正确，再搜索文件信息是否含有关键信息。  
**logic:** 扔进010中搜索ascii字符中是否包含flag的关键字（ctfshow的关键字当然是ctfshow，也有可能c*t*f，f*l*a*g，出题人就是那么喜欢跳格子），本题直接搜到ctfshow在文件中间（当然各位师傅眼力好也得花了，听我的别用你的眼睛了）
![](/assets/img/blog/20251128/misc7.png)  
**flag：** <kbd>ctfshow{c5e77c9c289275e3f307362e1ed86bb7}</kbd>
#### 2.8 Misc8.png
**锐评：** 我排在别人后面你就看不到我，你个小丑，略略略有本事你来找我噻！   
**logic:** 扔进010中对比魔数正确，搜索ascii字符中没有关键字，乃么好嘞，死哈一只了，不我还能抢救，彩色没有未来，黑白窗口给我力量，打开kali输入<kbd>binwalk misc8.png</kbd>，发现里面藏了两张png图片，此时使用<kbd>foremost misc8.png</kbd>，在桌面上out文件夹中会获得两张图片，一张就是flag啦！你会问，你不是linux吗为啥在桌面上，那当然我用的wsl啦，强推wsl比虚拟机好用一万倍！windows用户专属福利噢！
![](/assets/img/blog/20251128/misc8-1.png)  
![](/assets/img/blog/20251128/misc8.png) 
有人就会锐评你的锐评了，你这锐评和这题目有啥关联吗，那肯定有啊，我不喜欢说废话的，每句话言简意赅。**这是因为当你打开010查看的时候会发现两个89 50 4E 47说明有两个png文件，但是第二张png不会被显示，只会显示第一张，那么是不是把第一张删除了就能看到第二张了呢？让我们运行下面这行指令，就能直接得到结果，这是了解知识的解题方法，发现第二张png从3892地址开始，那么跳过3892个字节截取后面的内容就是第二张png的内容啦！
```shell
dd if=misc8.png of=flag.png bs=1 skip=3892
```
![](/assets/img/blog/20251128/misc8-2.png) 
**flag：** <kbd>ctfshow{1df0a9a3f709a2605803664b55783687}</kbd>
#### 未完待续...今天太晚了 有空再更新噢 宝子们 晚安