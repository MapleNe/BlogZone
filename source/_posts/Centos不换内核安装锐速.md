---
title: Centos不换内核安装锐速
date: 2020-03-20 07:18:30
categories: 折腾
urlname: 23
tags:
- 教程
---
使用指令查看内核，有一个3.10.....的内核，或者其他的版本
```
uname -r
```
在[锐速库](https://github.com/0oVicero0/serverSpeeder_kernel/blob/master/serverSpeeder.txt)中查看和你内核版本比较相近的内核版本，执行指令安装，将`3.10.0-229.1.2.el7.x86_64/x64`改为你选择的版本
```
wget --no-check-certificate -O appex.sh https://raw.githubusercontent.com/0oVicero0/serverSpeeder_Install/master/appex.sh && chmod +x appex.sh && bash appex.sh install '3.10.0-229.1.2.el7.x86_64/x64'
```
一路`Y`过去，启动了就恭喜你，失败了就重新找内核