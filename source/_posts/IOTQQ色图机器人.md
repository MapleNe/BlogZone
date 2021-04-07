---
title: IOTQQ色图机器人
date: 2020-07-31 03:06:00
categories: 折腾
urlname: 46
tags:
- Windows
- 笔记
- Linux
- Macos
---
该项目已改名为OPQbot
###安装机器人程序
项目地址：[Github](https://github.com/IOTQQ/IOTQQ)
可搭载在Linux Windows Macos平台 路由器和树莓派支持
选择对应版本下载->[传送门](https://gitter.im/IOTQQTalk/IOTQQ)
![QQ截图20200731105329.png](https://i.loli.net/2020/07/31/JMq1L49HCWITVwY.png)
编辑`CoreConf.conf`文件在`Token`一行中填入你申请的Token。
申请地址[Gitter Developer](https://developer.gitter.im/docs/welcome),一个Token只能绑定一个QQ，注意
![](https://i.loli.net/2020/07/31/ZKIjbWP1AxdMtuV.png)
![](https://i.loli.net/2020/07/31/rdOUGoAI3CtLvNq.png)
Windows启动直接双击IOTbot.exe
Linux启动使用Chmod +x IOTBOT && ./IOTbot
启动出现`Everthing is ok`后打开http://IP:PORT/v1/Login/GetQRcode
扫码登录QQ

###安装机器人插件
项目地址:[Github](https://github.com/yuban10703/IOTQQ-color_pic)
申请Key https://api.lolicon.app/#/setu?id=apikey
下载Python3 https://www.python.org/downloads/ 
安装对应版本的Python3
将插件源码Git clone到本地 或者Zip Download,到项目地址输入
```
pip3 install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
```
然后修改config.json 把botqqs中的qq换成你bot的,webapi的话iotbot和py在一台机子上运行就不用修改,把superAdminQQ的值换成你qq,保存退出,然后双击sex_pic.py运行应该就行了....
![](https://camo.githubusercontent.com/86aee55480cdcdeac61887bd89e3f816a38a2b7a/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f797562616e31303730332f426c6f67496d67646174612f696d672f32303230303731343233313134322e706e67)
![QQ截图20200731110856.png](https://i.loli.net/2020/07/31/sEjGxIrC8t6fZLB.png)




