---
title: "C# Reflection"
author: "Chenzengxin"
date: 2019.09.12
---

## Background

##### CSS 属性定义背景效果:

    background-color 属性定义了元素的背景颜色
    background-image 属性描述了元素的背景图像
    background-repeat (no-repeat、repeat-x、repeat-y)
    background-attachment 背景图像是否固定或者随着页面的其余部分滚动。
    background-position 属性改变图像在背景中的位置
``` CSS
body {background:#ffffff url('img_tree.png') no-repeat right top;}
```
---

## Text

##### 文本颜色:
    十六进制值 - 如: ＃FF0000
    一个RGB值 - 如: RGB(255,0,0)
    颜色的名称 - 如: red
``` CSS
body {color:red;}
h1 {color:#00ff00;}
h2 {color:rgb(255,0,0);}
```

##### 文本的对齐方式:
    文本可居中或对齐到左或右,两端对齐。
    当text-align设置为"justify"，每一行被展开为宽度相等，左，右外边距是对齐。
    text-align
``` CSS
h1 {text-align:center;}
p.date {text-align:right;}
p.main {text-align:justify;}
```

##### 文本修饰:
    text-decoration 属性用来设置或删除文本的装饰。
``` CSS
a {text-decoration:none;}
h1 {text-decoration:overline;}
h2 {text-decoration:line-through;}
h3 {text-decoration:underline;}
```

##### 文本转换:
    text-decoration 属性用来设置或删除文本的装饰。
``` CSS
p.uppercase {text-transform:uppercase;}
p.lowercase {text-transform:lowercase;}
p.capitalize {text-transform:capitalize;}
```

##### 文本缩进:
    text-decoration 属性用来设置或删除文本的装饰。
``` CSS
p {text-indent:50px;}
```


##### 所有属性:

``` CSS
color	设置文本颜色
direction	设置文本方向。
letter-spacing	设置字符间距
line-height	设置行高
text-align	对齐元素中的文本
text-decoration	向文本添加修饰
text-indent	缩进元素中文本的首行
text-shadow	设置文本阴影
text-transform	控制元素中的字母
unicode-bidi	设置或返回文本是否被重写 
vertical-align	设置元素的垂直对齐
white-space	设置元素中空白的处理方式
word-spacing	设置字间距
```
---
## Font

- CSS字体属性定义字体，加粗，大小，文字样式。
- 

##### CSS字型
- 通用字体系列 - 拥有相似外观的字体系统组合（如 "Serif" 或 "Monospace"）
- 特定字体系列 - 一个特定的字体系列（如 "Times" 或 "Courier"）

|Generic family|字体系列|说明|
|  ----  | ----  | ---- |
|Serif|Times New Roman Georgia|Serif字体中字符在行的末端拥有额外的装饰|
|Sans-serif|Arial Verdana|"Sans"是指无 - 这些字体在末端没有额外的装饰|
|Monospace|Courier New <br/> Lucida Console|所有的等宽字符具有相同的宽度|


##### 字体系列
- font-family 属性设置文本的字体系列。

``` CSS
p{font-family:"Times New Roman", Times, serif;}
```

##### 字体样式

- 正常 - 正常显示文本
- 斜体 - 以斜体字显示的文字
- 倾斜的文字 - 文字向一边倾斜（和斜体非常类似，但不太支持）
``` CSS
p.normal {font-style:normal;}
p.italic {font-style:italic;}
p.oblique {font-style:oblique;}
```

##### 字体大小
- font-size 设置文字的大小

``` CSS
h1 {font-size:40px;}
h2 {font-size:30px;}
p {font-size:14px;}
```
---

## 链接

##### 链接样式

- 链接的样式，可以用任何CSS属性（如颜色，字体，背景等）。

``` CSS
a:link {color:#000000;}      /* 未访问链接*/
a:visited {color:#00FF00;}  /* 已访问链接 */
a:hover {color:#FF00FF;}  /* 鼠标移动到链接上 */
a:active {color:#0000FF;}  /* 鼠标点击时 */
```
---

## 盒子模型
    所有HTML元素可以看作盒子，在CSS中，"box model"这一术语是用来设计和布局时使用。CSS盒模型本质上是一个盒子，封装周围的HTML元素，它包括：边距，边框，填充，和实际内容。盒模型允许我们在其它元素和周围元素边框之间的空间放置元素。


##### 

---