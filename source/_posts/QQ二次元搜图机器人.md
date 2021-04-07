---
title: QQ二次元搜图机器人
date: 2020-02-27 06:34:00
categories: 笔记
urlname: 9
tags:
- 教程
---
`CQ-picfinder-robot`插件由[神代綺凜](https://moe.best)使用nodejs编写（开源）
项目地址：[Github](https://github.com/Tsuk1ko/CQ-picfinder-robot)
该插件需要配合`酷Q`使用，并且需要启动`CoolQ HTTP API`插件，并将配置文件`use_ws`设置为`true`
详情查看[官方使用文档](https://cqhttp.cc/docs/4.10/#/Configuration)
![Screenshot_20200228-151211_QQ.png](https://i.loli.net/2020/02/28/RDZA7TwFU1gNs4V.png)

>这是一个以 Nodejs 编写的酷Q机器人插件，用于搜图、搜番、搜本子，并夹带了许多娱乐向功能

##安装
###酷Q支持Docker一键配置，先安装Docker
```
#CentOS 6
rpm -iUvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
yum update -y
yum -y install docker-io
service docker start
chkconfig docker on

#CentOS 7、Debian、Ubuntu
curl -sSL https://get.docker.com/ | sh
systemctl start docker
systemctl enable docker
```
安装酷Q
```
#酷QAir版
docker run --name wine-coolq -d \
-v /coolq:/home/user/coolq \
-p 9000:9000 \
-p 6700:6700 \
-e VNC_PASSWD=123456 \
richardchien/cqhttp

#酷QPro版
docker run --name wine-coolq -d \
-v /coolq:/home/user/coolq \
-p 9000:9000 \
-p 6700:6700 \
-e VNC_PASSWD=123456 \
-e COOLQ_URL=https://dlsec.cqp.me/cqp-tuling \
richardchien/cqhttp
```
###参数说明
```
-p 将内部的Web运行端口9000映射到外部的9000，可自行修改端口。
-v 将内部酷Q和其数据文件夹/home/user/coolq映射到外部的/coolq文件夹，可自行修改路径。
-e VNC_PASSWD为VNC密码。注意该密码不能超过8个字符，默认123456。
```
删除默认配置，使用特定配置
```
rm -rf /coolq/app/io.github.richardchien.coolqhttpapi/config/general.ini
```
访问`VNC`地址配置机器人,`http://ip:9000`输入密码，默认`123456`
第一次登陆QQ会生成配置文件，先进行修改`/coolq/app/io.github.richardchien.coolqhttpapi/config`目录下的`你的qq.json`
```
将use_ws后面的false改为true
#SSH客户端直接修改
sed -i 's#"use_ws": false#"use_ws": true#g' /coolq/app/io.github.richardchien.coolqhttpapi/config/*.json
```
安装Nodejs
```
#Debian/Ubuntu系统
curl -sL https://deb.nodesource.com/setup_10.x | bash -
apt install -y git nodejs 

#CentOS系统
curl -sL https://rpm.nodesource.com/setup_10.x | bash -
yum install nodejs git -y
```
安装CQ-picfinder-robot
```
#拉取项目
git clone https://github.com/Tsuk1ko/CQ-picfinder-robot.git
cd CQ-picfinder-robot
#复制配置文件
cp config.default.json config.json
#安装依赖
npm i
#安装pm2
npm install -g pm2
```
`config.json`配置文件参考如下：
```
#别直接将下面配置文件复制进去，JSON是不允许注释的，仅供参考
{
    //前面这几项配置请参考https://github.com/momocow/node-cq-websocket/blob/master/docs/api/CQWebSocket.md#cqwebsocketoption
    "host": "127.0.0.1",
    "port": 6700,
    "enableAPI": true,
    "enableEvent": true,
    "access_token": "",
    "reconnection": true,
    "reconnectionAttempts": 10,
    "reconnectionDelay": 5000,
    //以下开始都是搜图机器人配置
    "picfinder": {
        "debug": false,            //调试模式，启用后会在控制台输出每次查询的返回文本
        "admin": -1,               //指定管理者QQ，请务必设置
        "autoAddFriend": false,    //自动同意好友申请（false则忽略，但不会拒绝）
        "addFriendAnswers": [],    //根据问题回答同意好友申请（后续详解
        "autoAddGroup": false,     //自动同意入群申请（false同上，但可以用命令手动允许，后续有说明）
        "searchLimit": 30,         //每名用户每日搜索次数限制
        //复读机
        "repeat": {
            "enable": true,        //开关
            "times": 3,            //当检测到某个群有这么多次相同发言后会概率参与复读
            "probability": 40,     //复读概率（百分比）
            "commonProb": 0.1      //日常复读概率（百分比）
        },
        //setu功能
        "setu": {
            "enable": false,       //是否启用
            "allowPM": true,       //是否允许私聊使用
            "pximgProxy": "",      //设置发送setu时使用的反向代理，后续详解
            "deleteTime": 30,      //发送后这么多秒自动撤回（0则不撤回，下同）
            "cd": 600,             //使用冷却时间（秒），每名用户独立，0则无冷却
            "limit": 30,           //每名用户每日次数限制
            "whiteGroup": [],      //群组白名单（请按照json数组格式填写）
            "whiteOnly": false,    //仅允许白名单群使用（与上面的私聊使用是独立的）
            "whiteCd": 0,          //白名单群组的使用冷却时间
            "whiteDeleteTime": 0   //白名单群组的撤回时间
        },
        //指令正则表达式
        "regs": {
            //开启搜图模式
            "searchModeOn": "竹竹搜[图圖]",
            //关闭搜图模式
            "searchModeOff": "[谢謝]+竹竹",
            //签到
            "sign": "我(.*)签到",
            //setu
            "setu": "(竹竹.*[来來发發给給].*[色瑟][图圖])|(--setu)"
        },
        //回复
        "replys": {
            //默认回复
            "default": "必须要发送图片我才能帮你找噢_(:3」」\n支持批量！",
            //调试模式时
            "debug": "维护升级中，暂时不能使用，抱歉啦~",
            //个人搜索次数到达上限时
            "personLimit": "您今天搜的图太多辣！休息一下明天再来搜吧~",
            //搜索失败时
            "failed": "搜索失败惹 QAQ\n有可能是服务器网络爆炸，请重试一次",
            //签到相关
            "sign": "签到成功，送您10个赞！",
            "signed": "您今天已经签到过啦_(:3」∠)_",
            //开启搜图模式
            "searchModeOn": "了解～请发送图片吧！支持批量噢！\n如想退出搜索模式请发送“谢谢竹竹”",
            //已经开启搜图模式
            "searchModeAlreadyOn": "您已经在搜图模式下啦！\n如想退出搜索模式请发送“谢谢竹竹”",
            //关闭搜图模式
            "searchModeOff": "不用谢～",
            //已经关闭搜图模式
            "searchModeAlreadyOff": "にゃ～",
            //setu冷却中
            "setuLimit": "乖，要懂得节制噢 →_→",
            //setu请求错误
            "setuError": "瑟图服务器爆炸惹_(:3」∠)_",
            //其他不满足发送setu的条件
            "setuReject": "很抱歉，该功能暂不开放_(:3」」"
        },
        //OCR（详细见“附加功能”）
        "ocr": {
            "use": "ocr.space", //选择使用的OCR服务
            "ocr.space": {
                "defaultLANG": "eng",
                "apikey": ""
            },
            "baidubce": {
                "useApi": "accurate_basic",
                "apiKey": "",
                "secretKey": ""
            }
        },
        //明日方舟公开招募计算器（详细见“附加功能”）
        "akhr": {
            "enable": false,    //true则启用
            "ocr": "ocr.space"  //选择使用的OCR服务
        }
    },
    //数据库配置（用于缓存搜图结果）
    "mysql": {
        "enable": false,       //是否开启缓存功能
        "expire": 172800,      //缓存时间（秒），默认为两天（172800秒）
        "host": "127.0.0.1",   //数据库地址
        "port": 3306,          //端口
        "db": "",              //数据库名
        "user": "",            //用户名
        "password": "",        //密码
        "expire": 172800       //缓存时间
    },
    //Saucenao地址，一般请不要动，除非你猜到了我提供此设置的意义（
    "saucenaoHost": [
        "saucenao.com"
    ],
    //WhatAnime的域名，同上
    "whatanimeHost": [
        "trace.moe"
    ]
}
```
配置完成之后cd到插件目录使用指令启动
```
#启动
npm run pm2start
#停止
npm run pm2stop
#重启
npm run pm2restart
#查看日志
npm run pm2log
```

##使用
**日常使用**
```
#私聊
1、直接发送图片即可
2、详见下方搜图模式说明

#群组&讨论组
1、@机器人并发送图片
2、详见下方搜图模式说明(群限定)
3、特别地，在群组中可以发送符合配置中正则表达式的发言以进入搜图模式，在搜图模式中，发送的所有图片即使不@也会被搜图，此功能通常用于在手机上无法在转发图片时@的情况；另外，进入搜图模式后也请务必记得退出搜图模式！

#可以在同一条消息中包含多张图片(针对PC)，会自动批量搜索

#搜索图片时可以在消息内包含以下参数来指定搜索范围或者使用某项功能，参数之间互斥，优先级从上到下
1、--get-url：获取图片的在线链接（不会搜图）
2、--a2d：使用 ascii2d 进行搜索（优势在于可搜索局部图）
3、--pixiv：从P站中搜索
4、--danbooru：从Danbooru中搜索
5、--book：搜索本子
6、--anime：搜索番剧

#如果saucenao得到的结果相似度低于60%，会自动使用ascii2d进行搜索

#如果搜索到本子，会自动在 nhentai 中搜索并返回链接(如果有汉化本会优先返回汉化本链接)

#如果搜到番剧，会自动使用WhatAnime搜索番剧详细信息
1、AnimeDB与WhatAnime的结果可能会不一致，是正常现象，毕竟这是两个不同的搜索引擎
2、同时展示这两个搜索的目的是为了尽力得到你可能想要的识别结果
2、搜图模式
```
**搜图模式**
```
#搜图模式存在的意义是方便手机用户在转发图片等不方便在消息中夹带@或搜图参数的情况下指定搜索库

#在私聊时直接发送图库关键字
此时你发出来的下一张图（只有下一张，也就是一次性的）会使用指定搜索库

#在群组中发送符合配置中正则表达式的发言进入搜图模式
1、此时你发出的所有图片都会被搜图（默认使用全范围搜索）
2、发送图库关键字后，你后续发出的所有图片都会使用你指定的搜索库
3、每次使用完后请务必记得退出搜图模式啊，同理，也是发送符合配置中正则表达式的发言

#图库关键字：
1、all：默认的全范围搜索模式
2、以下与上方“日常使用”中描述的搜索参数功能相同
pixiv
danbooru
book
anime
```
**处理好友申请**
```
#如果在QQ中设置选择“允许任何人”，则直接通过，酷Q无法干预

#如果选择“需要验证信息”，则是否通过由autoAddFriend设置项决定

#如果选择“需要正确回答问题”，则是否通过由对方的回答决定，酷Q无法干预

#如果选择“需要回答问题并由我确认”，则在autoAddFriend为true，且addFriendAnswers数组不为空的情况下会进行判断，只有对方的回答与addFriendAnswers的设置完全一致才会同意
```
`autoAddFriend`为`false`时不会主动拒绝申请，只是忽略申请而已，`autoAddGroup`同理。
`addFriendAnswers`配置规则：
```
#请将问题的答案顺次作为addFriendAnswers数组的元素写入，例：
"addFriendAnswers": [
    "问题一的答案",
    "问题二的答案"
]
```

**手动加群**
当你设定了`picfinder.admin`为你自己的QQ后，假如`123456789`是你需要让机器人加的群，向机器人私聊发送`--add-group=123456789`，此时：
```
#如果该群之前已经在机器人处于运行状态的时候邀请过机器人，那么该邀请会被直接同意

#如果之前没有邀请过，那么下一次邀请将会被同意

#以上两种操作都是一次性的
```

**封禁用户/群组**
发送--ban-u=Q号或--ban-g=群号，该封禁功能并不是真的拉入黑名单，仅仅是忽略用户/群的发言，如果想解封请自行编辑data/ban.json删除对应Q号/群号。

更多配置查看[github](https://github.com/Tsuk1ko/CQ-picfinder-robot#%E6%97%A5%E5%B8%B8%E4%BD%BF%E7%94%A8)

##说明
```
#为什么有时候搜不想要的出结果？
需要说明的是，搜图引擎发现新图片并收录也是需要时间的，因此画师刚上传的画作一般情况下是没办法搜到的

另外，搜图时发送的图片必须是刚好完整的图片，使用以下几种情况的图片会导致大概率搜不到结果：
1、使用的是原图的局部图，即因剪裁而不完整，此时可以尝试使用ascii2d的特征搜索功能
2、图片被 马赛克/图片马赛克等 遮挡的部分面积过大
3、截图没截好，留有黑边，例如为了省事直接使用手机截屏或者电脑手动框选截图，这种情况请在搜图前4自行编辑裁去与图片无关的部分
4、清晰度过低的图片
```
每次重启Docker都会生成`general.ini`，其文件会使特定文件失效，需要将文件删除，也可以在安装Docker镜像的时候加入变量`-e COOLQ_ACCOUNT=123456`来解决这个问题
```
docker restart wine-coolq
rm -rf /coolq/app/io.github.richardchien.coolqhttpapi/config/general.ini
```

Docker启动指令
```
docker start wine-coolq
```