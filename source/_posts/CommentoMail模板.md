---
title: CommentoMail模板
date: 2020-03-16 01:13:00
categories: 笔记
urlname: 18
tags:
- 笔记
---
贴一下目前邮箱评论的模板吧，需要修改到mailer或者其他插件看着地方改就行了
![1](https://i.loli.net/2020/03/16/AzuhemfXqGta2EP.png)
##guest
```html
<div style="width: 550px;height: auto;border-radius: 5px;margin:0 auto;box-shadow: 0px 0px 20px #888888;position: relative;padding-bottom: 5px;">
    <div style="background-image: url(https://s2.ax1x.com/2019/12/10/QD1rg1.jpg);width:550px;height: 300px;background-size: cover;background-repeat: no-repeat;border-radius: 5px 5px 0px 0px;"></div>
    <div style="width: 200px;height: 40px;background-color: rgb(255, 114, 114);margin-top: -20px;margin-left: 20px;box-shadow: 3px 3px 3px rgba(0, 0, 0, 0.3);color: rgb(255, 255, 255);text-align: center;line-height: 40px;">Dear: {author_p}</div>
    <div style="background-color:white;line-height:180%;padding:0 15px 12px;width:520px;margin:30px auto;color:#555555;font-family:'Century Gothic','Trebuchet MS','Hiragino Sans GB',微软雅黑,'Microsoft Yahei',Tahoma,Helvetica,Arial,'SimSun',sans-serif;font-size:12px;margin-bottom: 0px;">  
        <h2 style="font-size:14px;font-weight:normal;padding:13px 0 10px 8px;"><span style="color: #12ADDB;font-weight: bold;"></span>您在<a style="text-decoration:none;color: #ff7272;" href="{permalink}" target="_blank">《{title}》</a>的评论有了新的回复呐~</h2>  
        <div style="padding:0 12px 0 12px;margin-top:18px">
            <style type="text/css">
                .comment>img{margin: 0px 6px 5px 6px;width: 25px;}
            </style>
            <p>您的评论：</p>  
            <p class="comment" style="background-color: #f5f5f5;border: 0px solid #DDD;border-radius: 5px;padding: 10px 15px;margin:18px 0">{text_p}</p>  
            <p><strong>{author}</strong>&nbsp;给您的回复：</p>  
            <p class="comment" style="background-color: #f5f5f5;border: 0px solid #DDD;border-radius: 5px;padding: 10px 15px;margin:18px 0">{text}</p>  
        </div>  
    </div>
    <div style="color:#8c8c8c;;font-family: 'Century Gothic','Trebuchet MS','Hiragino Sans GB',微软雅黑,'Microsoft Yahei',Tahoma,Helvetica,Arial,'SimSun',sans-serif;font-size: 10px;width: 100%;text-align: center;word-wrap:break-word;margin-top: -30px;">
        <p style="padding:20px;">萤火虫消失之后，那光的轨迹仍久久地印在我的脑际。那微弱浅淡的光点，仿佛迷失方向的魂灵，在漆黑厚重的夜幕中彷徨。——《挪威的森林》村上春树</p>
    </div>
    <a style="text-decoration:none; color:#FFF;width: 40%;text-align: center;background-color:#ff7272;height: 40px;line-height: 35px;box-shadow: 3px 3px 3px rgba(0, 0, 0, 0.30);margin: -10px auto;display: block;" href="{permalink}" target="_blank">查看回复的完整內容</a>
    <div style="color:#8c8c8c;;font-family: 'Century Gothic','Trebuchet MS','Hiragino Sans GB',微软雅黑,'Microsoft Yahei',Tahoma,Helvetica,Arial,'SimSun',sans-serif;font-size: 10px;width: 100%;text-align: center;margin-top: 30px;">
        <p>本邮件为系统自动发送，请勿直接回复~</p>
    </div>
    <div style="color:#8c8c8c;;font-family: 'Century Gothic','Trebuchet MS','Hiragino Sans GB',微软雅黑,'Microsoft Yahei',Tahoma,Helvetica,Arial,'SimSun',sans-serif;font-size: 10px;width: 100%;text-align: center;padding-bottom: 1px;">
        <p>?2020 Copyright {siteTitle}</p>
    </div>
</div>
```

##owner
```html
<div style="width: 550px;height: auto;border-radius: 5px;margin:0 auto;box-shadow: 0px 0px 20px #888888;position: relative;">
    <div style="background-image: url(https://s2.ax1x.com/2019/12/10/QD1rg1.jpg);width:550px;height: 250px;background-size: cover;background-repeat: no-repeat;border-radius: 5px 5px 0px 0px;"></div>
    <div style="background-color:white;line-height:180%;padding:0 15px 12px;width:520px;margin:10px auto;color:#555555;font-family:'Century Gothic','Trebuchet MS','Hiragino Sans GB',微软雅黑,'Microsoft Yahei',Tahoma,Helvetica,Arial,'SimSun',sans-serif;font-size:12px;margin-bottom: 0px;">
        <h2 style="font-size:14px;font-weight:normal;padding:13px 0 10px 8px;"><span style="color: #ff7272;font-weight: bold;"></span>您的文章<a style="text-decoration:none;color: #ff7272;" href="{permalink}" target="_blank">《{title}》</a>有了新的回复耶~</h2>
        <div style="padding:0 12px 0 12px;margin-top:18px">
            <p><strong>{author}</strong>&nbsp;给您的评论：</p>
            <style type="text/css">
                .comment>img{margin: 0px 6px 5px 6px;width: 25px;}
            </style>
            <p class="comment" style="background-color: #f5f5f5;border: 0px solid #DDD;border-radius: 5px;padding: 10px 15px;margin:18px 0">{text}</p>
            <p>其他信息：</p>
            <p style="background-color: #f5f5f5;border: 0px solid #DDD;border-radius: 5px;padding: 10px 15px;margin:18px 0">IP：{ip}<br />邮箱：<a style="text-decoration:none;color: #ff7272;" href="mailto:{mail}">{mail}</a><br />状态：{status} [<a style="text-decoration:none;color: #ff7272;" href='{manage}' target='_blank'>管理评论</a>]
            <p style="background-color: #f5f5f5;border: 0px solid #DDD;border-radius: 5px;padding: 10px 15px;margin:18px 0">时间：{time}</p>
        </div>
    </div>
    <a style="text-decoration: none;color: rgb(255, 255, 255);width: 40%;text-align: center;background-color: rgb(255, 114, 114);height: 40px;line-height: 40px;box-shadow: 3px 3px 3px rgba(0, 0, 0, 0.3);display: block;margin: auto;" href="{permalink}" target="_blank">查看回复的完整內容</a>
    <div style="color:#8c8c8c;;font-family: 'Century Gothic','Trebuchet MS','Hiragino Sans GB',微软雅黑,'Microsoft Yahei',Tahoma,Helvetica,Arial,'SimSun',sans-serif;font-size: 10px;width: 100%;text-align: center; padding-bottom: 1px;">
        <p>?2020 Copyright {siteTitle}</p>
    </div>
</div>
```