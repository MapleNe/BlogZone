---
title: 使用客户端更好地管理typecho
date: 2020-02-27 09:20:00
categories: 笔记
urlname: 10
tags:
- 教程
---
刚写完一篇文章没多久我又开始瞎折腾了，这次用客户端发布文章

##准备
 打开博客的XmlRpc接口 (设置->基本->XMLRPC 接口)

下载[xmlrpc](https://github.com/kraity/typecho-xmlrpc)替换`/var/Widget/XmlRpc.php`

打开`xmlrpc`的`Markdown`语法编辑功能`https://example.com/admin/profile.php`

##安装
[应用下载](https://www.coolapk.com/apk/240898)

##文件上传
解决客户端上传文件失败问题
修改位置：`/var/Widget/Upload.php` 
```
#126行
if (!file_put_contents($path, $file['bytes'])) {}
 #改为
if (!file_put_contents($path, base64_decode($file['bytes']))) {}
```
如果你使用其他上传插件，以下针对插件修改
注意:新版本需要base64解密`base64_decode($file['bytes'])`

###OssForTypecho 阿里云OSS上传插件
修改位置：`Plugin.php`
```
#152行
$result = $ossClient->uploadFile($options->bucket, substr($path,1), $uploadfile);
 #改为
if (isset($file['tmp_name'])) { $result = $ossClient->uploadFile($options->bucket, substr($path, 1), $uploadfile); } else { $result = $ossClient->putObject($options->bucket, substr($path, 1), $uploadfile); }
```
```
#310行
return isset($file['tmp_name']) ? $file['tmp_name'] : (isset($file['bytes']) ? $file['bytes'] : (isset($file['bits']) ? $file['bits'] : ''));
 #改为
return isset($file['tmp_name']) ? $file['tmp_name'] : (isset($file['bytes']) ? base64_decode($file['bytes']) : (isset($file['bits']) ? $file['bits'] : ''));
```
```
#169行
'mime' => @Typecho_Common::mimeContentType($path)
 #改为
'mime' => (isset($file['tmp_name']) ? Typecho_Common::mimeContentType($file['tmp_name']) : $file['mime'])
```
###Qiniu File Typecho 的附件上传至七牛云存储中
修改位置：`Plugin.php`
```
#108行
$filename = $file['tmp_name']; if (!isset($filename)) return false;
 #删除
```
```
#116到127行
if ($error == null) .... else return false; 
 #替换为
if (isset($file['bytes'])) { list($ret, $error) = $upManager->put($token, $option->savepath . $file['name'], base64_decode($file['bytes'])); if ($error == null) { return array( 'name' => $file['name'], 'path' => $option->savepath . $file['name'] . ($option->imgstyle == '' ? '' : '-' . $option->imgstyle), 'size' => $file['size'], 'type' => $ext, 'mime' => $file['mime']//Typecho_Common::mimeContentType($option->savepath . $file['name']) ); } else { return false; } } else { // 上传文件 $filename = $file['tmp_name']; //if (!isset($filename)) return false; list($ret, $error) = $upManager->putFile($token, $option->savepath . $file['name'], $filename); if ($error == null) { return array( 'name' => $file['name'], 'path' => $option->savepath . $file['name'] . ($option->imgstyle == '' ? '' : '-' . $option->imgstyle), 'size' => $file['size'], 'type' => $ext, 'mime' => Typecho_Common::mimeContentType($filename) ); } else { return false; } }
```

###cosUploadV5 针对腾讯云cos v5更新 for Typecho
修改位置：`Plugin.php`
```
#164行
$file['bytes']
 #改为
base64_decode($file['bytes'])
```
##问题
闪退需要使用Android7+版本
关闭post和ua过滤
##截图
![Screenshot_20200227-173604_.png](https://i.loli.net/2020/02/27/InQgGLz5Om9vyXJ.png)