---
title: Coding安装Hexo并推送到Github
date: 2020-03-06 15:22:00
categories: 折腾
urlname: 14
tags:
- 教程
---
今天还是要水下文章，这里说下，coding已经被腾讯收购了，所以叫Cloud Studio也是一样的
之所以使用Cloud Studio是因为简便，如果你有服务器的话可以不适用Cloud Studio
官网：[Cloud Studio](https://cloudstudio.net/)
自行注册

##总结
简单来说无非就几条命令，这里列一下，下面详细讲
```shell
npm install hexo-cli -g
hexo init Blog
cd Blog
npm install
hexo g
hexo d
```
##创建
注册完成之后先创建下工作空间
名称：必填，随意
预置：Nodejs
代码：空
创建

##安装
- 进入工作空间开始操作
打开控制台，输入指令
```shell
npm install hexo-cli -g
```
![1.png](https://i.loli.net/2020/03/06/JKA4y2cQwXlgCtS.png)
安装完成如下
![2.png](https://i.loli.net/2020/03/06/b7ryCI3eauhEFm9.png)

- 初始化hexo
```shell
hexo init blog
```
- CD到`blog`目录
```shell
cd blog
```
- 安装依赖
```shell
npm install
```
- 生成博客文件
```shell
hexo g
```
- 启动服务
```shell
hexo s
```
不过是cloud studio也看不到吧，这是多余的

##推送到github
- 配置推送信息
```
git config --global user.name "你的名字"
git config --global user.email "邮箱地址"
```
- 创建秘钥-全部默认回车
```shell
ssh-keygen -t rsa -C "your_email@mail.com"
```
key文件在你的根目录`.ssh`文件夹
- 将秘钥填入github仓库 deploy key
将`id_rsa.pub`文件中的`ssh key`填入仓库中
![3.png](https://i.loli.net/2020/03/06/Vb6MvxnPkJz1oDp.png)
验证是否连接成功
```shell
ssh -T git@github.com
```
出现你的名字或者邮箱即可
- 添加推送源
修改`_config.json`将其下`Mottoi`改为你的用户名以及仓库名·记住仓库名必须为`用户名.github.io`
```
deploy:
  type: git
  repository: https://github.com/Mottoi/Mottoi.github.io.git
  branch: master
```
- 推送
完成之后生成博客文件,并将其推送
```shell
hexo g
hexo d
```
 大功告成，你可以在仓库查看你的文件了