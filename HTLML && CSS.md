# HTML

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>ZONGXP</title>
</head>
<body>
 
<h1>我的第一个标题</h1>
<p>我的第一个段落。</p>
 
</body>
</html>
```

- **<!DOCTYPE html>** 声明为 HTML5 文档
- **<html>** 元素是 HTML 页面的根元素
- **<head>** 元素包含了文档的元（meta）数据，如 <meta charset="utf-8"> 定义网页编码格式为 **utf-8（**由于在大部分浏览器中直接输出中文会出现乱码，所以要在头部将字符声明为UTF-8**）**
- **<title>** 元素描述了文档的标题
- **<body>** 元素包含了可见的页面内容
- **<h1>** 元素定义一个大标题
- **<p>** 元素定义一个段落

> 基本框架
>
> ```html
> <!DOCTYPE html>
> <html>
> 	<head>
>         
> 	</head>
> 	<body>
>  
> 	</body>
> </html>
> ```



## 各部分详解

1. 标题

   通过<h1> - <h6> 标签来定义

2. 段落

   通过标签 <p> 来定义

3. 链接

   通过标签 <p> 来定义

4. 图像

   通过标签 <img> 来定义

5. 表格

   通过标签 <img> 来定义

## 速查列表

### 基本标签

```HTML
<h1>最大的标题</h1>
<h2> . . . </h2>
<h3> . . . </h3>
<h4> . . . </h4>
<h5> . . . </h5>
<h6>最小的标题</h6>
 
<p>这是一个段落。</p>
<br> （换行）
<hr> （水平线）
<!-- 这是注释 -->
```

### 文本格式化

```html
<b>粗体文本</b>
<code>计算机代码</code>
<em>强调文本</em>
<i>斜体文本</i>
<kbd>键盘输入</kbd> 
<pre>预格式化文本</pre>
<small>更小的文本</small>
<strong>重要的文本</strong>
 
<abbr> （缩写）
<address> （联系信息）
<bdo> （文字方向）
<blockquote> （从另一个源引用的部分）
<cite> （工作的名称）
<del> （删除的文本）
<ins> （插入的文本）
<sub> （下标文本）
<sup> （上标文本）
```

### 链接

```html
普通的链接：<a href="http://www.example.com/">链接文本</a>
图像链接： <a href="http://www.example.com/"><img src="URL" alt="替换文本"></a>
邮件链接： <a href="mailto:webmaster@example.com">发送e-mail</a>
书签：
<a id="tips">提示部分</a>
<a href="#tips">跳到提示部分</a>
```

> <a href="链接地址" target="目标窗口的打开方式">
>
> | target属性值 | 说明                           |
> | :----------- | :----------------------------- |
> | _self        | 默认方式，即在当前窗口打开链接 |
> | _blank       | 在一个全新的空白窗口中打开链接 |
> | _top         | 在顶层框架中打开链接           |
> | _parent      | 在当前框架的上一层里打开链接   |

### 图片

```html
<img src="URL" alt="替换文本" height="42" width="42">
```

### 样式/区块

```html
<style type="text/css">
h1 {color:red;}
p {color:blue;}
</style>
<div>文档中的块级元素</div>
<span>文档中的内联元素（行内元素）</span>
```

### 无序列表

```html
<ul>
    <li>项目</li>
    <li>项目</li>
</ul>
```

### 有序列表

```html
<ol>
    <li>第一项</li>
    <li>第二项</li>
</ol>
```

### 定义列表

```html
<dl>
  <dt>项目 1</dt>
    <dd>描述项目 1</dd>
  <dt>项目 2</dt>
    <dd>描述项目 2</dd>
</dl>
```

### 表格

```html
<table border="1">
  <tr>
    <th>表格标题</th>
    <th>表格标题</th>
  </tr>
  <tr>
    <td>表格数据</td>
    <td>表格数据</td>
  </tr>
</table>
```

### 框架

```html
<iframe src="demo_iframe.htm"></iframe>
```

### 表单

```html
<form action="demo_form.php" method="post/get">
<input type="text" name="email" size="40" maxlength="50">
<input type="password">
<input type="checkbox" checked="checked">
<input type="radio" checked="checked">
<input type="submit" value="Send">
<input type="reset">
<input type="hidden">
<select>
<option>苹果</option>
<option selected="selected">香蕉</option>
<option>樱桃</option>
</select>
<textarea name="comment" rows="60" cols="20"></textarea>
 
