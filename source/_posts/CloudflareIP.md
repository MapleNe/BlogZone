---
title: Cloudflare自选IP优化线路
date: 2021-04-15 01:04:07
caregories: 折腾
tags:
- 教程
- Cloudflare
---
使用[Cloudflare](https://cloudflare.com)自选IP之前要先注册账号​…
自选IP可以根据三网网络进行选择最优线路，智能解析推荐使用腾讯的DnsPod，可配置不同网络线路解析不同IP达到最优效果。

### 测试Cloudflare IP
项目地址：[Github](https://github.com/badafans/better-cloudflare-ip)

### Windows版本
windows批处理全自动无门槛操作
fping-4.2 for win32 修改版（基于 msys2.0 修改编译）点击下载[Windows版本](https://proxy.freecdn.workers.dev/?url=https://github.com/badafans/better-cloudflare-ip/releases/latest/download/windows.zip)

### Linux版本
linux shell脚本+fping

具体使用流程，需要编译里面 fping 4.2 修改版本，另外需要系统安装curl支持。

下载修改过的源码 fping-4.2.tar.gz 点击下载Linux源码

具体编译使用流程如下
```she
curl https://github.com/badafans/better-cloudflare-ip/releases/latest/download/linux.tar.gz -o linux.tar.gz
tar -vxf linux.tar.gz
cd linux
./configure
make
cd src
sudo ./cf.sh
```
### Android版本
安装termux，完整复制下方链接粘贴到termux并回车，后续运行只需输入./cf.sh并回车即可
```shell
curl https://proxy.freecdn.workers.dev/?url=https://raw.githubusercontent.com/badafans/better-cloudflare-ip/master/shell/cf.sh -o cf.sh && chmod +x cf.sh && ./cf.sh
```
### OpenWrt版本
完整复制下方链接粘贴到openwrt shell并回车，后续运行只需输入./cf-openwrt.sh并回车即可
```shell
curl https://proxy.freecdn.workers.dev/?url=https://raw.githubusercontent.com/badafans/better-cloudflare-ip/master/shell/cf-openwrt.sh -o cf-openwrt.sh && chmod +x cf-openwrt.sh && ./cf-openwrt.sh
```

## 使用
使用Cloudflare第三方合作平台Cname接入，正确添加域名后将域名解析到最优IP即可