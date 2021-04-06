---
title: Github部署Hexo源码记录
date: 2021-04-07 00:27:58
tags: 记录
---

### 使用的命令

配置推送部分

```shell
git init #初始项目
git add . #添加文件
git commit -m "" #添加说明
git remote add origin #添加远程地址
git push -u origin master #推送
```

生成密钥部分

```shell
ssh-genkey -t -C rsa "邮箱" #生成密钥
cd ~/.ssh  #查看密钥
```

配置全局账号部分

```shell
git config --global user.name "用户名"
git config --global user.email "邮箱"
```



### 命令步骤

1. 初始项目
2. 添加文件
3. 添加说明
4. 配置仓库
5. 配置密钥
6. 配置账号
7. 推送文件
8. 同步源码

### 部署流程

Local --> Github --> Cloudflare Deploy -->WebSite