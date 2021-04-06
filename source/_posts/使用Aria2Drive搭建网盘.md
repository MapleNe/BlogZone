---
title: 使用Aria2Drive搭建网盘
date: 2020-03-01 14:59:00
categories: 折腾
urlname: 27
tags:
- 教程
---
<!--markdown-->这个是群友推荐的，使用aria2+oneindex+rclone搭建下载自动上传到onedrive的网盘，原址[Aria2Drive：一键搭建自己的网盘](https://pa.ci/95.html)

##安装
因为作者适配的是`debian`所以我使用的是`debian`系统搭建的，不过作者理论上说支持ubuntu等，只要删除相关代码就行了
```shell
wget --no-check-certificate -O Aria2Drive.sh https://raw.githubusercontent.com/uselibrary/Aria2Drive/master/Aria2Drive.sh && chmod +x Aria2Drive.sh && bash Aria2Drive.sh
```
复制粘贴运行脚本之后会安装以下软件
基础性软件：`vim git curl wget unzip`
维持性软件：`nginx php-fpm php-curl`
功能性软件：`aria2 AriaNG Oneindex rclone`
安装过程中需要填写信息

 1. 域名
 2. 邮箱
 3. 密码
 4. 是否开启SSl

安装完成只会需要你配置`rclone`来挂载你的onedrive
```
No remotes found - make a new one
n) New remote
s) Set configuration password
q) Quit config
n/s/q> n   #选择N新建新配置
```
```
name> onedrive #配置名称，后面要用到
#选择网盘类型
Type of storage to configure.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
 1 / A stackable unification remote, which can appear to merge the contents of several remotes
   \ "union"
 2 / Alias for a existing remote
   \ "alias"
 3 / Amazon Drive
   \ "amazon cloud drive"
 4 / Amazon S3 Compliant Storage Provider (AWS, Alibaba, Ceph, Digital Ocean, Dreamhost, IBM COS, Minio, etc)
   \ "s3"
 5 / Backblaze B2
   \ "b2"
 6 / Box
   \ "box"
 7 / Cache a remote
   \ "cache"
 8 / Dropbox
   \ "dropbox"
 9 / Encrypt/Decrypt a remote
   \ "crypt"
10 / FTP Connection
   \ "ftp"
11 / Google Cloud Storage (this is not Google Drive)
   \ "google cloud storage"
12 / Google Drive
   \ "drive"
13 / Hubic
   \ "hubic"
14 / JottaCloud
   \ "jottacloud"
15 / Local Disk
   \ "local"
16 / Mega
   \ "mega"
17 / Microsoft Azure Blob Storage
   \ "azureblob"
18 / Microsoft OneDrive
   \ "onedrive"
19 / OpenDrive
   \ "opendrive"
20 / Openstack Swift (Rackspace Cloud Files, Memset Memstore, OVH)
   \ "swift"
21 / Pcloud
   \ "pcloud"
22 / QingCloud Object Storage
   \ "qingstor"
23 / SSH/SFTP Connection
   \ "sftp"
24 / Webdav
   \ "webdav"
25 / Yandex Disk
   \ "yandex"
26 / http Connection
   \ "http"
Storage> 18 #选择18，Microsoft OneDrive 安装选项不同，这是演示，安装过程请对准序号。
```
配置token

在[rclone](https://rclone.org/downloads/)下载电脑版本，打开cmd命令提示行输入以下指令
```
rclone authorize "onedrive"
```
认证获取token
```
Paste the following into your remote machine --->
{"access_token":"xxxx"}  #请复制{xx}整个内容(包括花括号)，后面需要用到
<---End paste
```
填入token
```
** See help for onedrive backend at: https://rclone.org/onedrive/ **

Microsoft App Client Id
Leave blank normally.
Enter a string value. Press Enter for the default ("").
client_id> #留空
Microsoft App Client Secret
Leave blank normally.
Enter a string value. Press Enter for the default ("").
client_secret> #留空
Edit advanced config? (y/n)
y) Yes
n) No
y/n> n
Remote config
Use auto config?
 * Say Y if not sure
 * Say N if you are working on a remote or headless machine
y) Yes
n) No
y/n> n  #选择n
For this to work, you will need rclone available on a machine that has a web browser available.
Execute the following on your machine:
    rclone authorize "onedrive"
Then paste the result below:
result> {"access_token":""}  #输入之前在客户端授权的内容
```

##补充

 1. 填入邮箱认证SSL证书会给你的邮箱发送一封邮件认证，务必填写正确
 2. Aria2密码请使用大小写字母以及数字标点符号，防止出错
 3. 安装完成后需要重启服务器以确保所有服务运行
 4. 如何安装请查看[Github](https://github.com/donwa/oneindex)

##说明
下载文件会储存在`/home/downloads/`文件夹
Aria2密码储存在`/etc/aria2/aria2.conf`
systemd会负责aria2的进程守护，`systemctl start/stop/enable/disable/restart aria2`

##使用
AriaNG地址为`你的域名/AriaNG`
需要配置`Aria RPC`![QQ截图20200301232915.png](https://i.loli.net/2020/03/01/RlxcVjMtPmUHgBC.png)
下载完成之后将会被上传到onedrive中，有时上传后没有删除下载文件，需要自己删除

