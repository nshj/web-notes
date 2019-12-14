# `<table>`:The Table element

`<table>`标签来表现二维表格中的信息.

此标签基本练习实例：[table标签创建表格](../workbook/html-exercise/03-table标签创建表格.html)

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

