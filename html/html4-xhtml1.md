# html 4.0 - xhtml 1.0

## Frameset 框架

- `frameset` 标签划分框架区域
- `frame` 标签定义各区域内容
- `noframes` 标签定义浏览器不支持该框架时的显示内容

### frameset 标签属性

- `rows` 行划分（数值、百分比、*）
- `cols` 列划分（数值、百分比、*）
- `frameborder` 框架边框（no、yes、数值）
- `border` 边框（数值）
- `bordercolor` 边框颜色

### frame 标签属性

- `name` 名称
- `src` 区域内容html地址
- `noresize` 是否可调整大小（noresize）
- `scrolling` 是否支持滚动条（yes、no、auto）
- `frameborder` 框架边框（no、yes、数值）
- `bordercolor` 边框颜色
- `marginheight` 外边框高
- `marginwidth` 外边框宽

### 框架示例

```html
<!-- 三行两列 -->
<frameset rows="20,*,20%" cols="50%,50%"></frameset>
<!-- 无边界 -->
<frameset frameborder="no" framespacing="0" border="0"></frameset>
<!-- 有边界 -->
<frameset frameborder="yes" framespacing="20" border="10" bordercolor="#000"></frameset>
<!-- 不可调整大小 -->
<frame name="main" src="main.html" noresize="noresize" scrolling="auto" />
```

```html
<frameset rows="20,*">
    <frame name="top" src="top.html" />
    <frame name="main" src="main.html" />
    <noframes>
        <body>不支持Frameset框架</body>
    </noframes>
</frameset>
```

## Head 头元素

- `meta` 子标签定义元数据
- `base` 子标签定义相对路径的基地址（须以`/`结尾）
- `link` 子标签引入资源文件
- `script` 子标签引入脚本文件

### meta 标签属性

- `name` 元数据名称（Description、Keyword、Author）
- `http-equiv` 定义HTTP响应头信息（Refresh、Content-Type）
- `content` 元数据或响应头信息内容

```html
<meta name="Description" content="my home page">
<meta http-equiv="Refresh" content="3;URL=login.html">
<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
```

### base 标签属性

```html
<base href="../">
```

### link 标签属性

```html
<link rel="stylesheet" type="text/css" href="main.css">
```

### script 标签属性

```html
<script type="text/javascript" src="main.js"></script>
```

## 字体样式

- `font` 字体样式标签
- `h1`,`h2`,`h3`,`h4`,`h5`,`h6` 标题层次标签
- `b` 粗体
- `i` 斜体
- `u` 下划线
- `s` 删除线
- `sup` 上标
- `sub` 下标
- `big` 大字体
- `small` 小字体
- `strong` 突出粗体
- `em` 突出斜体
- `address` 缩小斜体
- `code` 缩小体
- `p` 段落
- `br` 换行
- `hr` 水平线
- `pre` 预格式化
- `left` 左对齐
- `center` 居中对齐
- `right` 右对齐
- `div` 块元素
- `span` 行内块元素

```html
<!-- 字体样式（size=1~7） -->
<font color="blue" face="宋体" size="1"></font>
<!-- 标题层次（1~6） -->
<h1 align="left | center | right"></h1>
<!-- a^2 + b^2 = c^2 -->
a<sup>2</sup>+b<sup>2</sup>=c<sup>2</sup>
<!-- H2O -->
H<sub>2</sub>O
```

## 列表

```html
<!-- 无序列表 -->
<ul type="disk | circle | square"><li></li></ul>
<!-- 有序列表 -->
<ol type="1 | A | a | I | i" start="1 | A | a | I | i"><li></li></ol>
```

## dl 术语定义

```html
<dl>
    <dt>术语</dt>
    <dd>术语描述</dd>
</dl>
```

## table 表格

```html
<!-- cellpadding单元格内边距；cellspacing单元格间距 -->
<table border="1" cellpadding="5" cellspacing="5">
    <caption>标题</caption>
    <tr bgcolor="green" align="center">
        <th rowspan="2">序号</th><th>名称</th>
    </tr>
    <tr>
        <td colspan="2">1</td><td>zhang san</td>
    </tr>
</table>
```

```html
<!-- 打印时分页显示表头、表体、表尾 -->
<table>
    <thead></thead>
    <tbody></tbody>
    <tfoot></tfoot>
</table>
```

## form 表单

### form 标签属性

- `method` 请求方法（get、post）
- `action` 请求地址
- `enctype` 文件上传协议（`multipart/form-data`）

```html
<form method="post" action="file/upload" enctype="multipart/form-data"></form>
```

### 通用属性

- `name`
- `id`
- `tabindex`

### input 标签属性

- `type` 类型（hidden、file、text、password、radio、checkbox、button、image、submit、reset）
- `value`
- `size`
- `maxlength`
- `checked` 勾选状态（checked）
- `disabled` 禁用状态（disabled）
- `accept` 仅用于type=file时限定文件范围（逗号分隔的MIME类型）

```html
<!-- 文件，提交信息时文件名含路径 -->
<input type="file" accept="image/gif" />
<!-- 单选 -->
<input type="radio" value="yes" checked="checked" disabled="disabled" />
<!-- 多选，提交信息时若无value属性则默认值为"on" -->
<input type="checkbox" value="book" />
<!-- 图像，提交信息时含点击该图片的相对坐标 -->
<input type="image" src="go.png" alt="点击图片" />
```

### textarea 标签属性

```html
<!-- 多行文本 -->
<textarea rows="5" cols="16"></textarea>
```

### select 标签属性

```html
<select>
    <optgroup label="分组名">
        <option>选项</option>
    </optgroup>
    <option>选项</option>
</select>
```

## 图像映射

```html
<img src="workspace.jpg" alt="workspace" usemap="#workmap">
<map name="workmap" id="myworkmap">
    <!-- 四边形 coords=左,上,右,下 -->
    <area shape="rect" coords="34,44,270,350" alt="area1" href="/map/area1" />
    <!-- 圆形 coords=x,y,r -->
    <area shape="circle" coords="35,35,4" alt="area2" href="/map/area2" />
    <!-- 多边形 coords=x,y,...,xn,yn -->
    <area shape="poly" coords="10,15,20,25,35,45" alt="area3" href="/map/area3" /> 
</map>
```

## object 媒体对象

```html
<object data="play.mpg" type="video/mpeg" width="200" height="100">
    <param name="src" value="play.mpg" />
    <param name="autoplay" value="autoplay" />
</object> 
```

## fieldset 分组

```html
<fieldset>
    <legend>组标题</legend>
    <label for="username">用户名</label>
    <input name="username" value="" placeholder="请输入" />
</fieldset>
```

## 转义字符

- `&amp;` 与符（&）
- `&nbsp;` 空格
- `&lt;` 小于
- `&gt;` 大于
- `&lsquo;` 左单引号
- `&rsquo;` 右单引号
- `&ldquo;` 左双引号
- `&rdquo;` 右双引号
- `&ndash;` 短横号（—）
- `&mdash;` 长横号（——）
- `&copy;` 版权号（C）&copy;
- `&trade;` 商标号（TM）&trade;
- `&reg;` 注册号（R）&reg;
