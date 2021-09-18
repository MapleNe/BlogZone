---
title: Windows10家庭版转专业版
date: 2021-04-17 14:18:22
categories: 折腾
tags:
- 激活
- Windows
---

**注意：品牌机默认是消费者版镜像，需要另外升级成商业版才能转换**

### 更换密钥：

![QQ截图20210417143643.png](https://i.loli.net/2021/04/17/JfO7kc1nieylzNC.png)

MH37W-N47XK-V7XM9-C7227-GCQG9

W269N-WFGWX-YVC9B-4J6C9-T83GX

NPPR9-FWDCX-D2C8J-H872K-2YT43

NYW94-47Q7H-7X9TT-W7TXD-JTYPM

NJ4MX-VQQ7Q-FP3DB-VDGHX-7XM87

VK7JG-NPHTM-C97JM-9MPGT-3V66T

DR9VN-GF3CR-RCWT2-H7TR8-82QGT

W269N-WFGWX-YVC9B-4J6C9-T83GX

**密钥不能更换版本多试试别的密钥**



### KMS激活

一般用KMS激活或者用密钥激活，为了不出现别的什么问题，直接使用kms激活

先更换为KMS密钥

```shell
cd C:\Windows\System32
cscript slmgr.vbs /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX
```

然后激活

```shell
cd C:\Windows\System32
cscript slmgr.vbs /skms kms.loli.best
cscript slmgr.vbs /ato
cscript slmgr.vbs /xpr
```

Enjoy！

#### 软件激活

[下载工具](https://drive.scorain.com/个人仓库/软件/aactportablechs3264w.zip)可激活Windows和Office

直接激活即可

![](https://i.loli.net/2021/04/17/7rh2sxcvTIN4bnl.png)