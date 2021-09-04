---
title: SQL Server安装与卸载重装
date: 2021-09-4 01:39:09
categories: 折腾
tags: 
- 教程
- SQLServer
---
  视频教程时长比较长，建议开启1.5倍数观看，如看不清楚放慢速度即可。

建议先观看下文字教程的步骤再看视频。

### 安装教程

1. 下载解压SQLServer2012安装包，[点我下载](https://drive.scorain.com/个人仓库/软件/SQL%2BServer%2B2012%2B(64bit).zip)

2. 解压完成之后右键`sql.iso`文件选择装载.

3. 进入装载的iso文件中右键`setup`使用管理员模式运行

4. 在安装向导界面左边栏选择`安装`选项![安装向导](https://drive.scorain.com/个人仓库/博客文件/pic/1.png)

5. 如无网络安装直接下一步，有网络直接更新即可，等待`安装安装程序文件`加载完毕点击`安装`开始`下一步`。

6. `安装程序支持规则`检测完毕`下一步`。

7. `产品密钥`界面选择`输入产品密钥`密钥为：`FH666-Y346V-7XFQ3-V69JM-RHW28`，`下一步`。

8. `许可条款`勾选`我接受许可条款`，`下一步`。

9. `设置角色`默认不变`下一步`。

10. `功能选择`全选功能，`共享功能目录和共享功能目录(x86)`可更换到除C盘外的盘中，设置完成可`下一步`。

    `注意：部分系统中没有安装.NET3.5可能会导致某些功能安装失败。需要自行安装`

11. `安装规则`检测无错误，`下一步`。

12. `实例配置`实例根目录可更换到除C盘外的盘区中。配置完成，`下一步`。

13. `空间要求`，`下一步`。

14. ` 数据库引擎配置`身份验证使用`Windows身份验证模式(默认)`，指定SQL Server管理员点击`添加当前用户`，`下一步`。

15. `添加当前用户`

16. `Reporting services`默认直接`下一步`。

17. `分布式重播控制器`添加当前用户，`下一步。`

18. `最后几项`无需更改默认`下一步`开始`安装即可`，安装过程可能需要40-60分钟。

#### 视频教程

 <video id="movies" src="https://drive.scorain.com/个人仓库/博客文件/SQLSERVERINSTALL.mp4" autobuffer="true" controls="" width="100%"></video>



### 卸载教程

软件安装失败之后需要重新安装，其中出现的问题可能是无法更改目录，或者是其他问题。导致这些问题的原因都是软件没有卸载干净。

1. 打开`windows设置-应用`找到`Microsoft SQL Server 2012(64位)`点击卸载，选择删除。![](https://drive.scorain.com/个人仓库/博客文件/pic/2.png)

2. 跟着向导一步一步操作。

3. `选择实例`选择你要卸载的实例。

4. `选择功能`全部选择，`下一步`。

5. 点击`删除`

6. ![](https://drive.scorain.com/个人仓库/博客文件/pic/3.png)

7. 完成之后重启计算机！

   #### 彻底卸载（推荐），需完成上面的操作

   按键盘`Win+R`输入
   `regedit`打开注册表。!>家庭版没有此功能。

   1. 彻底删除SQL Server：

      - hkey_local_machine\software\Microsoft\MSSQLServer
      - hkey_local_machine\software\Microsoft\Microsoft SQL Server
      - hkey_current_user\software\Microsoft\Microsoft SQL Server
      - hkey_current_user\software\Microsoft\MSSQLServer
      - hkey_local_machine\system\currentcontrolset\control\session manager\pendingfilerenameoperations

   2. 注册表中的相关信息删除：

      - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer

      - HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\MSDTC

      - HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager中找到PendingFileRenameOperations项目，并删除它。这样就可以清除安装暂挂项目

      - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\setup

        删除ExceptionComponents

   3. 运行注册表,删除如下项：

      - HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server
      - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server
      - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer

   4. 删除完成重启计算机！

   5. 进入`windows设置-应用`删除`VS和SQL`组件![](https://drive.scorain.com/个人仓库/博客文件/pic/4.png)![](https://drive.scorain.com/个人仓库/博客文件/pic/5.png)

   6. 删除`C:\Program Files\`中Microsoft SQL Server目录

   7. 删除`C:\Program Files(x86)\`中Microsoft SQL Server目录

   8. 删除共享功能目录和实例目录

   9. 使用工具（管理员模式）清除配置缓存，[点击下载](https://drive.scorain.com/个人仓库/软件/SqlServer卸载工具集合.zip)，清除完成之后重启可重新设置安装目录

   10. 重启计算机！

      ![](https://drive.scorain.com/个人仓库/博客文件/pic/7.png)
   
      ![](https://drive.scorain.com/个人仓库/博客文件/pic/6.png)
   
       

