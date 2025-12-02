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
**锐评：** 什么！还有我打不开的图片格式？你别激动，智能看图，我说的不是你！你个流氓软件！PS：是我吗？等你打开再看到flag旗子分数都变成负分了！  
**logic:** 直接使用honeyview bandiview打开图片查看      
**flag：** <kbd>ctfshow{aade771916df7cde3009c0e631f9910d}</kbd>
#### 2.4 Misc4.txt
**锐评：** 同样的技能我要放六次，你接住喽！甭管什么妖怪，先进我的010炼丹炉，道生一，一生二，二生万物！  
**logic:** 打开一看6个txt，全部丢进010过一遍，对比魔数，改成相应的文件扩展名即可看到flag，然后将6张图片的信息串起来就是flag。  
**flag：** <kbd>ctfshow{4314e2b15ad9a960e7d9d8fcff902da}</kbd>
#### 2.5 Misc5.png
**锐评：** 什么！there is no flag！你说no就no？继续炼丹！  
**logic:** 扔进010中搜索ascii字符中是否包含flag的关键字（ctfshow的关键字当然是ctfshow，也有可能c\*t\*f，f\*l\*a\*g，出题人就是那么喜欢跳格子），本题直接搜到ctfshow在文件末尾（当然各位师傅眼力好直接就能看到）  
![](/assets/img/blog/20251128/misc5.png)  
**flag：** <kbd>ctfshow{2a476b4011805f1a8e4b906c8f84083e}</kbd>
#### 2.6 Misc6.png
**锐评：** 什么！看不起我？一样的题出两遍？  
**logic:** 扔进010中搜索ascii字符中是否包含flag的关键字（ctfshow的关键字当然是ctfshow，也有可能c\*t\*f，f\*l\*a\*g，出题人就是那么喜欢跳格子），本题直接搜到ctfshow在文件中间（当然各位师傅眼力好也得看花了这次，真到中间了）
![](/assets/img/blog/20251128/misc6.png)  
**flag：** <kbd>ctfshow{d5e937aefb091d38e70d927b80e1e2ea}</kbd>
#### 2.7 Misc7.jpg
**锐评：** 这知识点出三遍？质疑我们智商吗，其实这个让我们加深了肌肉记忆，拿进来先扔010，看文件格式魔数是否正确，再搜索文件信息是否含有关键信息。  
**logic:** 扔进010中搜索ascii字符中是否包含flag的关键字（ctfshow的关键字当然是ctfshow，也有可能c\*t\*f，f\*l\*a\*g，出题人就是那么喜欢跳格子），本题直接搜到ctfshow在文件中间（听我的别用你的眼睛了）
![](/assets/img/blog/20251128/misc7.png)  
**flag：** <kbd>ctfshow{c5e77c9c289275e3f307362e1ed86bb7}</kbd>
#### 2.8 Misc8.png
**锐评：** 我排在别人后面你就看不到我，你个小丑，略略略有本事你来找我噻！   
**logic:** 扔进010中对比魔数正确，搜索ascii字符中没有关键字，乃么好嘞，死哈一只了，不我还能抢救，彩色没有未来，黑白窗口给我力量，打开kali输入<kbd>binwalk misc8.png</kbd>，发现里面藏了两张png图片，此时使用<kbd>foremost misc8.png</kbd>，在桌面上out文件夹中会获得两张图片，一张就是flag啦！你会问，你不是linux吗为啥在桌面上，那当然我用的wsl啦，强推wsl比虚拟机好用一万倍！windows用户专属福利噢！
![](/assets/img/blog/20251128/misc8-1.png)  
![](/assets/img/blog/20251128/misc8.png)   
有人就会锐评你的锐评了，你这锐评和这题目有啥关联吗，那肯定有啊，我不喜欢说废话的，每句话言简意赅。**这是因为当你打开010查看的时候会发现两个89 50 4E 47说明有两个png文件，但是第二张png不会被显示，只会显示第一张，那么是不是把第一张删除了就能看到第二张了呢？**让我们运行下面这行指令，就能直接得到结果，这是了解知识的解题方法，发现第二张png从3892地址开始，那么跳过3892个字节截取后面的内容就是第二张png的内容啦！
```shell
dd if=misc8.png of=flag.png bs=1 skip=3892
```
![](/assets/img/blog/20251128/misc8-2.png) 
**flag：** <kbd>ctfshow{1df0a9a3f709a2605803664b55783687}</kbd>

