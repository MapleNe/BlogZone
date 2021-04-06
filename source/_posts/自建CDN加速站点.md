---
title: 自建CDN加速站点
date: 2020-03-24 05:11:46
categories: 折腾
urlname: cdn
tags:
- CDN
---
<!--markdown-->最近几天都是在优化站点访问速度，现在本站访问速度很快了，对我来说2秒加载完，本章是 关于如何自建cdn
使用宝塔控制面板，主要是容易，怎么装也不我用说了，需要两台服务器，一台源站一台CDN

##配置
在CDN服务器上安装宝塔面板，环境安装Nginx，CDN服务器一定要对源站的访问起到加速作用，这个不用我说大家都懂
编辑`hosts`文件添加你的源站IP、域名  例如

11.22.33.44 www.scorain.com
```
vi /etc/hosts
```
编辑完保存即可

在宝塔面板`网站`栏目添加一个网站，域名填写你要加速的域名，但又需要非WWW跳转WWW域名只需要填写两个域名开启301跳转即可
如果是WWw访问非WWW同上操作，并修改`hosts`需要加速的域名为非WWW域名
其他环境都不需要
![1](https://i.loli.net/2020/03/24/5eT6S8MJWQmsFj1.png)

配置反向代理并开启缓存，如果有`https`目标URL要使用对应协议头，发送域名保持原状
![2.png](https://i.loli.net/2020/03/24/w83rhiBYqfRMASK.png)

##解析
到DNS提供商（域名提供商）解析你的域名到CDN服务器即可访问你的CDN缓存节点

注：如果需要更新缓存需要使用：
```
yourdomain.com/purge/xxxx.html
```
来更新，在域名后面加purge/目标地址，例如我需要更新独立页面缓存
```
https://scorain.com/purge/kms.html
```

