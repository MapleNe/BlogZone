---
title: Termux安装Nodejs Git
date: 2020-03-26 12:34:41
categories: 折腾
urlname: termux
tags:
- 教程
- Linux
---
<!--markdown-->标题是这么写的，不过只是前提，关键还是要用Hexo来搭建个人博客啦
至于怎么搭建的话，我这里就不说了，还是看另一篇文章吧，操作步骤都是一样的
[Coding安装Hexo并推送到Github](https://www.scorain.com/van/14.html)

##准备一下
如果你还不知道什么是Termux的话，还是看看下面这段描述吧
>Termux是一个Android下一个高级的终端模拟器, 开源且不需要root, 支持apt管理软件包，十分方便安装软件包, 完美支持Python, PHP, Ruby, Go, Nodejs, MySQL等。随着智能设备的普及和性能的不断提升，如今的手机、平板等的硬件标准已达到了初级桌面计算机的硬件标准, 用心去打造完全可以把手机变成一个强大的工具.

简单来说就是你可以把Android手机当做Linux来用，毕竟是Linux内核嘛。
这里是Termux的安装包下载地址
[酷安Termux](https://www.coolapk.com/apk/com.termux)

##开始安装吧
如果你完成了简单介绍和安装，你已经对Termux有个大概的了解了
打开Termux『需要科学上网，喜欢搞♂机的都有一个』
无法打开安装的话用这个[完整包](https://tonyij.coding.net/s/550ac343-e525-458a-b396-084b3c3996b5)吧

等待环境安装完成，完成之后可以开始执行命令了
切换到清华源
```
sed -i 's@^\(deb.*stable main\)$@#\1\ndeb https://mirrors.tuna.tsinghua.edu.cn/termux/termux-packages-24 stable main@' $PREFIX/etc/apt/sources.list
sed -i 's@^\(deb.*games stable\)$@#\1\ndeb https://mirrors.tuna.tsinghua.edu.cn/termux/game-packages-24 games stable@' $PREFIX/etc/apt/sources.list.d/game.list
sed -i 's@^\(deb.*science stable\)$@#\1\ndeb https://mirrors.tuna.tsinghua.edu.cn/termux/science-packages-24 science stable@' $PREFIX/etc/apt/sources.list.d/science.list
apt update && apt upgrade
```
安装nodejs
```
pkg install nodejs -y
```
安装Git
```
pkg install git -y
```
安装Hexo  这里需要科学上网
```
npm install hexo-cli -g
```