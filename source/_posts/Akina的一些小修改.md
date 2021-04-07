---
title: Akina的一些小修改
date: 2020-03-02 03:06:00
categories: 笔记
urlname: 29
tags:
- 教程
---
Akina for Typecho是由[缺乏维生素](https://zhebk.cn/Web/Akina.html)移植自`Wordpress`
因为个人觉得有些不完善，所以加点小修改

## 聚焦
作者聚焦图片是写死了的，所以给主题小小修改一下就可以在后台给聚焦加标题图片链接了
修改位置：`index.php`
```php
<!-- 聚焦内容 -->
<div class="top-feature">
	<h1 class="fes-title">聚焦</h1>
		<div class="feature-content">
			<li class="feature-1"><a href="<?php $this->options->feature1();?>"><div class="feature-title"><span class="foverlay">feature1</span></div><img src="<?php echo theurl; ?>images/feature/feature1.jpg"></a></li>
			<li class="feature-2"><a href="<?php $this->options->feature2();?>"><div class="feature-title"><span class="foverlay">feature2</span></div><img src="<?php echo theurl; ?>images/feature/feature2.jpg"></a></li>
			<li class="feature-3"><a href="<?php $this->options->feature3();?>"><div class="feature-title"><span class="foverlay">feature3</span></div><img src="<?php echo theurl; ?>images/feature/feature3.jpg"></a></li>
		</div>
</div>
```
修改为
```php
<!-- 聚焦内容 -->
<div class="top-feature">
	<h1 class="fes-title">聚焦</h1>
		<div class="feature-content">
			<li class="feature-1"><a href="<?php $this->options->feature1();?>"><div class="feature-title"><span class="foverlay"><?php $this->options->title1();?></span></div><img src="<?php $this->options->n1();?>"></a></li>
			<li class="feature-2"><a href="<?php $this->options->feature2();?>"><div class="feature-title"><span class="foverlay"><?php $this->options->title2();?></span></div><img src="<?php $this->options->n2();?>"></a></li>
			<li class="feature-3"><a href="<?php $this->options->feature3();?>"><div class="feature-title"><span class="foverlay"><?php $this->options->title3();?></span></div><img src="<?php $this->options->n3();?>"></a></li>
		</div>
</div>
```
修改位置：`functions.php`
```php
	$feature1 = new Typecho_Widget_Helper_Form_Element_Text('feature1', NULL,NULL, _t('聚焦内容1'), _t('请规范填写，需https://，http://或者//'));
    $form->addInput($feature1);
	
	$feature2 = new Typecho_Widget_Helper_Form_Element_Text('feature2', NULL,NULL, _t('聚焦内容2'), _t('请规范填写，需https://，http://或者//'));
    $form->addInput($feature2);
	
	$feature3 = new Typecho_Widget_Helper_Form_Element_Text('feature3', NULL,NULL, _t('聚焦内容3'), _t('请规范填写，需https://，http://或者//'));
    $form->addInput($feature3);
```
修改为
```php
	$feature1 = new Typecho_Widget_Helper_Form_Element_Text('feature1', NULL,NULL, _t('聚焦文章1'), _t('请规范填写，需https://，http://或者//'));
    $form->addInput($feature1);
    $n1 = new Typecho_Widget_Helper_Form_Element_Text('n1', NULL,'/usr/themes/Akina/images/feature/feature1.jpg', _t('聚焦图片1'), _t('默认图/usr/themes/Akina/images/feature/feature1.jpg'));
    $form->addInput($n1);
    $title1 = new Typecho_Widget_Helper_Form_Element_Text('title1', NULL,'/usr/themes/Akina/images/feature/feature1.jpg', _t('标题1'));
    $form->addInput($title1);
	
	$feature2 = new Typecho_Widget_Helper_Form_Element_Text('feature2', NULL,NULL, _t('聚焦文章2'), _t('请规范填写，需https://，http://或者//'));
    $form->addInput($feature2);
    $n2 = new Typecho_Widget_Helper_Form_Element_Text('n2', NULL,'/usr/themes/Akina/images/feature/feature2.jpg', _t('聚焦图片2'), _t('默认图/usr/themes/Akina/images/feature/feature2.jpg'));
    $form->addInput($n2);
    $title2 = new Typecho_Widget_Helper_Form_Element_Text('title2', NULL,'/usr/themes/Akina/images/feature/feature1.jpg', _t('标题2'));
    $form->addInput($title2);
	
	$feature3 = new Typecho_Widget_Helper_Form_Element_Text('feature3', NULL,NULL, _t('聚焦文章3'), _t('请规范填写，需https://，http://或者//'));
    $form->addInput($feature3);
    $n3 = new Typecho_Widget_Helper_Form_Element_Text('n3', NULL,'/usr/themes/Akina/images/feature/feature3.jpg', _t('聚焦图片3'), _t('默认图/usr/themes/Akina/images/feature/feature3.jpg'));
	$form->addInput($n3);
	$title3 = new Typecho_Widget_Helper_Form_Element_Text('title3', NULL,'/usr/themes/Akina/images/feature/feature1.jpg', _t('标题3'));
    $form->addInput($title3);
```
有些乱，凑合着用

## 聚焦图片自动裁剪
配合上面的修改一起用，主题原本是没有自动裁剪图片功能的，没有事先裁剪好，图片会拉伸
修改位置：`css/style.css`
将下面代码添加到`.top-feature img {}`花括号里面，保存就成了
```
object-fit: cover;
```


## 添加灯箱效果
这个是因为在pc端看不见小图片我给加上去的，代码来自[Typecho文章图片添加灯箱效果](https://www.seogo.me/typecho/598.html)
修改位置：`header.php </head>`标签之前
```php
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7/jquery.min.js"></script> <!--如果主题已经引用了jQuery库，可以忽略这条-->
<link rel="stylesheet" href="https://cdn.staticfile.org/fancybox/3.5.2/jquery.fancybox.min.css">
<script src="https://cdn.staticfile.org/fancybox/3.5.2/jquery.fancybox.min.js"></script>
```
修改位置：`post.php`
```php
<?php $this->content(); ?>
#改为-------
<?php
    $pattern = '/\<img.*?src\=\"(.*?)\"[^>]*>/i';
    $replacement = '<a href="$1" data-fancybox="gallery" /><img src="$1" alt="'.$this->title.'" title="点击放大图片"></a>';
    $content = preg_replace($pattern, $replacement, $this->content);
    echo $content;
?>
```
修改位置：`footer.php </body>`标签之前
```php
<script type="text/javascript">
    $(document).ready(function () {
        $( ".fancybox").fancybox();
    });
</script>
```
完成刷新下吧。