#### 2.9 Misc9.png
**锐评：** 不想评价，可能出题人觉得我们太菜了，需要题海战术。   
**logic:** 使用010editor打开文件，<kbd>ctrl+f</kbd>搜索ctfshow即可获得flag。  
![](/assets/img/blog/20251128/misc9.png) 
**flag：** <kbd>ctfshow{5c5e819508a3ab1fd823f11e83e93c75}</kbd>
#### 2.10 Misc10.png
**锐评：** keybots解体！好啊，你又背着我藏私房旗。  
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），这里有个地方会给你误导，就是他有两个idat块，使用tweakpng合体后发现无事发生，便感觉不妙，这肯定是藏文件了，遂奔向binwalk的怀抱，一bin一个不吱声，果然发现里面有zip包，直接<kbd>binwalk -e misc10.png --run-as=root</kbd>梭出来，使用grep或者strings命令查找字符串。  
![](/assets/img/blog/20251128/misc10-1.png) 
![](/assets/img/blog/20251128/misc10-2.png) 
![](/assets/img/blog/20251128/misc10-3.png) 
**flag：** <kbd>ctfshow{353252424ac69cb64f643768851ac790}</kbd>
#### 2.11 Misc11.png
**锐评：** 乃悟前狼假寐，盖以诱敌。  
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），binwalk发现有隐藏文件，但是解出后并无flag信息，此时继续从010找答案，发现两个IDAT数据块，将第一个数据块使用tweakpng删除后保存即可得到flag。  
**theory：**IDAT 块只有当上一个块充满（正常length最大65524）时，才会继续一个新的块。程序读取图像的时候也会在第一个未满的块停止（查了下W3C标准，其实是PNG图片在压缩的时候会在最后一个块的标记位标明这是最后一个数据块）。所以如果某一块没有满但后面却还有 IDAT 块则说明后面的块是“假”的，这里发现第一个数据块根本没有填满就有另一个。
![](/assets/img/blog/20251128/misc11-1.png)   
![](/assets/img/blog/20251128/misc11.png)   
**flag：** <kbd>ctfshow{44620176948fa759d3eeafeac99f1ce9}</kbd>
#### 2.12 Misc12.png
**锐评：** 乃悟前狼们假寐，盖以诱敌。  
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），binwalk发现无隐藏文件，此时继续从010找答案，发现数个IDAT数据块，每块都不满就有下一块，使用tweakpng整合后在使用binwalk发现两个zlib文件，但是使用binwalk -e解包出来后发现无flag，考虑将第一个zlib部分删除，共 3149-41 = 3108，将未合并的图片使用tweakpng打开后发现前8IDAT刚好长度为3108，删除后重新保存图片获得flag。
![](/assets/img/blog/20251128/misc12-1.png)   
![](/assets/img/blog/20251128/misc12-2.png)   
**flag：** <kbd>ctfshow{10ea26425dd4708f7da7a13c8e256a73}</kbd>
#### 2.13 Misc13.png
**锐评：** 小时候玩过跳房子吗，有些地方不能踩噢。  
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），可以搜到c\*t\*f的关键词（我上面的题目疯狂暗示噢，夹花搜也有可能），发现每个关键部分隔了一个字符，将字符记录下来写python脚本解出flag。将所有可以字符串复制到脚本中解出，发现有三个flag是一致的，有一个flag不一样，将两个flag分别提交后即可。
![](/assets/img/blog/20251128/misc13-1.png)   
```python
interval_str1 = "ct¹f…s†hªoKw°{!aeS6¥eT34fxa%4Ý8ïf«52•8b‚1º7E4|2Td~7:2äeñ6úfõ4129T8ñ328é0l}"
interval_str2 = "ct¹f…s†hªoKw°{!1eS3¥eT24exd%4Ý8ïf«51•8b‚7ºeE4|2T6~7:däeñ1úcõ412aT8ñ329éal}"
interval_str3 = "ct¹f…s†hªoKw°{!aeS6¥eT34exa%4Ý8ïf«51•8b‚7ºeE4|2Td~7:däeñ6úfõ412fT8ñ329éal}"
interval_str4 = "ct¹f…s†hªoKw°{!aeS6¥eT446xc%4Ý8ïf«73•9b‚7ºeEb|2Td~1:däeñ6úeõ412fT8ñ329éal}"
interval_str = [interval_str1, interval_str2, interval_str3, interval_str4]
for key_str in interval_str:
    result = ""
    for i in range(0, len(key_str)):
        if i%2==0:
            result += key_str[i]
    print("第", interval_str.index(key_str) + 1, "个可疑字符串隐藏的flag:", result)
```
**flag：** <kbd>ctfshow{ae6e46c48f739b7eb2d1de6e412f839a}</kbd>
#### 2.14 Misc14.jpg
**锐评：** 还是那头狼假寐诱敌，但是这次的猎物是jpg。  
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），binwalk发现隐藏文件，使用binwalk -e解包无果，考虑使用以下命令将第二幅jepg前部分删除。
![](/assets/img/blog/20251128/misc14-1.png)   
```shell
dd if=misc14.jpg of=result.jpg bs=1 skip=$((0x837))
```
![](/assets/img/blog/20251128/misc14-2.jpg)   
**flag：** <kbd>ctfshow{ce520f767fc465b0787cdb936363e694}</kbd>
#### 2.15 Misc15.bmp
**锐评：** 别人能藏的地方我也能藏，谁还不是二进制动物啦。  
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），搜索到ctf关键词得到flag。
![](/assets/img/blog/20251128/misc15-1.png)   
**flag：** <kbd>ctfshow{fbe7bb657397e6e0a6adea3e40265425}</kbd>
#### 2.16 Misc16.png
**锐评：** 别人能藏的地方我也能藏，谁还不是二进制动物啦。  
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），无果上binwalk，发现有文件隐藏，直接使<kbd>用binwalk -e misc16.png --run-as=root</kbd>提取得到文件，使用grep命令搜索ctf关键词得到了flag。
![](/assets/img/blog/20251128/misc16-1.png)   
![](/assets/img/blog/20251128/misc16-2.png)   
**flag：** <kbd>ctfshow{a7e32f131c011290a62476ae77190b52}</kbd>
#### 2.17 Misc17.png
**锐评：** 宝儿，你不是我亲生的，你的DNA是89 50 4E 47，你是png的孩子。  
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），无果上binwalk，发现有文件隐藏，直接使<kbd>用binwalk -e misc17.png --run-as=root</kbd>提取得到文件无果，考虑合并IDAT后再使用binwalk扫描提取文件发现藏了一个zip，使用同样命令分离后，无法使用grep找到flag，将每个文件丢到010发现有个文件的魔数为png，修改后缀名即可。
![](/assets/img/blog/20251128/misc17-1.png)   
![](/assets/img/blog/20251128/misc17-2.png)   
**flag：** <kbd>ctfshow{0fe61fc42e8bbe55b9257d251749ae45}</kbd>
#### 2.18 Misc18.jpg
**锐评：** 你出生时有些事情就决定好了，例如像你们出生就是富二代。  
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），搜到ctf关键词但是发现断断续续的，而且有很多adobe的属性内容，考虑查看属性，使用exiftool命令查看。但是直接使用右键在windows上查看属性，不用排序，直接按照显示顺序输入即可。
![](/assets/img/blog/20251128/misc18.png)    
**flag：** <kbd>ctfshow{325d60c208f728ac17e5f02d4cf5a839}</kbd>
#### 2.19 Misc19.tif
**锐评：** 但是有些人出生就是富二代，他爸妈却没告诉他。  
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），搜到ctf关键词但是发现断的，两段拼起来即可。
![](/assets/img/blog/20251128/misc19.png)    
**flag：** <kbd>ctfshow{c97964b1aecf06e1d79c21ddad593e42}</kbd>
#### 2.20 Misc20.jpg
**锐评：** 少小离家老大回，乡音无改鬓毛衰。有些口音你生下来就会了改不了，让我们感叹母语迸发的力量。  
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），使用binwalk发现无隐藏文件，使用exiftool发现一段离谱的中文，接下来你只要读出来这段中文，flag就从你嘴巴里出来了，若你不会中文，这道题就跳过吧。
![](/assets/img/blog/20251128/misc20.png)    
**flag：** <kbd>ctfshow{c97964b1aecf06e1d79c21ddad593e42}</kbd>
#### 2.21 Misc21.jpg
**锐评：** 。  
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），使用binwalk发现无隐藏文件，使用exiftool发现一段序列串，将这个序列串复制到字符串自动映射的[**网站**](https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html)，发现asicii码解出来是有意义的，要把所有的X和Y变成16进制组合在一起，写脚本解决。
![](/assets/img/blog/20251128/misc21-2.png)    
![](/assets/img/blog/20251128/misc21-1.png)   
```python
data = [3902939465,1082452817,2371618619,2980145261]

result = "ctfshow{" + "".join(format(d, "x") for d in data) + "}"
print(result)
``` 
**flag：** <kbd>ctfshow{e8a221494084eb518d5c073bb1a1686d}</kbd>
#### 2.22 Misc22.jpg
**锐评：** 有的人表面黑白分明，刚正不阿，很高大的样子，其实他把黄黄的内心藏在了小小的图里，不仔细看真看不出来你是这样的人。  
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），使用binwalk发现无隐藏文件，使用exiftool发现有缩略图<kbd>Thumbnail Image                 : (Binary data 8201 bytes, use -b option to extract)</kbd>，提示使用exiftool -b提取，主打一个听人劝使用以下命令提取得到缩略图，黄色字就是flag。
![](/assets/img/blog/20251128/misc22.png)    
```shell
exiftool -b -ThumbnailImage misc22.jpg > thumb.jpg
``` 
**flag：** <kbd>ctfshow{dbf7d3f84b0125e833dfd3c80820a129}</kbd>
#### 2.23 Misc23.psd
**锐评：** 看清楚是psd，不是ptsd，因为经过时间长了少了time就不pstd了，我没t，我没t，恐龙抗狼抗狼抗！  
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），使用binwalk发现无隐藏文件，使用exiftool发现有getflag的提示，需要将时间戳从十进制转为十六进制就可以得到flag啦，发现修改历史中有很多时间戳，转为long类型时间戳后转十六进制即可获得。
![](/assets/img/blog/20251128/misc23.png)    
```python
from datetime import datetime, timezone, timedelta

def parse_timestamp(time_str):
    """
    解析 ISO 8601 时间字符串（带 +HH:MM 时区），返回 UTC 时间戳
    """
    # 使用 fromisoformat 解析
    dt = datetime.fromisoformat(time_str)
    # 转为 UTC 时间
    dt_utc = dt.astimezone(timezone.utc)
    # 返回整数 Unix 时间戳
    return int(dt_utc.timestamp())

def deal_time():
    result = "ctfshow{"
    # 时间列表
    times = [
        "1997:09:22 02:17:02+08:00",
        "2055:07:15 12:14:48+08:00",
        "2038:05:05 16:50:45+08:00",
        "1984:08:03 18:41:46+08:00"
    ]

    print(f"{'Original Time':35} {'Timestamp (DEC)':15} {'Timestamp (HEX)'}")
    print("-"*70)

    for t in times:
        # 把 ":" 改成 "-"，适配 fromisoformat
        t_iso = t.replace(":", "-", 2)  # 只替换前两个冒号（年份后冒号不要动）
        ts = parse_timestamp(t_iso)
        ts_hex = hex(ts).upper()[2:]  # 去掉 0x 并大写
        result+=ts_hex;
        print(f"{t:35} {ts:<15} {ts_hex}")
    result += "}"
    print(result.lower())

deal_time()
``` 
**flag：** <kbd>ctfshow{3425649ea0e31938808c0de51b70ce6a}</kbd>
#### 2.41 Misc41.jpg
**锐评：** 听说只有愚人节的愚人才能cosplay这道旗，H4ppy Apr1l F001's D4y！   
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），如果题目想戏耍你就肯定给你很多误解，你会发现图片都打不开，FOOL = F001？？？，喜欢cosplay是吧，那我就highlight所有愚人，看你们排的什么队！
![](/assets/img/blog/20251128/misc41.png)     
**flag：** <kbd>ctfshow{fcbd427caf4a52f1147ab44346cd1cdd}</kbd>
#### 2.24 Misc24.bmp
**锐评：** 听说站得高看得远，那我长得高是不是也能看到一样的风景。   
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），发现文件结构全是FF，使用binwalk也未发现隐藏文件，使用exiftool发现该图片字节数、比特位和大小，通过以下公式
$$
Byte(bmp) = width \times height \times bit \div 8
$$
计算后发现图片高度不对，遂查看数据块长度为675002B，24 bit位图，宽为900，计算高度为250，在010中修改高度得到图片
![](/assets/img/blog/20251128/misc24.bmp)     
**flag：** <kbd>ctfshow{dd7d8bc9e5e873eb7da3fa51d92ca4b7}</kbd>
#### 2.25 Misc25.png
**锐评：** 听说蹲下来才能拍出更美的照片。   
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），发现一切照旧，使用binwalk，exiftool未发现异常，考虑到是png，校验crc值，crc值010打开后12-28的字节，通过[**网站校验**](https://www.ip33.com/crc.html)发现问题，怀疑图片大小有问题，爆破高度，得到250，修改高度即可。
```python
import os
import struct
import zlib

IMG_DIR = "./img"
MIN_H = 1
MAX_H = 20000     # 需要更大范围自行调高

PNG_SIG = b"\x89PNG\r\n\x1a\n"


def parse_chunks(data):
    """解析 PNG chunk，返回 (length, type, data, crc, offset)"""
    if not data.startswith(PNG_SIG):
        raise ValueError("不是 PNG 文件")

    off = len(PNG_SIG)
    chunks = []

    while off + 8 <= len(data):
        length = struct.unpack(">I", data[off:off+4])[0]
        ctype = data[off+4:off+8]
        d_start = off + 8
        d_end = d_start + length
        if d_end + 4 > len(data):
            break

        cdata = data[d_start:d_end]
        crc = struct.unpack(">I", data[d_end:d_end+4])[0]

        chunks.append((length, ctype, cdata, crc, off))
        off = d_end + 4
        if ctype == b"IEND":
            break
    return chunks


def fix_ihdr_height(data, ihdr_data, crc_stored, width, off):
    """暴力遍历高度寻找使 CRC 正确的高度"""
    tail = ihdr_data[8:]   # IHDR 后 5 字节：bitdepth/color/filter/interlace
    correct = []

    for h in range(MIN_H, MAX_H + 1):
        new_data = struct.pack(">I", width) + struct.pack(">I", h) + tail
        crc_calc = zlib.crc32(b"IHDR" + new_data) & 0xffffffff
        if crc_calc == crc_stored:
            correct.append(h)

    return correct


def analyze_png(path):
    with open(path, "rb") as f:
        data = f.read()

    chunks = parse_chunks(data)
    result = []

    for length, ctype, cdata, crc_stored, off in chunks:
        crc_calc = zlib.crc32(ctype + cdata) & 0xffffffff
        if crc_calc == crc_stored:
            continue

        if ctype == b"IHDR":
            width = struct.unpack(">I", cdata[0:4])[0]
            height = struct.unpack(">I", cdata[4:8])[0]

            print(f"\n[!] IHDR CRC 错误 → 文件: {path}")
            print(f"    宽度: {width}")
            print(f"    原始高度: {height}")
            print(f"    CRC(存储):  0x{crc_stored:08X}")
            print(f"    CRC(计算):  0x{crc_calc:08X}")
            print(f"    IHDR 偏移: {off}")

            print("\n[*] 开始遍历高度寻找匹配 CRC ...")
            correct = fix_ihdr_height(data, cdata, crc_stored, width, off)

            if correct:
                print(" [+] 找到正确高度 candidate(s):", correct)
            else:
                print(" [-] 未找到匹配 CRC 的高度 (范围 {}~{})".format(MIN_H, MAX_H))

            result.append((path, width, height, correct, off))
    return result


def main():
    print("扫描 img/ 目录中 PNG 文件...\n")

    for fn in os.listdir(IMG_DIR):
        path = os.path.join(IMG_DIR, fn)
        if not os.path.isfile(path):
            continue

        with open(path, "rb") as f:
            if not f.read(8).startswith(PNG_SIG):
                continue

        analyze_png(path)


if __name__ == "__main__":
    main()
```
![](/assets/img/blog/20251128/misc25.png)     
**flag：** <kbd>ctfshow{494f611cc5842dd597f460874ce38f57}</kbd>
#### 2.26 Misc26.png
**锐评：** 你不会造轮子，还不会用轮子吗。   
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），发现一切照旧，使用binwalk，exiftool未发现异常，考虑到是png，校验crc值，crc值010打开后12-28的字节，通过[**网站校验**](https://www.ip33.com/crc.html)发现问题，怀疑图片大小有问题，爆破高度，得到606，修改高度即可，然后将高度变成16进制数就可以拼。（偷偷告诉你可以使用上题的脚本一把梭出高度噢）
![](/assets/img/blog/20251128/misc26.png)     
**flag：** <kbd>ctfshow{94aef125e087a7ccf2e28e742efd704c}</kbd>
#### 2.27 Misc27.png
**锐评：** 你不会造轮子，还不会用轮子吗。   
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），发现一切照旧，使用binwalk，exiftool未发现异常，考虑到是png，校验crc值，crc值010打开后12-28的字节，通过[**网站校验**](https://www.ip33.com/crc.html)发现问题，怀疑图片大小有问题，爆破高度，得到606，修改高度即可，然后将高度变成16进制数就可以拼。（偷偷告诉你可以使用上题的脚本一把梭出高度噢）
![](/assets/img/blog/20251128/misc27.png)     
**flag：** <kbd>ctfshow{94aef125e087a7ccf2e28e742efd704c}</kbd> 
#### 2.28 Misc28.gif
**锐评：** 敌不动我不动。   
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），先不急着上kali，由于是gif文件，需要先尝试分离帧，使用[**在线网站分离预览**](https://www.ufreetools.com/zh/tool/gif-frame-extractor)，发现只有一帧，考虑改变高度，切记将LocalScreenDescribtor与Data块中所有ImageDescribtor中的高度都要更改，否则无法显示部分帧的高度导致关键flag会遗漏。
![](/assets/img/blog/20251128/misc28.gif)     
**flag：** <kbd>ctfshow{59c8bc525426166b1c893fe12a387fd7}</kbd>
#### 2.28 Misc28.gif
**锐评：** 敌不动我不动。   
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），先不急着上kali，由于是gif文件，需要先尝试分离帧，使用[**在线网站分离预览**](https://www.ufreetools.com/zh/tool/gif-frame-extractor)，发现只有一帧，考虑改变高度，切记将LocalScreenDescribtor与Data块中所有ImageDescribtor中的高度都要更改，否则无法显示部分帧的高度导致关键flag会遗漏。
![](/assets/img/blog/20251128/misc28.gif)     
**flag：** <kbd>ctfshow{59c8bc525426166b1c893fe12a387fd7}</kbd>
#### 2.29 Misc29.gif
**锐评：** 敌乱动我乱动。   
**logic:** 使用010editor打开文件搜打撤（搜flag关键词，打量一遍文件魔数与文件结构，无果撤离上kali），先不急着上kali，由于是gif文件，需要先尝试分离帧，使用[**在线网站分离预览**](https://www.ufreetools.com/zh/tool/gif-frame-extractor)，发现多帧，但是移动到下方的时候考虑下方还有东西，尝试着改变高度，切记将LocalScreenDescribtor与Data块中所有ImageDescribtor中的高度都要更改，否则无法显示部分帧的高度导致关键flag会遗漏，重新送到帧分离器中发现其中第8帧含有flag，写入即可。
![](/assets/img/blog/20251128/misc29.png)     
**flag：** <kbd>ctfshow{03ce5be6d60a4b3c7465ab9410801440}</kbd>
#### 2.30 Misc30.bmp
**锐评：** 看清题目再做题，我打赌有人直接做题。   
**logic:** 使用010editor打开文件直接按照提示修改宽度为950，宽度英文为width不是height。
![](/assets/img/blog/20251128/misc30.bmp)     
**flag：** <kbd>ctfshow{6db8536da312f6aeb42da2f45b5f213c}</kbd>
#### 2.31 Misc31.bmp
**锐评：** 听说拉伸之后眼神也会变好。   
**logic:** 使用010editor打开文件搜打撤无果，发现数据块该图片字节数、比特位和大小，通过以下公式
$$
Byte(bmp) = width \times height \times bit \div 8
$$
计算后发现图片高度不对，遂查看数据块长度为487202B，24 bit位图，高为150，计算宽为1082，在010中修改高度得到图片
![](/assets/img/blog/20251128/misc31.bmp)     
**flag：** <kbd>ctfshow{fb09dcc9005fe3feeefb73646b55efd5}</kbd>
#### 2.32 Misc32.png
**锐评：** C4爆破！什么C4，cs玩多了？是CRC。   
**logic:** 使用010editor打开文件搜打撤无果，校验CRC发生问题，提示告诉高度正确，爆破宽度1044，在010中修改高度得到图片,给出一个自动校验CRC与先后爆破高度和宽度的代码,直接一把梭。
```python
import os
import struct
import zlib

IMG_DIR = "./img"
MIN_H = 1
MAX_H = 20000
MIN_W = 1
MAX_W = 20000

PNG_SIG = b"\x89PNG\r\n\x1a\n"


def parse_chunks(data):
    """解析 PNG chunk，返回 (length, type, data, crc, offset)"""
    if not data.startswith(PNG_SIG):
        raise ValueError("不是 PNG 文件")

    off = len(PNG_SIG)
    chunks = []

    while off + 8 <= len(data):
        length = struct.unpack(">I", data[off:off + 4])[0]
        ctype = data[off + 4:off + 8]
        d_start = off + 8
        d_end = d_start + length
        if d_end + 4 > len(data):
            break

        cdata = data[d_start:d_end]
        crc = struct.unpack(">I", data[d_end:d_end + 4])[0]

        chunks.append((length, ctype, cdata, crc, off))
        off = d_end + 4
        if ctype == b"IEND":
            break

    return chunks


def fix_ihdr_height(cdata, crc_stored, width):
    """只爆破高度"""
    tail = cdata[8:]  # IHDR 后 5 字节: bit-depth 等
    candidates = []

    for h in range(MIN_H, MAX_H + 1):
        new_data = struct.pack(">I", width) + struct.pack(">I", h) + tail
        crc_calc = zlib.crc32(b"IHDR" + new_data) & 0xffffffff
        if crc_calc == crc_stored:
            candidates.append(h)

    return candidates


def fix_ihdr_width(cdata, crc_stored, height):
    """只爆破宽度"""
    tail = cdata[8:]
    candidates = []

    for w in range(MIN_W, MAX_W + 1):
        new_data = struct.pack(">I", w) + struct.pack(">I", height) + tail
        crc_calc = zlib.crc32(b"IHDR" + new_data) & 0xffffffff
        if crc_calc == crc_stored:
            candidates.append(w)

    return candidates


def fix_ihdr_bruteforce_both(cdata, crc_stored, width, height):
    """
    先爆破高度，如果失败，再爆破宽度
    返回 (height_candidates, width_candidates)
    """
    print("\n[*] ① 开始爆破高度 ...")
    h_candidates = fix_ihdr_height(cdata, crc_stored, width)
    if h_candidates:
        print(" [+] 成功找到高度 candidate(s):", h_candidates)
        return h_candidates, []

    print(" [-] 高度未找到，继续爆破宽度 ...")

    w_candidates = fix_ihdr_width(cdata, crc_stored, height)
    if w_candidates:
        print(" [+] 成功找到宽度 candidate(s):", w_candidates)
        return [], w_candidates

    print(" [-] 宽度也未找到匹配 CRC")
    return [], []


def analyze_png(path):
    with open(path, "rb") as f:
        data = f.read()

    chunks = parse_chunks(data)

    for length, ctype, cdata, crc_stored, off in chunks:
        crc_calc = zlib.crc32(ctype + cdata) & 0xffffffff

        if crc_calc == crc_stored:
            continue

        if ctype == b"IHDR":
            width = struct.unpack(">I", cdata[0:4])[0]
            height = struct.unpack(">I", cdata[4:8])[0]

            print(f"\n[!] IHDR CRC 错误 → 文件: {path}")
            print(f"    宽度: {width}")
            print(f"    高度: {height}")
            print(f"    CRC(存储):  0x{crc_stored:08X}")
            print(f"    CRC(计算):  0x{crc_calc:08X}")
            print(f"    IHDR 偏移: {off}")

            # ★ 新逻辑：先爆高度 → 再爆宽度
            h_res, w_res = fix_ihdr_bruteforce_both(cdata, crc_stored, width, height)

            if h_res:
                print(f"\n最终结果：高度可能值 → {h_res}\n")
            elif w_res:
                print(f"\n最终结果：宽度可能值 → {w_res}\n")
            else:
                print("\n最终结果：高度、宽度均未找到匹配 CRC。\n")


def main():
    print("扫描 img/ 目录中 PNG 文件...\n")

    for fn in os.listdir(IMG_DIR):
        path = os.path.join(IMG_DIR, fn)
        if not os.path.isfile(path):
            continue

        with open(path, "rb") as f:
            if not f.read(8).startswith(PNG_SIG):
                continue

        analyze_png(path)


if __name__ == "__main__":
    main()
```
![](/assets/img/blog/20251128/misc32.png)     
**flag：** <kbd>ctfshow{fb09dcc9005fe3feeefb73646b55efd5}</kbd>
#### 2.33 Misc33.png
**锐评：** 长宽都不知道我怎么知道你有没有规矩。   
**logic:** 使用010editor打开文件搜打撤，发现crc校验失败，直接按照提示分别爆破长宽，得到的长宽为（978，142），将以上脚本改进可以得到png crc问题的一把梭脚本。
```python
import os
import struct
import zlib

IMG_DIR = "./img"

MIN_H = 1
MAX_H = 2000
MIN_W = 1
MAX_W = 2000

PNG_SIG = b"\x89PNG\r\n\x1a\n"


def parse_chunks(data):
    """解析 PNG chunk，返回 (length, type, data, crc, offset)"""
    if not data.startswith(PNG_SIG):
        raise ValueError("不是 PNG 文件")

    off = len(PNG_SIG)
    chunks = []

    while off + 8 <= len(data):
        length = struct.unpack(">I", data[off:off+4])[0]
        ctype = data[off+4:off+8]
        d_start = off + 8
        d_end = d_start + length
        if d_end + 4 > len(data):
            break

        cdata = data[d_start:d_end]
        crc = struct.unpack(">I", data[d_end:d_end+4])[0]

        chunks.append((length, ctype, cdata, crc, off))
        off = d_end + 4
        if ctype == b"IEND":
            break

    return chunks


# ---------- 第一阶段：爆高度 ----------
def brute_height(cdata, crc_stored, width):
    """爆破高度"""
    tail = cdata[8:]
    res = []

    for h in range(MIN_H, MAX_H + 1):
        new = struct.pack(">I", width) + struct.pack(">I", h) + tail
        if zlib.crc32(b"IHDR" + new) & 0xffffffff == crc_stored:
            res.append(h)

    return res


# ---------- 第二阶段：爆宽度 ----------
def brute_width(cdata, crc_stored, height):
    """爆破宽度"""
    tail = cdata[8:]
    res = []

    for w in range(MIN_W, MAX_W + 1):
        new = struct.pack(">I", w) + struct.pack(">I", height) + tail
        if zlib.crc32(b"IHDR" + new) & 0xffffffff == crc_stored:
            res.append(w)

    return res


# ---------- 第三阶段：二维爆破（高 × 宽） ----------
def brute_2d(cdata, crc_stored):
    """
    最终必杀技：宽度 + 高度双重不确定，双层爆破
    仅在前两个阶段失败时启用
    """
    tail = cdata[8:]
    res = []

    print("\n[!] 启动二维宽高爆破（可能较慢，但保证“一把梭”）")
    for w in range(MIN_W, MAX_W + 1):
        if w % 500 == 0:
            print(f"  → 进度：宽度 w={w}")

        for h in range(MIN_H, MAX_H + 1):
            new = struct.pack(">I", w) + struct.pack(">I", h) + tail
            if zlib.crc32(b"IHDR" + new) & 0xffffffff == crc_stored:
                res.append((w, h))

    return res


# ---------- 主分析函数 ----------
def analyze_png(path):
    with open(path, "rb") as f:
        data = f.read()

    chunks = parse_chunks(data)

    for length, ctype, cdata, crc_stored, off in chunks:
        crc_calc = zlib.crc32(ctype + cdata) & 0xffffffff
        if crc_calc == crc_stored:
            continue

        if ctype == b"IHDR":
            width = struct.unpack(">I", cdata[0:4])[0]
            height = struct.unpack(">I", cdata[4:8])[0]

            print(f"\n[!] IHDR CRC 错误 → 文件: {path}")
            print(f"    当前宽: {width}")
            print(f"    当前高: {height}")
            print(f"    CRC(存储): 0x{crc_stored:08X}")
            print(f"    CRC(计算): 0x{crc_calc:08X}")

            # ---------- 第一阶段：爆高度 ----------
            print("\n[*] ① 尝试爆破高度 ...")
            h_res = brute_height(cdata, crc_stored, width)
            if h_res:
                print(" [+] 找到高度:", h_res)
                return

            # ---------- 第二阶段：爆宽度 ----------
            print("[-] 高度无结果，② 尝试爆破宽度 ...")
            w_res = brute_width(cdata, crc_stored, height)
            if w_res:
                print(" [+] 找到宽度:", w_res)
                return

            # ---------- 第三阶段：二维最终爆破 ----------
            print("[-] 宽度无结果，③ 开始二维宽高联合爆破 ...")
            xy_res = brute_2d(cdata, crc_stored)

            if xy_res:
                print(" [+] 找到匹配 (宽, 高) 列表:", xy_res)
            else:
                print("[-] 宽高二维爆破仍未找到匹配 CRC（极少见，可能文件损坏）")


def main():
    print("扫描 img/ 目录中 PNG 文件...\n")

    for fn in os.listdir(IMG_DIR):
        path = os.path.join(IMG_DIR, fn)
        if not os.path.isfile(path):
            continue

        with open(path, "rb") as f:
            if not f.read(8).startswith(PNG_SIG):
                continue

        analyze_png(path)


if __name__ == "__main__":
    main()
```
![](/assets/img/blog/20251128/misc33.png)     
**flag：** <kbd>ctfshow{03070a10ec3a3282ba1e352f4e07b0a9}</kbd>
#### 2.30 Misc30.bmp
**锐评：** 如果你束手无策，你会干什么，你问什么屁话，当然是束手。   
**logic:** 由于这道题长宽全部被篡改，连crc都被改了，上面基于crc的爆破方式无法使用，只能另谋出路，IDAT 解压后长度 = (每行字节数+1) * 高度
→ 已知长度 + 猜宽 → 可推高度，filter byte 校验保证每行格式合法，CRC 校验保证 chunk 内容正确（如果 CRC 被篡改，需要先暴力爆破），最终写入新文件保证 IHDR 和 CRC 与真实数据一致，基于以上原理暴力破解，使用如下代码：
```python
import os
import struct
import zlib

IMG_DIR = "./img"
MIN_W = 1
MAX_W = 2000   # 你之前给定的最大宽
MIN_H = 1
MAX_H = 20000

PNG_SIG = b"\x89PNG\r\n\x1a\n"


# ============================================================
# ===============    基础功能：解析 PNG chunk    ===============
# ============================================================

def parse_chunks(data):
    if not data.startswith(PNG_SIG):
        raise ValueError("不是 PNG 文件")
    off = len(PNG_SIG)
    chunks = []
    while off + 8 <= len(data):
        length = struct.unpack(">I", data[off:off + 4])[0]
        ctype = data[off + 4:off + 8]
        d_start = off + 8
        d_end = d_start + length
        if d_end + 4 > len(data):
            break
        cdata = data[d_start:d_end]
        crc = struct.unpack(">I", data[d_end:d_end + 4])[0]
        chunks.append((length, ctype, cdata, crc, off))
        off = d_end + 4
        if ctype == b"IEND":
            break
    return chunks


def samples_per_pixel(color_type):
    return {
        0: 1,  # gray
        2: 3,  # RGB
        3: 1,  # indexed
        4: 2,  # gray+alpha
        6: 4,  # RGBA
    }.get(color_type, None)


def concat_idat(chunks):
    return b"".join(cdata for length, ctype, cdata, crc, off in chunks if ctype == b"IDAT")


# ============================================================
# ========= IDAT 解压 + 宽度盲爆，回推真实 (w,h) ===============
# ============================================================

def validate_by_idat_and_brutewidth(ihdr_cdata, idat_concat, crc_stored):
    width0 = struct.unpack(">I", ihdr_cdata[0:4])[0]
    height0 = struct.unpack(">I", ihdr_cdata[4:8])[0]
    bitdepth = ihdr_cdata[8]
    color_type = ihdr_cdata[9]
    tail = ihdr_cdata[8:]

    spp = samples_per_pixel(color_type)
    if spp is None:
        raise ValueError(f"Unsupported color type: {color_type}")

    try:
        raw = zlib.decompress(idat_concat)
    except Exception as e:
        print("    [!] IDAT 解压失败：", e)
        return []

    raw_len = len(raw)
    candidates = []

    for w in range(MIN_W, MAX_W + 1):
        bits_per_scanline = spp * bitdepth * w
        bytes_per_scanline = (bits_per_scanline + 7) // 8
        row_total = 1 + bytes_per_scanline

        if raw_len % row_total != 0:
            continue

        h = raw_len // row_total
        if not (MIN_H <= h <= MAX_H):
            continue

        # 快速检查 filter byte
        ok = True
        K = max(1, h // 50)
        for r in range(0, h, K):
            if raw[r * row_total] not in (0, 1, 2, 3, 4):
                ok = False
                break
        if not ok:
            continue

        # 完整检查
        for r in range(h):
            if raw[r * row_total] not in (0, 1, 2, 3, 4):
                ok = False
                break
        if ok:
            candidates.append((w, h))

    return candidates


# ============================================================
# ============= 原有 CRC 爆破：爆高度 & 爆宽度 ==================
# ============================================================

def brute_height(cdata, crc_stored, width):
    tail = cdata[8:]
    found = []
    for h in range(MIN_H, MAX_H + 1):
        new = struct.pack(">I", width) + struct.pack(">I", h) + tail
        if zlib.crc32(b"IHDR" + new) & 0xffffffff == crc_stored:
            found.append(h)
    return found


def brute_width(cdata, crc_stored, height):
    tail = cdata[8:]
    found = []
    for w in range(MIN_W, MAX_W + 1):
        new = struct.pack(">I", w) + struct.pack(">I", height) + tail
        if zlib.crc32(b"IHDR" + new) & 0xffffffff == crc_stored:
            found.append(w)
    return found


# ============================================================
# =========== 新增：生成修复后的 PNG（写新 IHDR） ==============
# ============================================================

def write_fixed_png(orig_path, chunks, new_width, new_height, new_crc):
    with open(orig_path, "rb") as f:
        data = f.read()

    sig = data[:8]
    out = bytearray()
    out += sig

    for (length, ctype, cdata, crc_old, off) in chunks:
        if ctype == b"IHDR":
            tail = cdata[8:]
            new_cdata = struct.pack(">I", new_width) + struct.pack(">I", new_height) + tail

            out += struct.pack(">I", len(new_cdata))
            out += b"IHDR"
            out += new_cdata
            out += struct.pack(">I", new_crc)
        else:
            out += struct.pack(">I", length)
            out += ctype
            out += cdata
            out += struct.pack(">I", crc_old)

    base = os.path.basename(orig_path)
    name, ext = os.path.splitext(base)

    out_path = os.path.join(
        os.path.dirname(orig_path),
        f"{name}_fixed_w{new_width}_h{new_height}.png"
    )

    with open(out_path, "wb") as f:
        f.write(out)

    print(f"    [+] 已生成修复 PNG: {out_path}")


# ============================================================
# =========== 新增：统一处理候选宽高 + 输出 CRC ================
# ============================================================

def finalize_candidates(path, chunks, candidates, ihdr_cdata):
    if not candidates:
        print("    [!] 未找到可用宽高")
        return

    print("\n    [+] 最终宽高候选列表：\n")

    tail = ihdr_cdata[8:]

    for (w, h) in candidates:
        new_ihdr = struct.pack(">I", w) + struct.pack(">I", h) + tail
        new_crc = zlib.crc32(b"IHDR" + new_ihdr) & 0xffffffff

        print(f"        - w={w}, h={h}, CRC=0x{new_crc:08X}")

        write_fixed_png(path, chunks, w, h, new_crc)


# ============================================================
# ==================== 主 PNG 分析流程 ========================
# ============================================================

def analyze_png(path):
    with open(path, "rb") as f:
        data = f.read()

    chunks = parse_chunks(data)
    idat_concat = concat_idat(chunks)

    for length, ctype, cdata, crc_stored, off in chunks:
        if ctype != b"IHDR":
            continue

        width = struct.unpack(">I", cdata[0:4])[0]
        height = struct.unpack(">I", cdata[4:8])[0]
        crc_calc = zlib.crc32(b"IHDR" + cdata) & 0xffffffff

        print(f"\n==================================================")
        print(f"[!] IHDR 文件: {path}")
        print(f"    IHDR 宽度: {width}, 高度: {height}")
        print(f"    CRC(存储): 0x{crc_stored:08X}")
        print(f"    CRC(计算): 0x{crc_calc:08X}")

        # CRC 不匹配 → 做爆破（原有逻辑）
        if crc_calc != crc_stored:
            print("    [*] CRC 不匹配 → 执行 CRC 爆破")

            hs = brute_height(cdata, crc_stored, width)
            ws = []

            if hs:
                candidates = [(width, h) for h in hs]
            else:
                ws = brute_width(cdata, crc_stored, height)
                if ws:
                    candidates = [(w, height) for w in ws]
                else:
                    print("    [!] CRC爆破失败，无法恢复尺寸")
                    return

            finalize_candidates(path, chunks, candidates, cdata)
            return

        # CRC 匹配 → 防篡改：用 IDAT 校验真实尺寸
        print("    [*] CRC 匹配，但可能被篡改 → 用 IDAT 盲爆校验真实尺寸")

        candidates = validate_by_idat_and_brutewidth(cdata, idat_concat, crc_stored)

        if candidates:
            print("    [+] IDAT 校验得到可能真实尺寸：", candidates)
        else:
            print("    [-] IDAT 校验失败 → 回退 CRC 爆破")

            hs = brute_height(cdata, crc_stored, width)
            ws = brute_width(cdata, crc_stored, height)

            candidates = [(width, h) for h in hs] + [(w, height) for w in ws]

        finalize_candidates(path, chunks, candidates, cdata)
        return


# ============================================================
# ======================= 扫描目录 ============================
# ============================================================

def main():
    print("扫描 img/ 目录中的 PNG 文件...\n")
    for fn in os.listdir(IMG_DIR):
        path = os.path.join(IMG_DIR, fn)
        if not os.path.isfile(path):
            continue
        with open(path, "rb") as f:
            if not f.read(8).startswith(PNG_SIG):
                continue
        analyze_png(path)


if __name__ == "__main__":
    main()
```
![](/assets/img/blog/20251128/misc34_fixed_w1123_h173.png)     
**flag：** <kbd>ctfshow{03e102077e3e5de9dd9c04aba16ef014}</kbd>
#### 未完待续...今天太晚了 有空再更新噢 宝子们 晚安