</form>
```



# CSS

- 语法：**选择器** + **一条或多条声明**

## 如何创建、引用

### 外部样式表

```html
<!-- main.html -->

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <!--引入外部样式表-->
    <link rel="stylesheet" href="main.css">
</head>
<body>
    <p>外部样式</p>
</body>
</html>
```

```css
// main.css

p {
    color: red;
    text-align: center;
}
```

### 内部样式表

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <!--引入内部样式表-->
    <style>
        p {
            color: red;
            text-align: center;
        }
    </style>
</head>
<body>
    <p>外部样式</p>
</body>
</html>	

```

### 内联样式

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
    <!--引入内联样式-->
    <p style="color: red;text-align: center">外部样式</p>
</body>
</html>

```

> 优先级
>
> 内联式最高
>
> 内部式和外部式冲突时，谁位于下方谁决定

## CSS选择器

### id选择器

> 为标有特定 id 的 HTML 元素指定特定的样式 （标签id唯一且不能重复）

![image-20230430155530455](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230430155530455.png)

### class选择器

> 为标有特定 class 的 HTML 元素指定特定的样式 （标签class不唯一可重复）

![image-20230430155700034](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230430155700034.png)

### 标签选择器

![image-20230430155723531](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230430155723531.png)

### 通配符选择器

> 可以匹配任何标签，常用于统一页面样式

![image-20230430155949341](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230430155949341.png)

### 交集选择器

> 被选择的元素必须同时满足多个条件，定义的时候用 ==标签名.ID名/类名==

![image-20230430160206482](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230430160206482.png)

### 并集选择器

> 多种元素共享某种属性,这时可以使用并集选择器。定义的时候用**逗号** 隔开

![image-20230430160301722](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230430160301722.png)

### 伪类选择器

#### anchor伪类

![image-20230430160513001](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230430160513001.png)

#### input伪类

| 选择器                                                       | 示例               | 示例说明                     |
| ------------------------------------------------------------ | ------------------ | ---------------------------- |
| [:focus](https://www.runoob.com/cssref/sel-focus.html)       | input:focus        | 选择元素输入后具有焦点       |
| [:checked](https://www.runoob.com/cssref/sel-checked.html)   | input:checked      | 选择所有选中的表单元素       |
| [:disabled](https://www.runoob.com/css/cssref/sel-disabled.html) | input:disabled     | 选择所有禁用的表单元素       |
| [:enabled](https://www.runoob.com/cssref/sel-enable.html)    | input:enabled      | 选择所有启用的表单元素       |
| [:in-range](https://www.runoob.com/cssref/sel-in-range.html) | input:in-range     | 选择元素指定范围内的值       |
| [:out-of-range](https://www.runoob.com/cssref/sel-out-of-range.html) | input:out-of-range | 选择元素指定范围外的值       |
| [:invalid](https://www.runoob.com/cssref/sel-invalid.html)   | input:invalid      | 选择所有无效值的元素         |
| [:valid](https://www.runoob.com/cssref/sel-valid.html)       | input:valid        | 选择所有有效值的元素         |
| [:optional](https://www.runoob.com/cssref/sel-optional.html) | input:optional     | 选择没有"required"属性的元素 |
| [:required](https://www.runoob.com/cssref/sel-required.html) | input:required     | 选择含有"required"属性的元素 |
| [:read-only](https://www.runoob.com/cssref/sel-read-only.html) | input:read-only    | 选择只读属性的元素           |
| [:read-write](https://www.runoob.com/cssref/sel-read-write.html) | input:read-write   | 选择可写属性的元素           |

#### other伪类

| 选择器                                                       | 示例                  | 示例说明                                |
| ------------------------------------------------------------ | --------------------- | --------------------------------------- |
| [:not(selector)](https://www.runoob.com/cssref/sel-not.html) | :not§                 | 选择所有p元素以外的元素                 |
| [:empty](https://www.runoob.com/cssref/sel-empty.html)       | p:empty               | 选择所有没有子元素的p元素               |
| [:first-child](https://www.runoob.com/cssref/sel-firstchild.html) | p:first-child         | 选择所有p元素的第一个子元素             |
| [:first-of-type](https://www.runoob.com/cssref/sel-first-of-type.html) | p:first-of-type       | 选择的每个p元素是其父元素的第一个p元素  |
| [:last-child](https://www.runoob.com/cssref/sel-last-child.html) | p:last-child          | 选择所有p元素的最后一个子元素           |
| [:last-of-type](https://www.runoob.com/cssref/sel-last-of-type.html) | p:last-of-type        | 选择每个p元素是其父元素的最后一个p元素  |
| [:nth-child(n)](https://www.runoob.com/cssref/sel-nth-child.html) | p:nth-child(2)        | 选择所有p元素的父元素的正数第二个子元素 |
| [:nth-of-type(n)](https://www.runoob.com/cssref/sel-nth-of-type.html) | p:nth-of-type(2)      | 选择所有p元素正数的第二个为p的子元素    |
| [:nth-last-child(n)](https://www.runoob.com/cssref/sel-nth-last-child.html) | p:nth-last-child(2)   | 选择所有p元素的父元素的倒数第二个子元素 |
| [:nth-last-of-type(n)](https://www.runoob.com/cssref/sel-nth-last-of-type.html) | p:nth-last-of-type(2) | 选择所有p元素倒数的第二个为p的子元素    |
| [:only-child](https://www.runoob.com/cssref/sel-only-child.html) | p:only-child          | 选择所有仅有一个子元素的p元素           |
| [:only-of-type](https://www.runoob.com/cssref/sel-only-of-type.html) | p:only-of-type        | 选择所有仅有一个子元素为p的元素         |
| [:first-letter](https://www.runoob.com/cssref/sel-firstletter.html) | p:first-letter        | 选择每个p元素的第一个字母               |
| [:first-line](https://www.runoob.com/cssref/sel-firstline.html) | p:first-line          | 选择每个p元素的第一行                   |
| [:before](https://www.runoob.com/cssref/sel-before.html)     | p:before              | 在每个p元素之前插入内容                 |
| [:after](https://www.runoob.com/cssref/sel-after.html)       | p:after               | 在每个p元素之后插入内容                 |

### 属性选择器

> 根据元素的属性及属性值来选择元素

![image-20230430160720840](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230430160720840.png)

![image-20230430160739799](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230430160739799.png)

![image-20230430160803688](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230430160803688.png)

## CSS常见样式

### 背景样式

> CSS 背景属性用于定义HTML元素背景的样式。

| 属性                                                         | 描述                                         |
| ------------------------------------------------------------ | -------------------------------------------- |
| [background](https://www.runoob.com/cssref/css3-pr-background.html) | 简写属性，作用是将背景属性设置在一个声明中。 |
| [background-attachment](https://www.runoob.com/cssref/pr-background-attachment.html) | 背景图像是否固定或者随着页面的其余部分滚动。 |
| [background-color](https://www.runoob.com/cssref/pr-background-color.html) | 设置元素的背景颜色。                         |
| [background-image](https://www.runoob.com/cssref/pr-background-image.html) | 把图像设置为背景。                           |
| [background-position](https://www.runoob.com/cssref/pr-background-position.html) | 设置背景图像的起始位置。                     |
| [background-repeat](https://www.runoob.com/cssref/pr-background-repeat.html) | 设置背景图像是否及如何重复。                 |

### 文本样式

> CSS 文本属性用于定义HTML文本内容的样式。

| 属性                                                         | 描述                       |
| ------------------------------------------------------------ | -------------------------- |
| [color](https://www.runoob.com/cssref/pr-text-color.html)    | 设置文本颜色。             |
| [direction](https://www.runoob.com/cssref/pr-text-direction.html) | 设置文本方向。             |
| [letter-spacing](https://www.runoob.com/cssref/pr-text-letter-spacing.html) | 设置字符间距。             |
| [line-height](https://www.runoob.com/cssref/pr-dim-line-height.html) | 设置行高。                 |
| [text-align](https://www.runoob.com/cssref/pr-text-text-align.html) | 对齐元素中的文本。         |
| [text-decoration](https://www.runoob.com/cssref/pr-text-text-decoration.html) | 向文本添加修饰。           |
| [text-indent](https://www.runoob.com/cssref/pr-text-text-indent.html) | 缩进元素中文本的首行。     |
| [text-shadow](https://www.runoob.com/cssref/css3-pr-text-shadow.html) | 设置文本阴影。             |
| [text-transform](https://www.runoob.com/cssref/pr-text-text-transform.html) | 控制元素中的字母。         |
| [unicode-bidi](https://www.runoob.com/cssref/pr-text-unicode-bidi.html) | 设置或返回文本是否被重写。 |
| [vertical-align](https://www.runoob.com/cssref/pr-pos-vertical-align.html) | 设置元素的垂直对齐。       |
| [white-space](https://www.runoob.com/cssref/pr-text-white-space.html) | 设置元素中空白的处理方式。 |
| [word-spacing](https://www.runoob.com/cssref/pr-text-word-spacing.html) | 设置字间距。               |

### 字体样式

> CSS 字体属性用于定义HTML内容字体的样式。

| 属性                                                         | 描述                                 |
| ------------------------------------------------------------ | ------------------------------------ |
| [font](https://www.runoob.com/cssref/pr-font-font.html)      | 在一个声明中设置所有的字体属性。     |
| [font-family](https://www.runoob.com/cssref/pr-font-font-family.html) | 指定文本的字体系列。                 |
| [font-size](https://www.runoob.com/cssref/pr-font-font-size.html) | 指定文本的字体大小。                 |
| [font-style](https://www.runoob.com/cssref/pr-font-font-style.html) | 指定文本的字体样式。                 |
| [font-variant](https://www.runoob.com/cssref/pr-font-font-variant.html) | 以小型大写字体或者正常字体显示文本。 |
| [font-weight](https://www.runoob.com/cssref/pr-font-weight.html) | 指定字体的粗细。                     |

### 列表样式

| 属性                                                         | 描述                                                 |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| [list-style](https://www.runoob.com/cssref/pr-list-style.html) | 简写属性，用于把所有用于列表的属性设置于一个声明中。 |
| [list-style-image](https://www.runoob.com/cssref/pr-list-style-image.html) | 将图像设置为列表项标志。                             |
| [list-style-position](https://www.runoob.com/cssref/pr-list-style-position.html) | 设置列表中列表项标志的位置。                         |
| [list-style-type](https://www.runoob.com/cssref/pr-list-style-type.html) | 设置列表项标志的类型。                               |

### 表格样式

> CSS 表格属性用于定义HTML表格的样式。

| 属性                                                         | 描述                                 |
| ------------------------------------------------------------ | ------------------------------------ |
| [border-collapse](https://www.w3school.com.cn/cssref/pr_tab_border-collapse.asp) | 设置是否把表格边框合并为单一的边框。 |
| [border-spacing](https://www.w3school.com.cn/cssref/pr_tab_border-spacing.asp) | 设置分隔单元格边框的距离。           |
| [caption-side](https://www.w3school.com.cn/cssref/pr_tab_caption-side.asp) | 设置表格标题的位置。                 |
| [empty-cells](https://www.w3school.com.cn/cssref/pr_tab_empty-cells.asp) | 设置是否显示表格中的空单元格。       |
| [table-layout](https://www.w3school.com.cn/cssref/pr_tab_table-layout.asp) | 设置显示单元、行和列的算法。         |

### 表格样式

> CSS 表格属性用于定义HTML表格的样式。

| 属性                                                         | 描述                                 |
| ------------------------------------------------------------ | ------------------------------------ |
| [border-collapse](https://www.w3school.com.cn/cssref/pr_tab_border-collapse.asp) | 设置是否把表格边框合并为单一的边框。 |
| [border-spacing](https://www.w3school.com.cn/cssref/pr_tab_border-spacing.asp) | 设置分隔单元格边框的距离。           |
| [caption-side](https://www.w3school.com.cn/cssref/pr_tab_caption-side.asp) | 设置表格标题的位置。                 |
| [empty-cells](https://www.w3school.com.cn/cssref/pr_tab_empty-cells.asp) | 设置是否显示表格中的空单元格。       |
| [table-layout](https://www.w3school.com.cn/cssref/pr_tab_table-layout.asp) | 设置显示单元、行和列的算法。         |







