---
title: Ubuntu开启Root密码登录
date: 2021-04-13 15:41:00
categories: 折腾
tags:
- 记录
---
编辑配置文件
```base
sudo vim /etc/ssh/sshd_config
```
`PermitRootLogin without-password ->  PermitRootLogin yes`
添加root密码
```base
sudo passwd root
```
重启ssh服务
```base
sudo systemctl ssh.service restart
```