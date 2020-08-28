# HTML基础介绍

超文本标记语言 (英语：**H**yper**t**ext **M**arkup **L**anguage，简称：HTML ) 是一种用来结构化 Web 网页及其内容的标记语言。

## 万维网（[World Wide Web]([https://zh.wikipedia.org/wiki/%E4%B8%87%E7%BB%B4%E7%BD%91](https://zh.wikipedia.org/wiki/万维网)))

> 万维网并不等同[互联网](https://zh.wikipedia.org/wiki/網際網路)，万维网只是互联网所能提供的服务其中之一，是靠着互联网运行的一项服务。

由李爵士（Sir Timothy John Berners-Lee）发明，当然也是创造的HTML、HTTP协议和第一个浏览器，实现服务器与客户端的通讯，因“发明了万维网、第一个浏览器和使得万维网得以扩展的基础协议及算法”而获得2016年度的[图灵奖](https://zh.wikipedia.org/wiki/图灵奖)。

## 计算机文本编码

[维基百科]([https://zh.wikipedia.org/wiki/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BC%96%E7%A0%81](https://zh.wikipedia.org/wiki/计算机编码))

常在HTML源码的开头就看到有`<meta charset="UTF-8">`

一般指定文档的字符集为UTF-8，包含了人类语言中大部分的文字。

## 基础的HTML文件

```html
<!DOCTYPE html>
<html>
    <head>
        <titl>基本的HTML结构</titl>
    </head>
    <body>
        <h1>
            我是一级标题，h1~h6共六级标题
        </h1>
  		<!-- HTML注释用这个 -->
        <p>
            这是一段文字
        </p>
    </body>
</html>
```

html 元素 是顶级元素或叫根元素，只能包含 head 或 body 元素。head元素存放元数据，即HTML文档本身的数据。内容放到body元素里面。

head元素大致放三种内容：

1. 描述网页的基本信息
2. 指向渲染网页需要的其他文件链接，如CSS、JavaScript
3. 各大厂商根据自己需要的定制信息

### 标签（tag)

如展示代码中的`<titl>基本的HTML结构</titl>` ，**开始标签 + 内容 + 结束标签**；`<img>  <input> ` 等，还有类似的单标签元素(Empty element)。

## HTML属性

属性放在开始标签里，`属性名 = "属性值"`，注意值都用用双引号，如`<a href="index.html" title="首页"> 首页 </a>`。还有的属性值是布尔属性，如`<input type="text" disable>`，只有是否两种值，所以写上和不写上各代表一种就完事了。

HTML属性基本分为三种：

1. [全局属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes) ==> class、id、title、style等
2. 某一类元素属性
3. 某一个元素属性

## 常用基本元素

1. 标题（heading）：分为六级`<h1>~<h6>`一般最多用到三到四级表体，不要加大、加粗标题，会影响无障碍访问和搜索引擎优化。要保持页面结构清晰，标题整洁、不要标题级别跳跃。

2. 段落（paragraph）：`<p></p>`

3. 图片（image）：`<img>`

4. 链接/锚（anchor）：`<a></a>`标签有`href`属性植入链接，（hypertext reference 超文本引用）。

5. 列表（list）：

   1. 有序列表(ordered list) 用`<ol></ol>`标签

   2. 无序列表（unordered list）用`<ul></ul>`标签

      两种列表中的每个列表项目(list item)用`<li></li>`标签

6. division：`<div>`元素 (或 HTML 文档分区元素) 是一个通用型的流内容容器,就是没语义

7. span：`<span>`元素，同样没有语义，是短语内容的通用行内容器，和`<div>`很相似，但`<div>`是一个[块级元素](https://developer.mozilla.org/en-US/docs/Web/HTML/Block-level_elements)，`<span>`是[行内元素](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements)

块级元素默认占据正行宽度；行内元素同行显示，默认宽度由内容决定。

## Other

需要了解[HTML实体字符](https://developer.mozilla.org/en-US/docs/Glossary/Entity) 

[查询实体字符](https://entitycode.com/)

# `<a>`:The Anchor element

HTML中的`<a>`元素主要是通过其标签的href（hypertext reference 超文本引用）属性指向网页或页面内指定的位置、文件、邮箱地址，只要可以用URL寻址的皆可以用此标签做链接。

此标签基本练习实例：[a标签创建链接](https://nshj.github.io/own-lab/htmlbook/html-exercise/00-a标签创建链接.html)

## 常用属性

该元素的属性包含全局属性。

`title`(全局属性)：提供所属元素相关的解释、咨询信息，当鼠标滑过暂停时，会有一个提示title效果。

`href`: 取值可以为指向目标页面地址。指向的链接不限于基于HTTP的URL，浏览器支持的URL方案都可以：

- 锚点，标签的name或者id等唯一属性值就是锚点的名称（name属性HTML5已不推荐在这里使用，锚点名称既然是唯一的，那id的唯一性更符合这的气质吧），href取值为“#+锚点名称”，当取值为空、#、#TOP时，点击链接会返回页面顶部
- 电话地址：href取值为“tel:+电话”
- 邮箱地址：href取值为“mail:+邮箱地址”

`target`:用怎样的方式呈现链接的窗口,默认是在当前窗口打开:

- _self:当前窗口打开,为默认值,即不写target属性也用这个方式打开新链接
- _blank:新窗口打开(经常使用此值)
- _parent:在当前框架的父框架打开(一般用于iframe中,暂不了解)
- _top:在顶层框架打开(一般用于iframe中,暂不了解)

`<download>`：此属性为设置要下载的链接，即告诉浏览器，不是打开是下载；属性值为命名的文件名。

# `<img>`:The Image  Embed element

主要是通过此标签让文本嵌入图片,通过标签的src(source)属性，这个属性是此标签必须的；`<img>`标签没有闭合标签.

此标签基本练习实例： [img标签创建图片](https://nshj.github.io/own-lab/htmlbook/html-exercise/01-img标签创建图片.html)

## 常用属性

`src`：必需属性，URL指向图片来源地址。

`alt`(alternative)：

1. 一条对图片的文本描述，不是必需属性，但对无障碍访问友好，屏幕阅读器会读出描述图片的文本信息
2. 当图片加载失败，文字会显示出来

# `<ol>`&`<ul>`&`<dl>`

The Ordered &Unordered List &Description(Definition) List element；有序和无序列表就和markdown里面显示的一样,基本理解为带数字和不带数字；

此标签基本练习实例：[ol&ul&dl标签创建列表](https://nshj.github.io/own-lab/htmlbook/html-exercise/02-ol&ul&dl标签创建列表.html)

这里要提一下，两种列表只能包含`<li>`标签，其次`<li>`标签里面可以继续嵌套列表，也就是说可以列表套列表，但写代码的时候要注意分清嵌套逻辑，别写混乱了。

`<dl>`元素的列表一般用来描述定义术语等，`<dt>`内的作为标题`<dd>`作为描述的列表项，以术语为例，术语名在`<dt>`里，描述解释的内容在`<dd>`，可以有多条描述，也可以有多条术语。

# `<table>`:The Table element

`<table>`标签来表现二维表格中的信息.

此标签基本练习实例：[table标签创建表格](https://nshj.github.io/own-lab/htmlbook/html-exercise/03-table标签创建表格.html)

## `<table>`使用的相关标签

在上面的练习demo里就用了基本的子标签做了个表格，基本结构如下：

```html
<table>
	<thead>
		<tr>
			<th>姓名</th>
			<th>政治</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>马大帅</td>
			<td>60</td>
		</tr>
	</tbody>
</table>
```

表格嵌套在内使用的基础常用标签：

* `<thead>`：表头,毕竟有的表格不止一行是表头；用它和`<tbody>`一起在表格里使用，在结构方面，更清晰的看出表头与表数据的部分
* `<tbody>`：表的数据主体，与`<thead>`一起服用效果好

* `<tr>`(Table Row)：此标签内代表表格的一行，标签内嵌入`<td>`或者`<th>`
* `<td>`：应该是表格的最小单位了，代表一个数据单元
* `<th>`：一样代表数据单元，不同的是它囊括的是表头的数据单元

还有一些表格嵌套在内使用的标签：

* `<caption>`：顾名思义，表格的标题；如果使用，它是嵌套在`<table>`标签里的第一个子元素
* `<tfoot>`：把它和`<thead><tbody>`放到一起来理解就不难了：有头，有脚，有身子，这样就构成了完整的表格的表达。你可以用它来表示做表格数据合计的最后一行，当然这三个标签需要在具体的表格下灵活运用，比如在最最简单的两行表格中可能只用`<tr>`囊括完了。
* `<colgroup>`：defines a group of columns within a table，用它表示表格中的一组列。（不了解怎么使用）

更多`<table>`相关联其他标签的使用，还需要慢慢实践中摸索和多查[MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table)。  



# 