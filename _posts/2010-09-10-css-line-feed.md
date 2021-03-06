---
layout: post
title: 关于文字换行与不换行
category: "note"
tags: ["css"]
---

近期工作过程中遇到需求方提出问题：有些地方由于一长串的英文或者数字导致页面模块被撑开。如果需求方在填内容的时候避免长串连续英文或者数字当然最好，但总会有些用户不会注意，为了一劳永逸只好用css样式去控制了：

首先我们来了解一些基础知识：

table-layout：用来显示表格单元格、行、列的算法规则的属性。其值包括：  
automatic：默认，列宽度由单元格内容设定；  
fixed：列宽由表格宽度和列宽度设定；  
inherit：规定应该从父元素继承 table-layout 属性的值。

所有浏览器都支持 table-layout 属性，8及以下版本的ie浏览器都不支持 inherit 值。

word-wrap：设置或检索当当前行超过指定容器的边界时是否断开转行。其值包括：  
normal：默认，控制连续文本换行；  
break-word：内容将在边界内换行。

使用break-word时是强制换行，中文没有问题，英文语句也没问题（带正常空格与标点符号），但是对于长串连续英文就不起作用。

word-break：设置或检索对象内文本的字内换行行为。其值包括：  
normal：默认，依照亚洲语言和非亚洲语言的文本规则，允许在字内换行。  
break-all：该行为与亚洲语言的normal相同。也允许非亚洲语言文本行的任意字内断开。该值适合包含一些非亚洲文本的亚洲文本。  
keep-all：与所有非亚洲语言的normal相同。对于中文，韩文，日文，不允许字断开。适合包含少量亚洲文本的非亚洲文本。

了解了以上基础知识后，接下来我们就很容易理解以下的断行解决办法了：

table：  
在table的css里加：table-layout:fixed;  
在td的css里加：word-wrap:break-word; word-break:break-all;

非table：  
直接在css里加：word-wrap:break-word; word-break:break-all;

但是，以上两种情况的解决方法，都不可避免遇到一个问题：就是普通英文语句中地单词在末尾时也会被断开。虽然这种方法能解决文字把模块撑开的问题，但却带来了新的问题，单词被断开总比页面被撑开好，而且需求方看到单词被断开也能手工在单词前面加换行代码，两害相权取其轻，所以我们还是选择单词断行。

然后顺便说一下css强制文字不换行，这比强制换行简单多了，只需要用到：white-space这个属性。

white-space属性设置如何处理元素内的空白，这个属性声明建立布局过程中如何处理元素中的空白符其值包括：  
normal：默认。空白会被浏览器忽略。  
pre：空白会被浏览器保留。其行为方式类似 HTML 中的`<pre>`标签。  
nowrap：文本不会换行，文本会在在同一行上继续，直到遇到`<br>`标签为止。  
pre-wrap：保留空白符序列，但是正常地进行换行。  
pre-line：合并空白符序列，但是保留换行符。  
inherit：规定应该从父元素继承 white-space 属性的值。

解决方法是直接在元素的css里加：white-space:nowrap;

__2012.02.13补充，各浏览器兼容的pre换行：__

普通html标签只需要用`word-wrap:break-word;word-break:break-all;overfllw:hidden;`即可实现自动换行，但在`pre`标题里面不行，以下是解决办法：

各浏览器兼容的pre换行的css代码：

	pre{
	  white-space: pre-wrap;       /* css-3 */
	  white-space: -moz-pre-wrap;  /* Mozilla, since 1999 */
	  white-space: -pre-wrap;      /* Opera 4-6 */
	  white-space: -o-pre-wrap;    /* Opera 7 */
	  word-wrap: break-word;       /* Internet Explorer 5.5+ */
	}

(完)。


