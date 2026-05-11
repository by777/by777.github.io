---
layout: post
title: Linux常用工具：grep/awk/sed
date: 2023-12-29 21:30:00 +0800
description: Linux常用工具：grep/awk/sed
img: post-2.jpg
tags: [cnblogs]
author: Bai Qi
---

# Linux常用工具

  * grep 文本过滤
  * sed steam editor 文本编辑工具
  * awk 格式化文本



# Ⅰ.grep

grep (global regular expression) 命令用于查找文件里符合条件的字符串或正则表达式。

## 命令组成
    
    
    grep [options] pattern [files]
    

逐个解释grep命令的各部分

  1. pattern：表示要查找的字符串或正则表达式
  2. files: 表示要查找的文件名，可以同时查找多个文件
  3. 常用选项见下表

option | 解释  
---|---  
-i | ignorecase  
-o | 仅仅显示匹配到的字符串本身  
-v | 反转，显示不能被模式匹配的行  
-E | 使用扩展的正则表达式  
-n | 显示匹配行的行号  
-r | 递归查找子目录中的文件  
-l | 只打印匹配的文件名  
-a /--text | 要忽略二进制的数据  
-w /--word-regexp | 只显示全字符合的列  
  
## b)基本正则表达式

正则表达式是一种用于匹配和操作文本的强大工具，它是由一系列字符和特殊字符组成的模式，用于描述要匹配的文本模式。正则表达式可以在文本中查找、替换、提取和验证特定的模式。  
正则表达式有3大常用功能

  1. 匹配字符
  2. 匹配次数
  3. 位置锚定



> **元字符**  
>  元字符(Metacharacter)是一类非常特殊的字符，它能够匹配一个位置或字符集合中的一个字符，元字符可以分为两种类型: 1.匹配位置的元字符 2.匹配字符的元字符

元字符 | 作用  
---|---  
^ | 用于模式的最左侧，^oldboy匹配以oldboy开始的**行**  
$ | 用于模式的最右侧  
^$ | 匹配空行  
. | 匹配任意一个有且仅有一个字符，不能匹配空行  
\ | 转义字符  
* | **匹配前一个字符** ，连续出现0此或1次以上，重复0次代表空，即匹配所有内容。a*表示匹配a0次或者多次  
.* | 组合符，匹配所有内容（一个文档所有的内容）  
^.* | 组合符，匹配任意多个字符开头的内容  
.*$ | 组合符，匹配任意多个字符结尾的内容  
[abc] | 匹配[]内的任意1个字符  
[^abc] | 匹配除了后面的所有字符，即除开abc的所有字符，注意写在[]里面的意义改变  
  
## 扩展正则表达式ERE

必须使用grep -E 才能生效

元字符 | 作用  
---|---  
+ | 匹配前一个字符1次或多次，a+表示匹配1个以上a  
[😕]+ | 匹配括号内的：或者/ 字符1次或多次  
? | 匹配前一个字符0次或多次  
|   
() | 分组过滤，表示被括起来的内容是一个整体  
a | 匹配前一个字符最少n次最大m次  
a | 匹配前一个字符最少n次  
a | 匹配前一个字符n次  
a | 匹配前一个字符最大m次  
  
## 修饰符（标记）

标记也称为修饰符，正则表达式的标记用于指定额外的匹配策略。  
标记不写在正则表达式里，标记位于表达式之外，格式如下：
    
    
    /pattern/flags
    

修饰符 | 含义 | 描述  
---|---|---  
i | ignore - 不区分大小写 | 将匹配设置为不区分大小写，搜索时不区分大小写: A 和 a 没有区别。  
g | global - 全局匹配 | 查找所有的匹配项。  
m | multi line - 多行匹配 | 使边界字符 ^ 和 $ 匹配每一行的开头和结尾，记住是多行，而不是整个字符串的开头和结尾。  
s | 特殊字符圆点 . 中包含换行符 \n | 默认情况下的圆点 . 是匹配除换行符 \n 之外的任何字符，加上 s 修饰符之后, . 中包含换行符 \n。  
  
# Ⅱ.awk

awk有文本格式化的能力
    
    
    awk [option] 'pattern[action]' file
    # awk 参数 '条件动作' 文件
    

  * 打印第一列数据


    
    
    awk '{print $1}' alex.txt
    # $0 代表所有列，没有使用任何模式，默认使用空格作为分隔符（多个空格视作一个）
    # $0代表所有列
    # $NF代表分割后的最后一列
    # 倒数第二列可以写作$(NF-1)
    

内置变量 | 解释  
---|---  
$n | 指定分隔符后，当前记录的第n个字段  
$0 | 完整的输入记录  
FS | 字段分隔符，默认是空格  
NF(Number of fields) | 分割后当前行一共有多少字段  
NR(Number of records) | 当前记录数，行数  
更多字段... | man awk  
      
    
    #1.一次输出多列
    awk '{print $1,$4,$5}' alex.txt
    
    #2.自定义输出内容
    # 注意：外层单引号，内层双引号
    awk '{print "第一列",$1,"第四列",$4,"第五列",$5}' alex.txt
    第一列 line1 第四列 line1 第五列 line1
    第一列 line2 第四列 line2 第五列 line2
    第一列 line3 第四列 line3 第五列 line3
    第一列 aaaaaaaa 第四列  第五列 
    第一列 bbb 第四列  第五列 
    

