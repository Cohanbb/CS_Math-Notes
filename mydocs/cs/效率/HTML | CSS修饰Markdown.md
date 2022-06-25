**本文索引**  

- [使用 HTML/CSS 修饰 Markdown 中的字体格式](#使用-htmlcss-修饰-markdown-中的字体格式)
  - [颜色和大小](#颜色和大小)
  - [格式](#格式)
  - [字体](#字体)
  - [引用](#引用)

<hr>

# 使用 HTML/CSS 修饰 Markdown 中的字体格式

## 颜色和大小

```html
<font color=red size=6 >修改颜色和大小</font>
<p style="color:blue; font-size:32px">修改颜色和大小</p>
```

<font color=red size=6 >修改颜色和大小</font>
<p style="color:blue; font-size:32px">修改颜色和大小</p>

## 格式

```html
<b>加粗</b> <I>斜体</I> <U>下划线</U> <S>删除线</S>
<sub>下标</sub> <sup>上标</sup>
```

<b>加粗</b> <I>斜体</I> <U>下划线</U> <S>删除线</S>
<sub>下标</sub> <sup>上标</sup>

## 字体

常用的几款中、英文字体。

```html
<p style="font-family:Simsun;">宋体</p>
<p style="font-family:STKaiti;">楷体</p>
<p style="font-family:STHeiti;">黑体</p>
<p style="font-family:Times New Roman;">Times New Roman</p>
<p style="font-family:Arial;">Arial</p>
<p style="font-family:Courier;">Courier</p>
<p style="font-family:Consolas;">Consolas</p>
```

<p style="font-family:Simsun;">宋体</p>
<p style="font-family:STKaiti;">楷体</p>
<p style="font-family:STHeiti;">黑体</p>
<p style="font-family:Times New Roman;">Times New Roman</p>
<p style="font-family:Arial;">Arial</p>
<p style="font-family:Courier;">Courier</p>
<p style="font-family:Consolas;">Consolas</p>


## 引用

Markdown 自带的引用 `>` 并不好用，可使用 HTML 实现。 

```html
<blockquote>
第一层
<blockquote>
第二层
</blockquote>
第一层
</blockquote>
```

<blockquote>
第一层
<blockquote>
第二层
</blockquote>
第一层
</blockquote>
