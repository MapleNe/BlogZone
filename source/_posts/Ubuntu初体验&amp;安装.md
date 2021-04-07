---
title: Ubuntu初体验&amp;安装
date: 2020-02-27 04:12:00
categories: 笔记
urlname: 8
tags:
- 教程
---
最近突发奇想想装个Linux系统用，第一次用Linux系统我选择Ubuntu发行版，主要是第一次装，没什么经验，安装系统过程磕磕碰碰，这里做个总结，避免忘记

## 准备
一个8G或以上的U盘
[Ubuntu](http://mirrors.ustc.edu.cn/ubuntu-releases/)镜像
[Balena Etcher](https://www.balena.io/etcher/)镜像烧录工具
一台电脑或者虚拟机

### 虚拟机不需要U盘

## 制作
打开`Balena Etcher`，点击`Select image`选择镜像，插入U盘点击`Flash`等待制作完成
![10](https://i.loli.net/2020/02/27/nsYhd6C95KU4WlI.png)
![10](https://i.loli.net/2020/02/27/rS4GwdRB9VkTo1e.png)

## 安装
主机关机重启进入Bios设置U盘启动，具体操作[百度](https://baidu.com)主板型号
启动之后选择`Install Ubuntu`
按照自己所需选择语言
![1](https://i.loli.net/2020/02/27/g6wOZ2Nz1CxJiRU.png)
拔掉网线选择最小安装能安装更快
![2](https://i.loli.net/2020/02/27/WVu1zftspxE83eH.png)
全新安装
![3](https://i.loli.net/2020/02/27/dbYJZf1m9CjlXtF.png)
密码是必要的
![4](https://i.loli.net/2020/02/27/r1Pv2zN47TmAudW.png)
等待安装完成
![5](https://i.loli.net/2020/02/27/vesEqMt6j21GD9i.png)
>分区是非必须的，全部分配给`/`根目录就行