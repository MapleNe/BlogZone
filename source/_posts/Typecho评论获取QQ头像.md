---
title: Typecho评论获取QQ头像
date: 2020-03-28 09:31:00
categories: 折腾
urlname: 37
tags:
- 教程
---
Typecho默认获取的头像是`Gravatar`的，要修改为获取QQ的头像只需一点小改动
在`/var/Typecho/Common.php`第986行

```php
    public static function gravatarUrl($mail, $size, $rating, $default, $isSecure = false)
    {
        if (defined('__TYPECHO_GRAVATAR_PREFIX__')) {
            $url = __TYPECHO_GRAVATAR_PREFIX__;
        } else {
            $url = $isSecure ? 'https://secure.gravatar.com' : 'http://www.gravatar.com';
            $url .= '/avatar/';
        }

        if (!empty($mail)) {
            $url .= md5(strtolower(trim($mail)));
        }

        $url .= '?s=' . $size;
        $url .= '&amp;r=' . $rating;
        $url .= '&amp;d=' . $default;

        return $url;
    }
```
修改为
```php
public static function gravatarUrl($mail, $size, $rating, $default, $isSecure = false)
{
        $reg = "/^\d{5,11}@[qQ][Qq]\.(com)$/";
        if (preg_match($reg, $mail)) {
            $img    = explode("@", $mail);
            $url = "//q2.qlogo.cn/headimg_dl?dst_uin={$img[0]}&spec=100";
        } else {
            if (defined('__TYPECHO_GRAVATAR_PREFIX__')) {
                $url = __TYPECHO_GRAVATAR_PREFIX__;
            } else {
                $url = $isSecure ? 'https://secure.gravatar.com' : 'http://www.gravatar.com';
                $url .= '/avatar/';
            }
            if (!empty($mail)) {
                $url .= md5(strtolower(trim($mail)));
            }
            $url .= '?s=' . $size;
            $url .= '&amp;r=' . $rating;
            $url .= '&amp;d=' . $default;
        }
        return $url;
}
```

如果找不到可以`Ctrl F`查找一下`获取gravatar头像地址`
就在注释下方