### awk参数

参数 | 解释  
---|---  
-F | 制定分割字符段  
-v | 定义或修改一个awk内部的变量  
-f | 从脚本中读取awk命令  
      
    
    # 利用内置变量NR表示行号，显示文件第5行。注意不需要加$
    awk 'NR==5' pwd.txt
    sync:x:4:65534:sync:/bin:/bin/sync
    
    
    
    # 利用awk取ip
    ifconfig eth0 | awk 'NR==2{print $2}'
    172.23.73.170
    
    
    
    # 指定awk分割符（-F）和输出分割符(-v OFS="\t")
    # 逗号会以空格输出
    awk -F ":" '{print "USER:", $1, "shell", $NF}' pwd.txt
    # 使用tab作为输出分隔符
    awk -F ":" -v OFS="\t" '{print "USER:", $1, "shell", $NF}' pwd.txt
    

### awk格式化-printf

  * printf和print最大的区别是需要指定format
  * format用于指定后面每个item的输出格式
  * printf不会自动打印换行符\n



### format的指示符

  * %c: 显示字符的ASCII码
  * %d: %i 十进制整数
  * %e: 以科学计数法打印
  * %s: 显示字符串
  * -: 左对齐，默认右对齐
  * +: 显示数值符号： printf "%+d"


    
    
    awk '{printf "%s\n", $1}' pwd.txt
    

# Ⅲ.sed

sed常用内置命令字符，用于对文件增删改查,sed 可依照脚本的指令来处理、编辑文本文件。  
Sed 主要用来自动编辑一个或多个文件、简化对文件的反复操作、编写转换程序等。
    
    
    sed [选项] [sed内置命令字符] [输入文件]
    

参数选项 | 解释  
---|---  
-n | 取消默认sed的输出，常与p一起使用  
-i | 直接把修改内容写入文件，不用-i修改的是内存数据  
-e | 多次编辑，不需要管道符了  
-r | 支持正则扩展  
sed的内置命令字符 | 解释  
---|---  
a | append，在指定行后添加一行/多行文本  
d | delete，删除匹配行  
i | insert，在指定行前面添加一行/多行文本  
p | print，打印匹配的字符，常与n一起使用  
s/正则/替换内容/g | 匹配正则内容并替换，结尾g表示全局匹配  
  
sed的匹配范围

范围 | 解释  
---|---  
空地址 | 全文处理  
单地址 | 指定文件某一行  
/pattern/ | 被模式匹配的每一行  
范围区间 | 10,20 10到20行，10,+5第10行下面5行，/pattern1/,/pattern2/  
步长 | 1~2 表示第1，3，5，7，9行，2~2两个步长，表示2，4，6，8行  
      
    
    #取消默认输出（-n），打印文件第2、3行的内容
    sed '2,3p' lufftcity.txt 
    # 需要
    My name is chaoge.
    I tench linux.
    I tench linux.
    I like play computer game.
    I like play computer game.
    My qq is 123456789.
    
    sed -n '2,3p' lufftcity.txt
    I tench linux.
    I like play computer game.
    
    # 过滤出含有linux的字符串
    sed -n '/linux/p' lufftcity.txt
    I tench linux.
    
    # 删除有game的行
    sed -n '/game/d' lufftcity.txt
    
    # 删除第5行到结尾
    sed '4,$d' lufftcity.txt
    My name is chaoge.
    I tench linux.
    I like play computer game.
    
    # 将文件的My替换His
    # ///可以替换成###或者@@@
    sed "s/My/His/g" lufftcity.txt
    
    # 使用-e组合命令，My替换成His，qq号码替换888888
    sed "s/My/His/g" -e "s/123456789/888888888/g" lufftcity.txt
    
    # 在文件第二行后追加AAA
    sed -i "2a AAA" lufftcity.txt
    
    # 在文件第2行前插入两行数据
    sed -i "2i HaHaHa line1\nWooWOoo line2" lufftcity.txt
    
    # 每一行都匹配，空地址
    sed -i "a------------------" lufftcity.txt 
    
    # sed 取linux IP地址
    root@XX14:~/linux_study# ifconfig eth0 
    eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
            inet 172.23.73.170  netmask 255.255.240.0  broadcast 172.23.79.255
            inet6 fe80::215:5dff:feb9:e08c  prefixlen 64  scopeid 0x20<link>
            ether 00:15:5d:b9:e0:8c  txqueuelen 1000  (Ethernet)
            RX packets 634  bytes 401476 (401.4 KB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 284  bytes 47334 (47.3 KB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
    ifconfig eth0 | sed -n "2p" | sed  "s/^.*inet//" | sed "s/netmask.*$//"
     172.23.73.170  
    ifconfig eth0 | sed -e "2s/^.*inet//"  -e "s/ netmask.*$//p" -n
    
