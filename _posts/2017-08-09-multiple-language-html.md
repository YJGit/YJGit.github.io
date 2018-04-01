---
layout: post
title:  Html多语言切换，Jquery实现
date:   2017-08-10 16:46:59 +0800
categories: 前端学习
tag: Jquery
---

* content
{:toc}


## 前言

最近在捣鼓自己的简历，想要做一个多语言切换效果，觉得这个功能还是很常见的，尤其是各种翻译教程博客之类的，都有这种切换功能。但是网上查了一会，方法是不少，但是并没有找到什么特别简洁的实现方法。结果花费了好一阵功夫，终于找到了一种自己觉得还不错的方法。实现方法如下：  

## 实现方法

1. 这个方法使用jQuery:lang()选择器，比如选取带有以"it"开头的lang属性值的所有<p>元素： ```$("p:lang(it)")```    
接下来就利用这个选择器来实现中英两种语言切换的效果。
2. 首先在测试的html里插入语言选择器:   
```
	<div id="langBox">
		<select id="lang">
			<!-- <option value="browser">Indicated by the browser</option> -->
			<option value="en">ENGLISH</option>
			<option value="ch">中文</option>
		</select>
	</div>  
```
3. 然后在需要切换的地方使用```<span lang="en"></span>```或者```<span lang="ch"></span>```标签将内容包裹起来。这两个标签一个里头接选择*ENGLISH* 时要展现的内容，一个里头接选择*中文* 时要展现的内容： 
```
	<h2 class="container-block-title">
		<span lang="en">Interests</span>
		<span lang="ch">兴趣爱好</span>
	</h2>
	<ul class="list-unstyled interests-list">
		<li>
			<span lang="en">Playing Basketball</span>
			<span lang="ch">打篮球</span>
		</li>
		<li>
			<span lang="en">Reading</span>
			<span lang="ch">阅读</span>
		</li>
		<li>
			<span lang="en">Traveling</span>
			<span lang="ch">旅游</span>
		</li>
	</ul>
```
4. 引入script：
```
	<script src="http://code.jquery.com/jquery-latest.js"></script>
	<script src="language.js"></script>
```    

    language.js内容也很简单：
```
	$(function(){
		//语言默认英文
		var language = $('#lang :selected').val();
		$("span:lang(ch)").hide();
		$("span:lang(en)").show();
		//用语言种类选择
		$('#lang').change(function(){
			language = $('#lang :selected').val();
			if(language == "en"){
				$("span:lang(ch)").hide();
				$("span:lang(en)").show();
			}
			else{
				$("span:lang(en)").hide();
				$("span:lang(ch)").show();
			}
		})
	})
```
大致做法就是当语言选择器改变的时候，展示所选语言的相关内容，而隐藏其他。 
## demo源码  
因为是用于demo，所以比较简陋，各路前端大神自然有很多方法使自己的页面酷炫起来。  
index.html:  
```
	<html>
	<head>
	<title>Demo</title>

	<script src="http://code.jquery.com/jquery-latest.js"></script>
	<script src="language.js"></script>
	</head>
	<body>
		<div id="langBox">
			<select id="lang">
				<!-- <option value="browser">Indicated by the browser</option> -->
				<option value="en">ENGLISH</option>
				<option value="ch">中文</option>
			</select>
	    </div>
		
		<h2 class="container-block-title">
			<span lang="en">Interests</span>
			<span lang="ch">兴趣爱好</span>
		</h2>
		<ul class="list-unstyled interests-list">
			<li>
				<span lang="en">Playing Basketball</span>
				<span lang="ch">打篮球</span>
			</li>
			<li>
				<span lang="en">Reading</span>
				<span lang="ch">阅读</span>
			</li>
			<li>
				<span lang="en">Traveling</span>
				<span lang="ch">旅游</span>
			</li>
		</ul>
	</body>
	</html>
```
language.js:  
```
	$(function(){
		//语言默认英文
		var language = $('#lang :selected').val();
		$("span:lang(ch)").hide();
		$("span:lang(en)").show();
		//用语言种类选择
		$('#lang').change(function(){
			language = $('#lang :selected').val();
			if(language == "en"){
				$("span:lang(ch)").hide();
				$("span:lang(en)").show();
			}
			else{
				$("span:lang(en)").hide();
				$("span:lang(ch)").show();
			}
		})
	})
```