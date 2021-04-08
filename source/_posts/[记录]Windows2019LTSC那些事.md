---
title: [记录]Windows2019 LTSC那些事
date: 2020-03-19 11:34:00
categories: 折腾
tags:
- 笔记
---
重置系统装机已经很长时间了，最开始的时候还是使用的小白一键装机，到后来的PE装机，成功得把系统 ~~装废了~~ 装好了，不过之前主要装的还是比较正常的家用系统，对于企业用系统还是比较懵的，总是因为一些操作导致引导失败找不到系统什么的，还是菜的一批

## 记录
使用Windows 2016 升级Windows 2019
目前使用的Windows2019，之前使用2016，系统是阉割过的，找不到PowerShell因此在itellyou找到一个2019,系统升级到2019导致的系统菜单打不开，各种错误
![QQ截图20200319192535.png](https://i.loli.net/2020/03/19/JmrhVoYAnkI1SR5.png)
这是之前855m的阉割Windows 2016系统，使用很流畅，适合日常用，不适合喜欢折腾的新手。
下面这张是itellyou下载的4GB原版镜像
![QQ截图20200319192753.png](https://i.loli.net/2020/03/19/tLSG7a1d9NjyFpM.png)

文件大小区别还是很大的，那么本站作为技术博客(个人认为)当然也得拿出点什么小技巧

## 注意事项
不会装系统的小白还是乖乖百度一下怎么制作启动盘以及重装系统吧
1. 原版系统可以在[Itellyou](https://msdn.itellyou.cn/)找到
2. Windows 2019 Ltsc或者类似的企业长期服务版，需要使用dism++的windows to go来加载系统
3. ESD文件需要使用WinNT来释放镜像
4. 不要把软件都装在C盘，这样会导致系统加载速度变慢，当然有独立的SSD固态硬盘最好

## 一些小东西
Windows 2019 安装微软商店
打开网址https://store.rg-adguard.net/ 
以`PackageFamilyName`方式搜索`Microsoft.WindowsStore_8wekyb3d8bbwe`
下载这些文件
![1.png](https://i.loli.net/2020/03/19/ysklPmQYGHfOoe8.png)
创建一个文件夹，使用PowerShell到此目录下执行命令以安装微软商店，注意使用管理员模式
```
Add-AppxPackage *
```


