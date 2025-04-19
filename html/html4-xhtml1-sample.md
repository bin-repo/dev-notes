# html 4.0 - xhtml 1.0 sample

## HTML 4.0

### HTML 4.01 Strict

- html4-strict.html

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 //EN" "http://www.w3.org/TR/html4/strict.dtd">
<html lang="en">
<head>
    <title>Title</title>
</head>
<body>
</body>
</html>
```

### HTML 4.01 Transitional

- html4-transitional.html

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html lang="en">
<head>
    <!-- 头元素：title、meta、base、link、script -->

    <title>Title</title>

    <!-- <meta name="Description | Keyword | Author"> -->
    <meta content="网页描述" name="Description">
    <meta content="搜索引擎关键字" name="Keyword">
    <meta content="作者" name="Author">

    <!-- <meta http-equiv="Refresh | Content-Type"> -->
    <meta content="60;URL=http://www.baidu.com" http-equiv="Refresh"><!-- 定时刷新[;URL=跳转地址]-->
    <meta content="text/html;charset=UTF-8" http-equiv="Content-Type"><!-- 内容类型[;字符编码] -->

    <!-- <base href="../"> -->
    <base href="http://www.sample.com/"><!-- 地址须以/结尾 -->

    <!-- <link  type="text/css"> -->
    <link rel="stylesheet" type="text/css" href="xxx.css">

    <!-- <script type="text/javascript">脚本内容</script> -->
    <script type="text/javascript" src="xxx.js"></script>
</head>
<body>
    <!-- 字体样式 -->

    <!-- <font>字体样式，size=1~7</font> -->
    <font color="blue" face="宋体" size="1">宋体 #1</font>

    <!-- <h1~6 align="left | center | right">标题层次<h1~6> -->
    <h1 align="center">标题 #1</h1>
    <h2 align="center">标题 #2</h2>
    <h3 align="center">标题 #3</h3>
    <h4 align="center">标题 #4</h4>
    <h5 align="center">标题 #5</h5>
    <h6 align="center">标题 #6</h6>

    <!-- b、i、u、s、sup、sub、big、small、strong、em、address、code -->
    <b>粗体</b>
    <i>斜体</i>
    <u>下划线</u>
    <s>删除线</s>
    <sup>上标</sup>
    <sub>下标</sub>
    <big>大字体</big>
    <small>小字体</small>
    <strong>突出粗体</strong>
    <em>突出斜体</em>
    <address>缩小斜体</address>
    <code>缩小体</code>

    <!-- p、br、hr、pre -->
    <p>段落</p>
    <br>换行
    <hr>水平线
    <pre>预格式化，原样输出</pre>

    <!-- div（块标记）、span（行内块标记） -->
    <div id="块标记"></div>
    <span id="行内块标记" ></span>

    <!-- 列表 -->

    <!-- 无序列表 <ul type="disc | circle | square"><li></li></ul> -->
    <ul type="disc"><li>无序列表 ul-li</li><li>无序列表 ul-li</li></ul>
    <ul type="circle"><li>无序列表 ul-li</li><li>无序列表 ul-li</li></ul>
    <ul type="square"><li>无序列表 ul-li</li><li>无序列表 ul-li</li></ul>

    <!-- 有序列表 <ol type="1 | A | a | I | i" start="n"><li></li></ol> -->
    <ol type="1" start="0"><li>有序列表 ol-li</li><li>有序列表 ol-li</li></ol>
    <ol type="A" start="3"><li>有序列表 ol-li</li><li>有序列表 ol-li</li></ol>
    <ol type="a" start="3"><li>有序列表 ol-li</li><li>有序列表 ol-li</li></ol>
    <ol type="I" start="3"><li>有序列表 ol-li</li><li>有序列表 ol-li</li></ol>
    <ol type="i" start="3"><li>有序列表 ol-li</li><li>有序列表 ol-li</li></ol>

    <!-- 定义、解释、关键字描述 -->

    <!-- dl、dt、dd -->
    <dl><dt>术语</dt><dd>术语描述</dd></dl>

    <!-- 表格 -->

    <!-- <table、caption、tr、th、td、thead、tbody、tfoot -->
    <table border="1" cellpadding="5" cellspacing="5" bgcolor="darkgrey"><!-- 边框、内边距、外边距、背景色 -->
        <caption>标题</caption>
        <tr bgcolor="green" align="center">
            <th>列名称</th><th>列名称</th><!-- rowspan="跨行数" colspan="跨列数" -->
        </tr>
        <tr bgcolor="lightblue" align="left">
            <td>列记录</td><td>列记录</td><!-- rowspan="跨行数" colspan="跨列数" -->
        </tr>
        <thead>分页打印时表头</thead>
        <tbody>分页打印时表体</tbody>
        <tfoot>分页打印时表尾</tfoot>
    </table>

    <!-- 表单 -->

    <form action="action.do" method="get" id="form" name="form1" enctype="multipart/form-data"><!-- method = get | post -->
        <label>文本输入：<input type="text" value="abc" size="18" maxlength="32"></label>
        <label>口令输入：<input type="password" value="123" size="8"></label>
        <label>单项选择：<input type="radio" name="sex" value="male" checked><input type="radio" name="sex" value="female"></label>
        <label>多项选择：<input type="checkbox" name="pet" value="dog" checked><input type="checkbox" name="pet" value="cat" checked></label>
        <label>文件选取：<input type="file" name="filename" accept="image/gif,image/bmp,image/jpg"></label><!-- 提交含路径全名 -->
        <label>隐藏内容：<input type="hidden" value="hidden" disabled></label>
        <label>提交按钮：<input type="submit" value="submit"></label>
        <label>复位按钮：<input type="reset" value="reset"></label>
        <label>普通按钮：<input type="button" value="button"></label>
        <label>图片按钮：<input type="image" src="xxx.jpg" alt="图片未找到时提示内容"></label><!-- 提交相对坐标 -->
        <label>多行文本：<textarea rows="3" cols="3">123456789</textarea></label>
        <label>下拉列表：<select name="choice"><optgroup label="联系方式"><option>电话</option><option>微信</option></optgroup></select></label>
        <!--分组-->
        <fieldset>
            <legend>组标题</legend>
            <label><input></label>
            <label><input></label>
        </fieldset>
    </form>

    <!-- 图像映射 -->

    <img src="xxx.jpg" alt="xxx" height="" width="" align="middle" border="边框" vspace="垂直间距" hspace="水平间距" usemap="my-map">

    <map name="my-map" id="my-map">
        <area alt="圆形" shape="circle" href="映射" coords="x坐标,y坐标,r半径">
        <area alt="矩形" shape="rect" href="映射" coords="left左,top上,right右,bottom下">
        <area alt="多边" shape="poly" href="映射" coords="x1,y1,...,xn,yn">
    </map>

    <!-- 媒体对象 -->

    <object data="xxx.mpg" type="video/mpeg" width="" height="">
        <param name="src" value="xxx.mpg">
        <param name="autoplay" value="autoplay">
    </object>

    <!-- 常用转义字符 -->

    &amp; <!-- &和 -->
    &nbsp; <!-- 空格 -->
    &lt; &gt; <!-- 小于、大于 -->
    &lsquo; &rsquo; <!-- 单引号左、右 -->
    &ldquo; &rdquo; <!-- 双引号左、右 -->
    &ndash; &mdash; <!-- 破折号 -->
    &copy; &trade; &reg; <!-- © 版权、™ 商标、® 注册商标 -->

</body>
</html>
```

