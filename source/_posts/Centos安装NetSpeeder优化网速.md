---
title: Centos安装NetSpeeder优化网速
date: 2020-03-23 11:40:05
categories: 折腾
urlname: 28
tags:
- Linux
---
net-speeder可以在高延迟不稳定链路上优化单线程下载速度，消耗双倍流量降低延迟

##安装
```
wget https://github.com/snooda/net-speeder/archive/master.zip&&unzip master.zip&&yum install epel-release -y&&cd net-speeder-master&&sh build.sh&&yum install screen -y&&screen ./net_speeder eth0 "ip"
```
将`eth0`改为你网卡名称，使用命令`ifconfig all`查看,若是提示`command not found`请执行指令
```
yum install net-tools
```

安装过程中报错，安装lib即可
```
yum install libpcap*
yum install libnet*
```