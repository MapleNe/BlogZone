---
title: 关于源站泄露ip问题
date: 2020-03-11 11:47:17
categories: 笔记
urlname: 15
tags:
- 碎碎念
---
<!--markdown-->1. 源站签一个没有任何信息的ssl，并设置为默认网站，这是nginx问题
2. 不要使用本机smtp发信，邮件会显示你的ip
3. CDN使用http回源，不要协议跟随，源站不签ssl，小问题是后台进不去