### HTML 4.01 Frameset

- html4-frameset.html

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">
<html lang="en">
<head>
    <title>Title</title>
</head>
<frameset rows="180,*,30%">
    <frame frameborder="0" marginheight="5" marginwidth="5" scrolling="no" noresize src="top.html">
    <frameset cols="200,*,20%">
        <frame frameborder="0" marginheight="5" marginwidth="5" scrolling="auto" src="left.html">
        <frame frameborder="1" marginheight="5" marginwidth="5" scrolling="yes" src="main.html">
        <frame frameborder="1" marginheight="5" marginwidth="5" scrolling="no" src="right.html">
    </frameset>
    <frame frameborder="1" marginheight="5" marginwidth="5" scrolling="no" src="bottom.html">
    <noframes>
        <body>
            <p>
                This page uses frames, but your browser does not support them.
                <br/>
                <br/>
                Frames: 
                <a href="top.htm">Top</a>, 
                <a href="left.htm">Left</a>,
                <a href="main.htm">Main</a>,
                <a href="right.htm">Right</a>,
                <a href="bottom.htm">Bottom</a>
            </p>
        </body>
    </noframes>
</frameset>
</html>
```

## XHTML 1.0

### XHTML 1.0 Strict

- xhtml1-strict.xhtml

```html
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
    <title>Title</title>
</head>
<body>
</body>
</html>
```

### XHTML 1.0 Transitional

- xhtml1-transitional.xhtml

```html
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
    <title>Title</title>
</head>
<body>
</body>
</html>
```

### XHTML 1.0 Frameset

- xhtml1-frameset.xhtml

```html
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
    <title>Title</title>
</head>
    <frameset cols="250,*">
        <frame name="left_nav" src="left_nav.htm" frameborder="0" scrolling="no" />
        <frame name="main" src="main.htm" frameborder="1" />
        <noframes>
            <body>
                <p>
                    This page uses frames, but your browser does not support them.
                    <br/>
                    <br/>
                     Frames: 
                    <a href="left_nav.htm">Navigation</a>, 
                    <a href="main.htm">Content</a>
                 </p>
            </body>
        </noframes>
    </frameset>
</html>
```
