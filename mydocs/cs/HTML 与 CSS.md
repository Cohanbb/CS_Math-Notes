---
title: HTML CSS
author: Cohanbb
---
<p align="center">
    <font size="6"><strong>HTML 与 CSS</strong></font>
</p>

# 摘要
一个 Web 页面是如何在浏览器上展示的？我们在浏览器上查看网页源代码，可看到众多的标签、符号和文字，这就是一个 HTML 文件，而浏览器可以将这个文件解析成一个 Web 页面。一个 Web 页面如何设计样式、呈现出精美的视觉效果？则需要通过 CSS 对 HTML 进行加工美化。

<hr>

**文章索引**

- [HTML](#html)
  - [简介](#简介)
  - [基本架构](#基本架构)
  - [HTML 标签](#html-标签)
    - [基本标签](#基本标签)
    - [文本格式化](#文本格式化)
    - [特殊标签](#特殊标签)
- [CSS](#css)
  - [简介](#简介-1)
  - [CSS 语法](#css-语法)
    - [基本形式](#基本形式)
    - [文本属性](#文本属性)
    - [结构属性](#结构属性)

<hr>

# HTML

## 简介 
HTML(HyperText Markup Language) **超文本**标记语言，何谓超文本？简单来说，超文本指具有超链接功能的文本，即一个超文本可以由若干个超链接构成，最常见的应用场景便是 Web 页面，也用于其他领域，譬如 Markdown 文档。

## 基本架构
`<html>` 标签：表明是一个 HTML 文档。  
`<title>` 标签：定义文档的标题。  
`<body>` 标签：定义文档的内容主体。  
`<p>` 标签：定义一个段落。  
`<br />` 标签：换行标签。  

**注：莫要忘记加上结束标签！**  

```html
<html>
    <title>demo</title>
    <body>
        <p>
            Hello World!<br />Hello Web! 
        </p>
    </body>
</html>
```

这段代码在浏览器中的效果：
<html>
    <title> demo </title>
    <body>
        <p>
            Hello World!<br />Hello Web!
        </p>
    </body>
</html>

## HTML 标签

### 基本标签   
`html` 标签：表示是一个 HTML 文档。  
`<title>` 标签：定义文档的标题。  
`<body>` 标签：定义文档的内容主体。  
`<p>` 标签：定义一个段落。  
`<br />` 标签：表示换行。  
`<h>` 标签：定义文本中的标题。    
`<hr>` 标签：表示一条水平分割线。    
`<!-- -->` 标签：定义注释。    

### 文本格式化

```html
<b>粗体</b><br />
<i>斜体</i><br />
<em>强调文字</em><br />
<small>小号文字</small><br />
<strong>加重视觉效果</strong><br />
<sub>上标</sub><br />
<sup>下标</sup><br />
<ins>插入字</ins><br />
<del>删除字</del><br />
```

这段代码解析后为：  

<b>粗体</b><br />
<i>斜体</i><br />
<em>强调文字</em><br />
<small>小号文字</small><br />
<strong>加重视觉效果</strong><br />
<sub>上标</sub><br />
<sup>下标</sup><br />
<ins>插入字</ins><br />
<del>删除字</del><br />

### 特殊标签
**链接**

```html
<a href="http://cohanbb.github.io/">这是一条链接</a>
```

<a href="http://cohanbb.github.io/">这是一条链接</a>

**图像**

```html
<img src="https://i-1-lanrentuku.52tup.com/2020/7/10/b87c8e05-344a-48d1-869f-ef6929fc8b17.jpg?imageView2/2/w/1024/" alt="图片加载失败" width="300" height="300"/>
```

<img src="https://i-1-lanrentuku.52tup.com/2020/7/10/b87c8e05-344a-48d1-869f-ef6929fc8b17.jpg?imageView2/2/w/1024/" alt="图片加载失败" width="300" height="300"/>

**预格式文本**

```html
<pre>
    预格式文本
        文本会保留换行和空格
            文本换为等线体，常用于表示代码块
</pre>
```

<pre>
    预格式文本
        文本会保留换行和空格
            文本换为等线体，常用于表示代码块
</pre>

**代码和代码块**

```html
<code>printf('代码')</code>

<pre>
    <code>printf('代码块');</code>
    <code>return;</code>
</pre>
```

<code>printf('代码')</code>

<pre>
    <code>printf('代码块');</code>
    <code>return;</code>
</pre>

**表格**

```html
<table border="1">
    <tr>
        <th>标题1</th>
        <th>标题2</th>
    </tr>
    <tr>
        <td>row 1, cell 1</td>
        <td>row 1, cell 2</td>
    </tr>
    <tr>
        <td>row 2, cell 1</td>
        <td>row 2, cell 2</td>
    </tr>
</table>
```

<table border="1">
    <tr>
        <th>标题1</th>
        <th>标题2</th>
    </tr>
    <tr>
        <td>row 1, cell 1</td>
        <td>row 1, cell 2</td>
    </tr>
    <tr>
        <td>row 2, cell 1</td>
        <td>row 2, cell 2</td>
    </tr>
</table>

**列表**

```html
有序列表
<ol>
    <li>YES</li>
    <li>NO</li>
</ol>

无序列表
<ul>
    <li>yes</li>
    <li>no</li>
</ul>

自定义列表
<dl>
    <dt>YES</dt>
    <dd>yes</dd>
    <dt>NO</dt>
    <dd>no</dd>
</dl>
```

有序列表
<ol>
    <li>YES</li>
    <li>NO</li>
</ol>

无序列表
<ul>
    <li>yes</li>
    <li>no</li>
</ul>

自定义列表
<dl>
    <dt>YES</dt>
    <dd>yes</dd>
    <dt>NO</dt>
    <dd>no</dd>
</dl>

**引用**

```html
<blockquote> 
    一级引用
    <blockquote>
        二级引用
    </blockquote>
</blockquote>
```

<blockquote> 
    一级引用
    <blockquote>
        二级引用
    </blockquote>
</blockquote>

**块级元素和内联元素**

```html
1.这是一个<div>
块级元素<br />从新的一行出现以及结束
</div>

2.这是一个<span>
内联元素，不会以新行开始
</span>
```

1.这是一个<div>
块级元素<br />从新的一行出现以及结束
</div>

2.这是一个<span>
内联元素，不会以新行开始
</span>

**表单**

```html
<form action="URL" method="get or post">
    username: <input type="text" name="username"><br />
    password: <input type="password" name="password"><br />
    单选框<br />
    <input type="radio" name="sex" value="male">男<br />
    <input type="radio" name="sex" value="female">女<br />	
    复选框<br />
    <input type="checkbox" name="number" value="1">1<br />
    <input type="checkbox" name="number" value="2">2<br />
    提交表单<br />
    <input type="submit" value="submit"/>
</form>
```

<form action="URL" method="get or post">
    username: <input type="text" name="username"><br />
    password: <input type="password" name="password"><br />
    单选框<br />
    <input type="radio" name="sex" value="male">男<br />
    <input type="radio" name="sex" value="female">女<br />	
    复选框<br />
    <input type="checkbox" name="number" value="1">1<br />
    <input type="checkbox" name="number" value="2">2<br />
    提交表单<br />
    <input type="submit" value="submit"/>
</form>

**脚本**

```html
<script>
    script code, such as JavaScript.
</script>
```

**样式**

```html
<style type="text/css">
    css code
</style>
```

# CSS

## 简介
CSS(Cascading Style Sheets) 层叠样式表，用以定义 HTML 中元素的样式，HTML 使用 CSS 的方式有三种：
1. 内联样式：在 HTML 元素标签中使用 "style" 属性。

    ```html
    <p style="color:blue;font-family:consolas;">
        inline
    </p>
    ```

2. 内部样式表：在 HTML 文档 `<header>` 区域使用 `<style>` 包含 CSS。

    ```html
    <head>
    <style type="text/css">
        CSS code
    </style>
    </head>
    ```

3. 外部引用：使用外部 CSS 文件定义样式。

    ```html
    <head>
        <link rel="stylesheet" type="text/css" href="xxx.css">
    </head>
    ```

## CSS 语法

### 基本形式

```css
[选择器] {
    [属性]: [描述];
        ......
}
```

选择器可以是 HTML 标签，也可以是 id 或 class。
* id 选择器只能定义标有特定 id 的元素的样式，形式为 `#[id]`。
* class 选择器可以定义一类元素的样式，形式为 `.[class]`。

### 文本属性
**background**

* background-color:

    > 三种定义方式：RGB "rgb(x,x,x)"，十六进制 "#H H H"， name "black"。

* background-image: 

    > url('pic-url')

* background-repeat：背景图像在哪个方向重复。

    > repeat, repeats-x, repeat-y, no-repeat

* background-attachment：背景图像是否跟随页面滚动。
* background-position：背景图像的位置。

**text**

* color：文本颜色。
* direction：文本方向。
* letter-spacing：字符间隔。
* word-spacing：单词间隔。
* line-height：行高。
* text-align：对齐方式。

    > left, right, center, justify, inherit

* text-indent：首行缩紧。
* text-shadow：文本阴影。
* text-decoration：文本画线修饰。
* white-space：空白元素的处理方式。

    >  默认 normal，即空白元素会被浏览器忽略。  
    >  nowrap 文本不会换行，一直到 `<br>` 标签。   
    >  pre 保留空白，pre-wrap 保留空白，但是正常换行。   
    >  pre-line 合并空白元素，但是保留一个空格，正常换行。  

* word-wrap：单词的换行方式，一般用 break-word。
* word-break：是否允许单词内断开，若用 break-all，则会在单词内部断开。

**font**

* font-family：

    |说明|Generic-family|特定系列|具体字体|
    |--|--|--|--|
    |有衬线体|Serif|Times, Georgia|"Times New Roman", "Geogria", "宋体", "仿宋"|
    |无衬线体|Sans-serif|Sans-serif|"Arial", "Helvetica", Verdana", "黑体" 等|
    |等宽体|Monospace|Consolas|"Courier", "Courier New", "Lucinda Console"等|
    
* font-size：

    > CSS 中表示字体大小有多种形式：
    > 1. px 像素值。
    > 2. pt 磅(= 0.75px)。
    > 3. em 相对父元素的大小。
    > 4. rem 相对于 html 标签中 font-size 的大小，默认 1rem = 16px。
    > 5. percentage 同 em。
    > 6. 使用绝对大小和相对大小值。
    
* font-style：斜体样式。
* font-weight：字体粗细。 

**链接**

* a:link：未访问过的链接。
* a:visited：已访问过的链接。
* a:hover：鼠标放置的链接。
* a:active：鼠标点击的链接。

```css
a:link or visited or hover or active {
    background-color:; /*链接背景颜色*/
    color:; /*链接字体颜色*/
    text-decoration:; /*链接文本画线修饰*/
}
```

### 结构属性
**盒子模型**   
所有的 HTML 元素都可以看成一个盒子模型，包括外边距(margin)、边框(border)、内边距(padding)、内容(content)，内容指的是文本或图像等。

![](https://www.runoob.com/images/box-model.gif)

**margin** 

|属性|说明|描述|
|--|--|--|
|margin-top|上边距|auto, length, percentage|
|margin-right|右边距|auto, length, percentage|
|margin-bottom|下边距|auto, length, percentage|
|margin-left|左边距|auto, length, percentage|
|margin|以上四个可简写为 margin|按个数 4，3，2，1 依次表示：<br /> 上，右，下，左；上，左右，下；上下，左右；全部外边距。 |

**border**

* border-width：边框的宽度。
    
    > 1. 可以用 thin, medium, thick, length, inherit 表示。
    > 2. 按个数 4，3，2，1 依次表示：上，右，下，左；上，左右，下；上下，左右；全部边框的宽度。

* border-color：边框的颜色。

    > 1. RGB 十六进制 name 三种表示法。
    > 2. 按个数 4，3，2，1 依次表示：上，右，下，左；上，左右，下；上下，左右；全部边框的颜色。 

* border-style：边框的风格。

    > 1. 无边框 none，点线边框 dotted，虚线边框 dashed，实线边框 solid，两个实线边框 double，3D沟槽边框 groove，3D脊边框 ridge，3D嵌入边框 inset，3D突出边框 outset。
    > 2. 按个数 4，3，2，1 依次表示： 上，右，下，左；上，左右，下；上下，左右；全部边框的风格。

* border-[none/top/right/bottom/left]：以上三个简写。

    > 参数依次为：[width],[style],[color]

* border-radius：设置圆角边框。

    > length 或 percentage。

* border-[top/right/bottom/left]-[width/style/color]：设置某一边的某一个属性。

**padding**  
使用方法与 margin 类似。

**display**  
典型的块元素：`<p>` `<div>` `<pre>` `<h>`，典型的内联元素：`<a>` `<span>` `<code>`，display 可以更改元素的显示方式。

* inline： 内联元素。
* block：块元素。

**overflow**

* visible：默认值，超出的内容会呈现在边框外面。 
* hidden：溢出内容被修剪，且被隐藏。
*  scroll：溢出内容被修剪，显示滚动条。
* auto：浏览器根据情况自动添加滚动条。
* inherit：继承父元素的 overflow 属性值。


# 参考文献
[1] 菜鸟教程. HTML 教程[EB/OL]. https://www.runoob.com/html/html-tutorial.html.   
[2] 菜鸟教程. CSS 教程[EB/OL]. https://www.runoob.com/css/css-tutorial.html.