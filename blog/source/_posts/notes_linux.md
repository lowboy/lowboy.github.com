layout: post
title: Notes About Linux
date: 2014-05-10 16:49:09
categories: 笔记
tags: [linux,积累,学习笔记]
---
<!--more-->
##常用命令##
1. 压缩命令：

	命令格式：tar  -zcvf   压缩文件名.tar.gz   被压缩文件名
   	可先切换到当前目录下。压缩文件名和被压缩文件名都可加入路径。


2. 解压缩命令：

	命令格式：tar  -zxvf   压缩文件名.tar.gz
	命令格式：tar  -jxvf   压缩文件名.tar.bz2
	解压缩后的文件只能放在当前的目录

##bash脚本##

&emsp;&emsp;首先,bash文件的开头是`#!/bin/bash`,表示运行调用。
然后呢，如果使用*bash*，一般也是进行批处理。
常用的命令格式有
```sh
```
```sh
do
command
done
```
```sh
for arg in [list]
for((i=1;i<10;++i))
while[] #多条命令时，以最后一条为准
```
```sh
if(condition1)
then command1
else command2 #else if 可简写为elif
fi
```
```sh
case "$var" in
        "$condition1")
            command...
        ;;
        "$condition2")
            command...
        ;;
        ...
        esac
```

命令样例
```sh
print_args()  
{  
    for arg in "$@"  
    do  
        echo $arg  
    done  
}  
print_args 1 2 3 4  
print_args "this is a test"  
<span style="color: #000000;">print_args this is a test</span>
```
```sh
AREAS=(1901 1902 1903 1904 1905 1906 1907   1908 1909 1910 1911 1912 1913)  
NAMES=(南京 无锡 徐州 常州 苏州 南通 连云港 淮安 盐城 扬州 镇江 泰州 宿迁)  
NUM_OF_AREAS=13  
area_name_of()  
{  
    for ((I=0; I<$NUM_OF_AREAS; ++I))  
    do  
        if [ "$1" == "${AREAS[I]}" ]; then  
            echo "${NAMES[I]}"  
        fi  
    done  
}  
echo $(area_name_of 1903)  
for AREA in ${AREAS[*]};  
do  
    echo $AREA $(area_name_of $AREA)  
done
```
```sh
for i in {1..5}  
do  
   echo "Welcome $i times" #这种思想挺重要
done
```
批量后接_MED重命名
```sh
for i in *.jpg;
do mv "$i" "${i%.jpg}_MED.jpg" ;
done
```
批量替换特定词汇重命名
```sh
for i in *.jpg;
do mv "$i" "${i%_MED.jpg}_LRG.jpg" ;
done 
```
