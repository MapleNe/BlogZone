---
title: 爷关更-没用小技巧-U盘换图标
date: 2021-01-26 05:11:00
categories: 折腾
urlname: 54
tags:
- 小技巧
---
<!--markdown-->日常没用小技巧+1，给U盘换个图标是不是感觉就提升了两个档次？
工具网址：http://www.bitbug.net/

将你准备的图片在工具网址转换为64x64的ico图片并将图片放入U盘中
在U盘新建一个文本并命名为`autorun.inf`
写入代码
```
[autorun]
icon=你的图片名字带后缀,0
```
![1.png](https://i.loli.net/2021/01/26/WZDx1gLy3iNjwFS.png)
图片文件和autorun文件在根目录
保存之后重新插拔U盘就能看到你设置的图片了
之后再将两个文件隐藏即可