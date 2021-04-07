---
title: 使用Haproxy代理防止smtp发信泄露ip
date: 2020-03-17 14:40:30
categories: 折腾
urlname: 19
tags:
- 教程
---
Smtp发信会泄露源站ip，CDN无法防护，使用Haproxy就可以避免了
## Centos
```shell
yum -y install haproxy
```
## debian
```shell
echo deb http://httpredir.debian.org/debian wheezy-backports main | \
      sed 's/\(.*\)-sloppy \(.*\)/&@\1 \2/' | tr @ '\n' | \
      tee /etc/apt/sources.list.d/backports.list
#安装
apt-get update
apt-get install haproxy -t wheezy-backports
```

## 配置
清空文件内容
```shell
cd /etc/haproxy/
> haproxy.cfg
```
写入以下配置
```shell
global
ulimit-n  51200
defaults
log global
mode    tcp
option  dontlognull
timeout connect 1000ms
timeout client 150000ms
timeout server 150000ms
listen status
bind 0.0.0.0:1080
mode http
log global
stats refresh 30s
stats uri /admin?stats
stats realm Private lands
stats auth admin:password
stats hide-version
frontend ssin
bind *:465
#如果是普通模式，那这里就填25，如果是SSL模式，就需要填465
default_backend ssout
backend ssout
server server1 11.22.33.44 maxconn 204800
#这里的IP需要改成SMTP地址的IP，ping一下SMTP域名即可得到地址
```
设置为开机启动
```shell
service haproxy restart
chkconfig haproxy on
```

## 使用
在你的网站服务器下编辑`hosts`文件,写入你的中转服务器以及使用的smtp
```shell
vi /etc/hosts

127.0.0.1 localhost
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
22.33.44.55  smtp.qq.com
#22.33.44.55就是中转服务器的IP
```