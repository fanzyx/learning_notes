# HTML

> <p style="font-size:18px">什么是HTML</p>
> <p style="color:blue">HTML是Hyper Text Markup Language（超文本标记语言）的缩写，包括文字图片音频视频动画等</p>

***

```html
<!DOCTYPE html>
<!-- ↑标签告诉浏览器使用什么标准解析 -->

<!-- HTML的注释形式 -->
<html>
	<head>
		<!-- 设置网页编码 -->
		<meta charset="utf-8" />
		
		<!-- 设置网页标题 -->
		<title>我是网页标题</title>
		
		<!-- 引入CSS样式 -->
		<link rel="stylesheet" href="css/index.css">
		
		<!-- 引入JavaScript脚本 -->
		<script type="text/javascript" src="js/index.js"></script>
	</head>
	<body>

	<h1>我是1级标题</h1>
	<h2>我是2级标题</h2>
	<h3>我是3级标题</h3>
	<h4>我是4级标题</h4>
	<h5>我是5级标题</h5>
	<h6>我是6级标题</h6>
	
	<p>我是段落标签，用于分段</p>
	
	<span>我是行内标签，只能显示一行内容</span>
	
	<br/>换行标签
		
	<hr/>水平线标签
	
	<p>一段正文，现在要为部分文字进行加粗<strong>我被加粗了</strong>和进行斜体化<em>我变斜体了</em>，特殊符号：空格 &nbsp; 大于号 &gt; 小于号 &it; 引号 &quot; 版权符 &copy; 分号不要忘了写</p>
	
	<img src="img/image1.png" title="鼠标悬停时显示此文字" alt="如果图片失效就显示这段文字" width="200" height="200"/>
	
	<br/>
	
	<a href="http://www.fan1111.com" target="_blank">链接标签，跳转到href指向的网址，并用新窗口跳转</a>
	
	<br/>
	
	<a href="http://www.fan1111.com" target="_self">链接标签，跳转到href指向的网址，并用当前窗口跳转</a>
	
	<br/>
	
	<a name="mark">标记锚链接位置</a>
	
	<br/>
	
	<!-- 当锚链接标记与点击链接位置超出浏览器同一页面时会跳转 -->
	<a href="#mark">点击跳转到标记的锚链接</a>
	
	<div>块级结构标签，常用来对页面进行结构化布局</div>
	
	<!-- 有序列表 -->
	<ol>
		<li>声明列表项1</li>
		<li>声明列表项2</li>
		<li>声明列表项3</li>
	</ol>
	
	<!-- 无序列表 -->
	<ul>
		<li>声明列表项1</li>
		<li>声明列表项2</li>
		<li>声明列表项3</li>
	</ul>
	
	<!-- 定义列表 -->
	<dl>
		<dt>声明列表项1</dt>
			<dd>声明表项内容1</dd>
			<dd>声明表项内容2</dd>
			<dd>声明表项内容3</dd>
		<dt>声明列表项2</dt>
			<dd>声明表项内容1</dd>
			<dd>声明表项内容2</dd>
			<dd>声明表项内容3</dd>
		<dt>声明列表项3</dt>
			<dd>声明表项内容1</dd>
			<dd>声明表项内容2</dd>
			<dd>声明表项内容3</dd>
	</dl>
	
	<!-- 声明表格 -->
	<table style="border: black solid 1px;">
		<!-- 行标签---第1行 -->
		<tr>
			<td>第1列</td>
			<td>第2列</td>
		</tr>
		<!-- 行标签---第二行 -->
		<tr>
			<td>第1列</td>
			<td>第2列</td>
		</tr>
		<!-- 行标签---第二行 -->
		<tr>
			<!-- 跨列合并，合并N列 -->
			<td colspan="n">第1列</td>
			<!-- 跨行合并，合并N行 -->
			<td rowspan="n">第2列</td>
		</tr>
	</table>
	
	<br/>
	
	<!-- 视频标签，controls为视频控件 -->
	<video src="视频路径" controls></video>
	
	<br/>
	
	<!-- 音频标签，controls为音频控件 -->
	<audio src="音频路径" controls></audio>
	
	<br/>
	
	<!-- 内联框架 -->
	<!-- 在超链接标签上设置target目标窗口属性为希望显示的框架窗口名 -->
	<iframe src="img/img1.png" name="mainFrame" width="200px" height="200px"></iframe>
	<a href="要显示在内联框架中的网页路径" target="mainFrame">点击跳转</a>
	
	<!-- 表单 -->
	<!-- 设置提交方式method:get/post，提交地址:一般写后端的映射地址 -->
	<form method="get" action="welcome.html" name="myform">

    <p>文本框
        <input type="text" name="username" value="用户名" size="30" maxlength="20" />
    </p>
    
	<p>密码框
        <input type="password" name="password" size="20"/>
    </p>
    
	<p>单选框
        <input type="radio" name="sex" value="男" checked /> 男
        <input type="radio" name="sex" value="女" />女
    </p>
    
	<p>复选框
        <input type="checkbox" name="interest" value="sports" checked />运动
        <input type="checkbox" name="interest" value="chat" />聊天
        <input type="checkbox" name="interest" value="play" />玩游戏
    </p>
	
	列表
    <select name="select" size="显示表项行数，最好设为1">
        <option value="选项的值1" selected>列表选项1</option>
        <option value="选项的值2" >列表选项2</option>
    </select>
    
	<p>按钮
        <input type="button"  value="按钮上显示的文字-普通"/>
        <input type="submit"  value="按钮上显示的文字-提交"/>
        <input type="reset"  value="按钮上显示的文字-重置"/>
    </p>
    
	<p>图片按钮(有提交功能，和提交按钮相同)
        <input type="image" src="img/image1.png" width="40px" height="40px"/>
    </p>
    
	<p>邮箱
        <input type="email" />
        <input type="submit">
    </p>
    
	<p>网址
        <input type="url" />
        <input type="submit">
    </p>
    
	<p>数字
        <input type="number"  min="0" max="100" step="数字间隔" />
        <input type="submit">
    </p>
    
	<p>滑块
        <input type="range"  min="0" max="100" step="滑动间隔" />
        <input type="submit">
    </p>
    
	<p>搜索框
        <input type="search" />
        <input type="submit">
    </p>
    
	<p>隐藏域，内容不会在页面上显示
        <input type="hidden" value="666"  />
    </p>
    
	<p>只读文本框和禁用按钮
        <input type="text" value="张三" name="name" readonly/>
        <input type="submit" disabled value="保存" />
    </p>
	
	<p>表单元素id和label标签
		<input type="radio" name="sex" id="male"/><label for="male">标注的文本男</label>
		<input type="radio" name="sex" id="female"/><label for="female">标注的文本女	</label>
	</p>
    
	<p>正则表达式规则-pattern，初步验证输入的是否为手机号码
    <input type="text" name="tel" placeholder="请输入手机号码" required pattern="^1[358]\d{9}" />
    </p>
	
	<p>多行文本域
        <textarea  cols="显示的列数" rows="显示的行数">文本内容</textarea>
    </p>
    
	<p>文件域
    <form action="welcome.html" method="post" enctype="multipart/form-data">
        <p><input type="file" name="files" width="100" height="100"></p>
        <p><input type="submit" name="upload" value="上传" width="200" height="200">	</p>
    </form>
    </p>

	</form>
	<!-- 提示语：placeholder（适用于input中text/search/url/email/password） -->
	<!-- 必填项：required（适用于text/search/url/email/password/number/checkbox/radio/file） -->

	</body>
</html>
```






