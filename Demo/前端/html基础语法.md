---
cssclass:
UID: 20241101184558
tags: "html"
source: 
cssclasses: 
created: "2024-11-01 18:45"
updated: "2024-11-05 19:23"
---

## html基础
### 文本格式化标签

| 标签名    | 效果  | 简化  |
| ------ | --- | --- |
| strong | 加粗  | b   |
| em     | 斜线  | i   |
| ins    | 下划线 | u   |
| del    | 删除线 | s   |

---
### 图像标签

```
<img src="图片位置的URL" alt="图片名称">
```

| #属性    | 作用      | 说明                |
| ------ | ------- | ----------------- |
| alt    | 替换文本    | 图片无法显示的时候显示的文字    |
| title  | 提示文本    | 鼠标悬停在图片上面的时候显示的文字 |
| width  | 图片的宽度   | 值为数字,没有单位         |
| height | 图片的高度   | 值为数字,没有单位         |
| border | 设置图像的粗细 |                   |

### div和span标签
div是单独一行 span跨距

---
### 超链接

```
<a href="跳转目标" target="目标窗口的弹出方式" >文本或图形</a>
```

| #属性    | 作用                                      |     |
| ------ | --------------------------------------- | --- |
| href   | 用于链接目标的url地址                            |     |
| target | 用于指定链接页的打开方式,其中_self为默认值,_blank为在新窗口中打开 |     |
|        |                                         |     |
锚点链接

```
 在链接文本你的href属性中,设置属性值为#名字的形式,如<a href="#我是名字">跳转</a>
要跳到目标位置标签,里面添加一个id属性=刚才的名字,如<h3 id="我是名字">跳转</h3>
```

### 注释
<!---我是注释--->

### 特殊字符

| 特殊字符 | 描述   | 字符的代码    |
| ---- | ---- | -------- |
| 空格   | 空格   | & nbsp;  |
| <    | 小于   | "&lt;"   |
|      | 大于   | &gt;     |
|      | 和号   | &amp;    |
|      | 人民币  | &yen;    |
|      | 版权   | &copy;   |
|      | 注册商标 | &reg;    |
|      |      | &deg     |
|      |      | &plusmn  |
|      |      | &times;  |
|      |      | &divide; |
|      |      | &sup2    |
|      |      | &3       |
|      |      |          |
### 表格标签
#### 用法

```
<table></table>用于定义表格的标签
<tr></tr>用来定义表格中的行,必须嵌套在<table></table>标标签
<td></td>用来定义表格中的单元格,必须嵌套在<tr></tr>标签中
```

#### 表头

```
表头单元格用th
```

#### 属性

| 属性名         | 属性值               | 描述                       |
| ----------- | ----------------- | ------------------------ |
| align       | left,center,right | 规定表格相对周围严肃的对齐方式          |
| border      | 1或者""             | 规定表格单元是否用有边框,默认为""表示没有边框 |
| cellpadding | 像素值               | 规定单元边沿与其内容之间的空白          |
| cellspacing | 像素值               | 规定单元格之间的空白,默认为2像素        |
| width       | 像素值或者百分比          | 规定表格的宽度                  |
#### 表格结构标签

```
<therad>表格头部区域 <thbody>标签的主区域
```

#### 合并单元格

合并单元格的方式
- 跨行合并: rowspan="合并单元格的个数"
- 跨列合并:colspan="合并单元格的个数"
目标单元格(写合并代码)
- 跨行:最上侧单元格为目标单元格,写合并代码
- 跨列:最左侧单元格写合并代码
### 列表
#### 无序列表
<ul>
<li>列表</li>
</ul>
#### 有序列表
<ol>
<li>有序列表</li>
</ol>
#### 自定义列表 #重点
```
<dl>
	<dt>名字</dt>
	<dd>名字</dd>
	<dd>名字</dd>
</dl>
```
### 表单标签
表单的组成
		表单域 表单空间 提示信息
			<form>会把他范围内的表单信息提交给服务器
			 <form action="url地址" method="提交方式" name="表单域名称 ">
			 </form>

1. "< input>"表单元素

