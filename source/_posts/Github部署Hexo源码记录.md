---
title: Github部署Hexo源码记录
date: 2021-04-07 00:27:58
categories: 笔记
tags:
- 记录
- 教程
---



###  使用的命令

配置推送部分

```shell
git init #初始项目
git add . #添加文件
git commit -m "" #添加说明
git remote add origin #添加远程地址
git push -u origin master #推送
git pull origin master #同步远程仓库代码到本地
```

生成密钥部分

```shell
ssh-keygen -t rsa -C "邮箱" #生成密钥
cd ~/.ssh  #查看密钥
```

配置全局账号部分

```shell
git config --global user.name "用户名"
git config --global user.email "邮箱"
```



###  命令步骤

1. 初始项目
2. 添加文件
3. 添加说明
4. 配置仓库
5. 配置密钥
6. 配置账号
7. 推送文件
8. 同步源码

###  部署流程

Local --> Github --> Cloudflare Deploy -->WebSite

服务器不知道被哪个憨批Ddos了，转战Cloudflare新出的Pages



## 教程

部署环境，安装Nodejs和Git。

#### 初始化Hexo

```shell
npm install hexo-cli -g ##安装Hexo
hexo init ##初始化博客
```



#### 部署Github远程仓库

创建一个仓库，并复制SSH链接，所有指令都需要进入博客源码文件夹执行，初始化的项目会带有(master)标识

```shell
git init  ##初始化项目
git remote add origin SSH链接 ## 添加远程仓库
git config --global user.name "名称" ##添加全局用户名
git config --global user.email "邮箱" ##添加全局邮箱
```

生成一个SSH密钥并部署到Github仓库

```shell
ssh-keygen -t rsa -C "邮箱" #生成密钥
cd ~/.ssh  #查看密钥
```

复制`.pub`文件里的密钥，将其添加到[个人资料](https://github.com/settings/keys)的`SSH and GPG keys`中

#### 推送文件到Githzub仓库

进入项目文件夹

```shell
git add . ##添加文件到.git文件中
git commit -m "update"  ##添加说明，这一步是必须的
git push -u origin master  ##推送到仓库中 第一次需要加-u参数，后面不必
```



### 将博客部署到Vercel中

1. 使用Github登陆[vercel](https://vercel.com)
2. 新建一个项目选择你的源码仓库
3. `FRAMEWORK PRESET`选择Hexo 其他默认
4. 点击Deploy确认部署

![image.png](https://i.loli.net/2021/04/11/t1oVSqB8pf547zL.png)