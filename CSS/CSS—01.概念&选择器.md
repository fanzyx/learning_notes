# CSS概念

> <p style="font-size:18px">什么是CSS</p>
> <p style="color:blue">CSS是Cascading Style Sheet （级联样式表）的缩写，可以对字体、颜色、边距、高度、宽度、背景图片、网页定位等进行设定</p>

***

> <p style="font-size:18px">CSS的优势</p>
> <p style="color:blue">1.内容与样式分离</p>
> <p style="color:blue">2.网页的表现统一，容易修改</p>
> <p style="color:blue">3.丰富的样式，页面布局更加灵活</p>
> <p style="color:blue">4.减少网页的代码量，增加网页的浏览速度，节省网络带宽</p>

***

> <p style="font-size:18px">CSS在HTML中的引入方式</p>

- 行内样式
```css
<div style="color:blue">行内样式</div>
```
- 内部样式表
```css
<head>
	<meta charset="utf-8">
	<title>CSS学习</title>
	<style type="text/css">
		h1{
			<!-- 设置h1标签的样式 -->
		}
	</style>
</head>
```
- 外部样式表（建议使用此方式）
```css
<head>
	<meta charset="utf-8">
	<title>CSS学习</title>
	<!-- 引入外部css文件 -->
	<link href="../css/learnCSS.css" />
</head>

```

***

> <p style="font-size:18px">CSS样式优先级</p>
> <p style="color:blue">就近原则：行内样式>内部样式>外部样式</p>
为了方便展示，后面将以内部样式表的形式书写，实际开发中建议使用外部样式表。
***

# CSS选择器

![CSS选择器](https://github.com/wyd288/fan1111/blob/master/src/images/CSS%E7%AC%94%E8%AE%B0/CSS%E2%80%941.%E6%A6%82%E5%BF%B5&%E9%80%89%E6%8B%A9%E5%99%A8-%E9%80%89%E6%8B%A9%E5%99%A8.png?raw=true)

> <p style="font-size:18px">基本选择器</p>

- ID选择器

> <p style="color:blue">根据id选择元素使用 #(井号)前缀 ，在同一个页面中id要唯一。</p>

```html
<html>
	<head>
		<meta charset="utf-8">
		<title>CSS学习</title>
		<style type="text/css">
			#id_selector {
			    <!-- 设置元素样式 -->
			}
		</style>
	</head>
	<body>
		<div id="id_selector">ID选择器</div>
	</body>
</html>
```

- 类选择器

> <p style="color:blue">根据class属性选择元素使用 .(点)前缀 ,Class在同一页面中可以有多个相同的值。</p>

```html
<html>
	<head>
		<meta charset="utf-8">
		<title>CSS学习</title>
		<style type="text/css">
			.class_selector {
				<!-- 设置元素样式 -->
			}
		</style>
	</head>
	<body>
	    <div class="class_selector">类选择器</div>	
	</body>
</html>
```

- 标签选择器

> <p style="color:blue">根据标签选择元素使用标签名，如有多个则全部选择。</p>

```html
<html>
	<head>
		<meta charset="utf-8">
		<title>CSS学习</title>
		<style type="text/css">
			p {
			    <!-- 设置元素样式 -->	
			}
		</style>
	</head>
	<body>
		<p id="p_selector">标签选择器</p>
	</body>
</html>
```

> <p style="font-size:18px">高级选择器</p>
'parent'、'child'指代ID选择器、类选择器及标签选择器中的一个，'element'指代标签元素。

- 层次选择器

书写形式| 功能说明
---|---
parent&nbsp;&nbsp;child| 后代元素选择器，选择父元素内所有的子元素。
parent>child| 子元素选择器，选择父元素内所有的子元素，子元素内的子元素无法选择。
element1+element2| 相邻元素选择器,选择与element1下面相邻的第一个元素element2，如果元素类型不匹配则无法选中。
element1~element2| 通用元素选择器,选择与element1下面相邻的所有指定类型元素element2。


- 结构伪类选择器(过滤器)

书写形式| 功能说明
---|---
parent :first-child | 选择父元素的第一个子元素
parent :last-child | 选择父元素的最后一个子元素
parent :nth-child(n) | 选择父元素的第n个子元素
parent element:first-of-type | 选择父元素中第一个类型为element的子元素
parent element:last-of-type | 选择父元素中最后一个类型为element的子元素
parent element:nth-of-type(n) | 选择父元素中第n个类型为element的子元素


- 属性选择器

书写形式| 功能说明
---|---
element[attr] | 选择具有attr属性名的element
element[id ^="first"] | 选择具有id属性且其值是以first开头的element
element[id $="first"] | 选择具有id属性且其值是以first结尾的element
element[id *="first"] | 选择具有id属性且其值包含first的element

***