```
<input type="属性值"/>
````  

| 属性值      | 描述                              |
| ----------- | --------------------------------- |
| butoon      | 定义可点击按钮                    |
| checkbox    | 复选框                            |
| file        | 定义输入字段和浏览按钮,供文件上传 |
| hidden      | 定义隐藏的输入输入                |
| image       | 定义图像形式的提交按钮            |
| password    | 定义密码字段                      |
| radio       | 定义单选按钮                      |
| reset       | 定义重置按钮                      |
| submit      | 定义提交按钮                      |
| text        | 定义单行输入字段                  |
| name        | 定义input元素的名称               |
| value       | 规定input元素的默认的值           |
| checked     | 规定此input元素首次加载时应被选中 |
| maxlength   | 规定输入自负担最大长度            |
| placeholder | 默认显示                          |
#### lable标签

```
< lable for ="sex"></lable>
<input type="radio" name="sex" id="sex" />
```

#### select表单下拉元素

```
<select>
<option>这是选项</option>
</select>
```

在< o pt ion>中定义selected="selected"时,当前默认选中项

#### < tex tarea> 表单元素

```
<textarea  cols="30" rows="10"></textarea>
```

cols是每行的字数
rows是显示多少行

### 字体属性
#### font-family设置字体

```
css使用font-family属性定义文本的字体系列
```

#### font-size定义字体大小

```
p {
	font-size: 20px;
}
```

#### font-weight设置文本字体的粗细

| 值                                                                            | 描述                                                        |
| ----------------------------------------------------------------------------- | ----------------------------------------------------------- |
| normal                                                                        | 默认值。定义标准的字符。                                    |
| bold                                                                          | 定义粗体字符。                                              |
| bolder                                                                        | 定义更粗的字符。                                            |
| lighter                                                                       | 定义更细的字符。                                            |
| - 100<br>- 200<br>- 300<br>- 400<br>- 500<br>- 600<br>- 700<br>- 800<br>- 900 | 定义由粗到细的字符。400 等同于 normal，而 700 等同于 bold。 |
| inherit                                                                       | 规定应该从父元素继承字体的粗细。                            |
#### font-style文字样式

```
font-style: normal|italic|oblique|initial|inherit;
```

|值|描述|
|---|---|
|normal|默认值。浏览器显示一个标准的字体样式。|
|italic|浏览器会显示一个斜体的字体样式。|
|oblique|浏览器会显示一个倾斜的字体样式。|
|inherit|规定应该从父元素继承字体样式。|
#### font的复合属性
font-style和font-weight可以默认不写,但是font-size和font-family必须有 

```
font: font-style font-weight font-size/line-height font-family;
```

####字体总结

| 属性        | 表示     | 注意点                                  |
| ----------- | -------- | --------------------------------------- |
| font-size   | 字号     | 我们通常用的单位是px像素,一定要跟上单位 |
| font-family | 字体     |                                         |
| font-weight | 字体粗细 | 加粗700或者bold 不加粗是400normal       |
| font-style  | 字体样式 | 倾斜是italic  不倾斜是normal 常用normal |
| font        | 复合属性 | font-style font-weight font-size/lin-height font-family 其中font-style和font-weight是可以省略不写的                                        |
### 文本属性
#### color文本颜色

```
color: red;
```

|值|描述|
|---|---|
|_color_name_|规定颜色值为颜色名称的颜色（比如 red）。|
|_hex_number_|规定颜色值为十六进制值的颜色（比如 #ff0000）。|
|_rgb_number_|规定颜色值为 rgb 代码的颜色（比如 rgb(255,0,0)）。|
|inherit|规定应该从父元素继承颜色。|
#### text-align水平对齐方式

```
text-align: center;
```

| 属性值 | 解释   |
| ------ | ------ |
| left   | 左对齐 |
| right  | 右对齐 |
| center | 居中对齐       |
#### text-decoration装饰文本
text-decoration属性规定添加文本的修饰,可以给文本添加下划线、删除线、上划线等。

| 属性值       | 秒速                   |
| ------------ | ---------------------- |
| none         | 默认.没有装没有        |
| underline    | 下划线.链接a自带下划线 |
| overline     | 上划线                 |
| line-through | 删除线                       |
#### text-indent文本缩进
text-indent 用来指定文本首行缩进

```
text-indent: 10px;
```

em是一个相对单位,就是当前元素(font-size)1个文字的大小,如果当前元素没有设置大小,则会按照父元素的1个文字大小.
#### line-height 行间距

```
line-height:26px;
```

#### 文本属性总结

| 属性            | 表示     | 注意点                                 |
| --------------- | -------- | -------------------------------------- |
| color           | 文本颜色 | 通常用16禁止                           |
| text-align      | 文本对齐 | 可以设定文字水平的对齐方式             |
| text-indent     | 文本缩进 | 通常用段落首行缩进 texe-indent:2em;    |
| text-decoration | 文本修饰 | 添加下划线是underline 取消下划线是none |
| line-height     | 行高     | 控制行与行之间的                                       |
#### 引用外部样式表 

```
<link rel="stylesheet" href="css文件的路径" >
```

![[Pasted image 20241105173428.png]]
### css复合选择器
#### 后代选择器
<font color="red">后代选择器</font>又称为<font color="red">包含选择器</font>,可以被选择父元素.其写法就是把外层标签写在前面,内层标签写在后面 ,中间用空格符分隔,当标签发生嵌套时,内层标签就成为外层标签的后代.

```
元素1 元素2 {样式声明}
```
#### 子选择器
子元素选择器 只能选择作为某元素的最近一级元素.简单理解就是选亲儿子元素
```
元素1>元素2{样式声明}
列如
div>p{样式声明} 选自div里面所有最近一级p标签元素
```
#### 并集选择器
并集选择器可以选择多组标签,同时为他们定义相同的样式
并集选择器
```
元素1 ,元素2{样式声明}
```
#### 伪类选择器
伪类选择器用于向某些选择器添加特殊的效果
伪类选择器书写的最大特点是使用:表示
#### 链接伪类选择器
```
a:link      /*选择所有未被访问的链接*/
a:visited    /*选择所有已被访问的链接*/
a:hover   /*选择鼠标指针位于其上的链接*/
a:active  /*选择活动链接(鼠标按下未弹起的链接)*/
```
链接伪类选择器注意实现
1.为了确保生效,按照LVHA的循序声明: link visited hover active
#### :focus伪类选择器
焦点就是光标,一般情况input表单元素才能获取,因此这个选择器主要针对于表单元素来说的
```
input:focus{
	background-color:yellow;
}
```





