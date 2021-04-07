---
title: Nodecache免费CDN加速
date: 2020-03-08 11:23:00
categories: 折腾
urlname: 14-1
tags:
- CDN
---
今天网站被CC和DD了，CC整不住我网站就用DD，真实蛮恶心的
这次套个NodeCache的CDN，网站打开速度比之前好了很多，注册还送1000G流量
请务必`使用Aff注册`才会有1000G流量,点击下方链接即可
注册请使用`域名邮箱 outlook gmail或其他邮箱`，QQ不支持
官网：[nodecache](https://console-api.nodecache.com/f?aff=4xDqy4)

## 介绍
>Nodecache致力于为客户提供一站式的在线业务加速服务，以场景化CDN为核心，为客户提供DNS、HTTPS/SSL证书、多媒体处理（WebP 自适应、H.265 自适应等）等服务

## 使用
在使用之前你必须要有一个ssl证书，如果你使用的是宝塔面板，并且已经启动ssl可以在ssl设置选项复制证书
将你的`key`和`pem`填入
![1.png](https://i.loli.net/2020/03/08/WnqVuFc3b5Dd7CT.png)

添加完成之后可以进入`CDN`页面添加域名信息
![2.png](https://i.loli.net/2020/03/08/X4RBcQzPwD1jpOm.png)
![3.png](https://i.loli.net/2020/03/08/8ByfmYns5HM6kAN.png)
选择`亚太优化`，创建完成之后会得到一个`CNAME`解析值，将域名解析即可

将ssl证书应用到这里，否则无法打开带有`https`协议的网站
![4.png](https://i.loli.net/2020/03/08/mnGdoHVwzpCieJk.png)

## 补充
若是无法正常使用记得截图给博主看看
