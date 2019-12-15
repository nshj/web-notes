# HTML基础介绍

超文本标记语言 (英语：**H**yper**t**ext **M**arkup **L**anguage，简称：HTML ) 是一种用来结构化 Web 网页及其内容的标记语言。

## 万维网（[World Wide Web]([https://zh.wikipedia.org/wiki/%E4%B8%87%E7%BB%B4%E7%BD%91](https://zh.wikipedia.org/wiki/万维网)))

> 万维网并不等同[互联网](https://zh.wikipedia.org/wiki/網際網路)，万维网只是互联网所能提供的服务其中之一，是靠着互联网运行的一项服务。

由李爵士（Sir Timothy John Berners-Lee）发明，当然也是创造的HTML、HTTP协议和第一个浏览器，实现服务器与客户端的通讯，因“发明了万维网、第一个浏览器和使得万维网得以扩展的基础协议及算法”而获得2016年度的[图灵奖](https://zh.wikipedia.org/wiki/图灵奖)。

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

[返回笔记目录](../README.md)