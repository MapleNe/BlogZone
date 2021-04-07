---
title: QUIC.Cloud加速CDN
date: 2020-03-07 05:03:00
categories: 折腾
urlname: 24
tags:
- CDN
---
简单介绍下`Quic.cloud`，这是一家提供wordpress缓存加速节点的CDN服务商
免费账号提供20G流量，但我账号好像不走流量了
>QUIC.cloud is the first and only content delivery network with the ability to cache dynamic WordPress pages. Using QUIC as the transfer protocol, QUIC.cloud will make your website faster and more secure than the competition.
QUIC.cloud greatly reduces transmission time to all of your site’s visitors, no matter where they live. Your website is potentially located across the globe from its visitors, but with QUIC.cloud, your content is cached on servers all around the world. When a visitor requests content from your site, a copy is served from the visitor’s nearest server location. By transmitting both static and dynamic content from the closest server, instead of from the main site server, QUIC.cloud dramatically speeds up your site.
Please Note: QUIC.cloud is still in its beta stage, and is not recommended for use in production environments.

[官网](https://www.quic.cloud/)

## 添加域名
![1](https://i.loli.net/2020/03/07/p2QsZeIoimFOTxW.png)
![2](https://i.loli.net/2020/03/07/Hc1XQsy7TKCFMzo.png)
![3](https://i.loli.net/2020/03/07/oJ5Mg3ZKL9Olsj2.png)

## 节点
这个CDN默认是把中国大陆全部解析到了新加坡AWS的节点，这方面自己分线路解析一下到合适的节点比较好

至于看所有的节点，你可以用`https://tools.ipip.net/ping.php`去Ping你的CNAME

### 1. 东京AWS节点 52.69.47.110
推荐联通&移动使用，联通走上海-东京NTT直连，移动走上海-日本EQUINIX直连（电信其实东京是有20G的163的，但是因为爆了很多地方回程调到东京NTT去了）

### 2. 新加坡AWS节点 13.250.65.49
半适合电信用，联通移动都绕日本。和日本一样，到电信部分地区走东京NTT回程，巨堵，不确定性很强。

### 3. 俄勒冈AWS节点 18.237.80.88
推荐电信使用，AWS在美西也接了163（质量不如东京新加坡，但是路由不会搞特殊化）。联通移动也可以用，接了北美CUG和CMI，但是不推荐。

### 4. 德国AWS节点 13.250.65.49
移动电信可以用，AWS在德国接了CMI和CT Europe，质量比较一般，如果你源站在欧洲可以考虑。

可以参考下我的
![4](https://i.loli.net/2020/03/07/kByHqbX8GtjZTAg.png)

