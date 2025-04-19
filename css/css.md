# CSS

层叠样式表（Cascading Style Sheets）

## 主要术语

- 元素（element）
- 标签（tag）
- 选择器（selector）
- 声明块（declaration block）
- 属性（property）
- 值（value）

## 使用方式

### 内联样式（Inline Styles）

```html
<p style="font-family:sans-serif;color:#3366CC">AA</p>
```

### 内部样式（Internal Styles）

```html
<style type="text/css">
p { font-family:sans-serif; color:#3366CC; }
</style>
<p>AA</p>
```

### 外部样式（External Styles）

```html
 <link rel="stylesheet" type="text/css" href="mystyle.css" />
```

```css
/* mystyle.css */
p {
    font-family:sans-serif;
    color:#3366CC;
}
```

## 语法

- 规则

```text
selector,...,selector{property:value;property:value;...;property:value;}
```

- 注释

```text
/* 注释 */
```

## 选择器（selector）

### 元素选择器

- `tag {一组标签}`

```html
<style type="text/css">p {}</style>
<p>段落1</p>
<p>段落2</p>
```

- `tag1,tag2 {多组标签}`

```html
<style type="text/css">h1,h2 {}</style>
<h1>标题1</h1>
<h2>标题2</h2>
```

- `tag1 tag2 {后代标签}`

```html
<style type="text/css">table td {}</style>
<table>
    <tr>
        <td>序号</td>
        <td>名称</td>
    </tr>
</table>
```

- `tag1>tag2 {子代标签}`

```html
<style type="text/css">div > p {}</style>
<div>
    <p>子代</p>
    <div>
        <p>后代</p>
    </div>
</div>
```

- `tag1+tag2 {后续相邻一个兄弟}`

```html
<style type="text/css">div + p {}</style>
<div></div>
<p>相邻</p>
<p>不相邻</p>
```

- `tag1~tag2 {后续同级多个兄弟}`

```html
<style type="text/css">th ~ tr {}</style>
<table>
    <th><td></td></th>
    <tr>兄弟1</tr>
    <tr>兄弟2</tr>
</table>
```

### ID选择器（`#`）

```html
<style type="text/css">#main {}</style>
<div id="main">需设置id属性</div>
```

### CLASS选择器（`.`）

```html
<style type="text/css">.info {}</style>
<div class="info">需设置class属性</div>
```

### Pseudo伪类/伪元素选择器（`:`）

```text
selector:pseudo-class {property:value;}
selector:pseudo-element {property:value;}
selector.class:pseudo-class {property:value;}
selector.class:pseudo-element {property:value;}
```

```html
<style type="text/css">a:link {} a.red:visited {}</style>
<a>超链接</a>
<a class="red">超链接</a>
```

#### anchor伪类

- `:link` 未访问的链接，例：a:link{}
- `:visited` 已访问的链接
- `:hover` 鼠标划过链接
- `:active` 已选择的链接

#### status伪类

- `:enabled` 已启用的表单元素，例：input:enabled{}
- `:disabled` 被禁用的表单元素
- `:valid` 有效值的元素
- `:invalid` 无效值的元素
- `:in-range` 范围内值的元素
- `:out-of-range` 超范围值的元素
- `:read-only` 只读属性的元素
- `:read-write` 读写属性的元素
- `:checked` 已选中的表单元素
- `:focus` 获得焦点的元素
- `:required` 设置required属性的元素
- `:optional` 未设置required属性的元素

#### index伪类

- `:empty` 没有子元素的元素
- `:only-child` 仅有一个子元素的元素
- `:only-of-type` 仅有一个子元素为该类型的元素
- `:first-of-type` 该类型的第一个元素
- `:last-of-type` 该类型的最后一个元素
- `:nth-of-type(n)` 该类型的第n个元素
- `:nth-last-of-type(n)` 该类型的倒数第n个元素
- `:first-child` 第一个子元素
- `:last-child` 最后一个子元素
- `:nth-child(n)` 第n个子元素
- `:nth-last-child(n)` 倒数第n个子元素
- `:first-letter` 第一个字母
- `:first-line` 第一行
- `:before` 元素之前的内容
- `:after` 元素之后的内容
- `:not(selector)` 非指定元素的元素
- `:lang(language)` 设置属性lang="{language}"的元素

#### other伪类

- `:root` 选择文档的根元素
- `:target` 由属性href设定锚点

```html
<a href="section1">section 1</a>
<p id="section1">content</p>
```

### 元素属性选择器（`[]`）

- `[attr] {设置attr属性的元素}`
- `[attr=value]{且值为value的元素}`
- `[attr~=value]{且值包含value的元素}`
- `[attr|=value]{且值以value开头的元素，支持-连接符`
- `[attr*=value]{且值能模糊匹配到value的元素`
- `[attr^=value]{且值以value开头的元素}`
- `[attr$=value]{且值以value结尾的元素}`

## 属性（property）

### 背景（background）

- `background-color` 背景色

```css
background-color: #ff0000; /*十六进制*/
background-color: rgb(255,0,0); /*RGB*/
background-color: rgb(10%,90%,10%);
background-color: red; /*颜色名称*/
background-color: transparent; /*无色透明*/
```

- `background-image` 背景图像

```css
/* 默认水平或垂直方向平铺 */
background-image: url('xxxx.png');
```

- `background-position` 背景图像位置

```css
background-position: center; /* top right bottom left center inherit */
background-position: top center;
/* xpos ypos */
background-position: 0% 0%; /*左上角（默认值）*/
background-position: 100% 100%; /*右下角*/
background-position: 0px 0px; /*左上角（坐标原点）*/
```

- `background-size` 背景图像大小

```css
background-size: auto; /*自动（默认值）*/
background-size: cover; /*保持纵横比缩放区域最小*/
background-size: contain; /*保持纵横比缩放区域最大*/
background-size: 80% 100%; /*宽高缩放比列*/
background-size: 200px 50px; /*宽高固定尺寸*/
```

- `background-repeat` 背景图像平铺

```css
background-repeat: repeat; /*平铺（默认值）*/
background-repeat: no-repeat; /*不平铺*/
background-repeat: repeat-x; /*仅水平方向*/
background-repeat: repeat-y; /*仅垂直方向*/
background-repeat: round; /*循环*/
```

- `background-attachment` 背景图像滚动

```css
background-attachment: scroll; /*滚动（initial默认值）*/
background-attachment: fixed; /*不随页面滚动*/
background-attachment: local; /*随元素内容滚动*/
background-attachment: inherit;
```

- `background` 背景综合

```css
/*颜色 图像 位置 大小 平铺 滚动*/
background: #00ff00 url('xxxx.png') no-repeat fixed;
```

### 文本（text）

- `color` 文本颜色

```css
color: #ff0000; /*rgb()、颜色名称、transparent*/
```

- `direction` 文本方向

```css
direction: ltr; /*从左到右（默认值）*/
direction: rtl; /*从右到左*/
direction: inherit;
```

- `letter-spacing` 字符间距
- `word-spacing` 字间距

```css
letter-spacing,word-spacing: normal; /*默认值*/
letter-spacing,word-spacing: 3px; /*允许负值*/
letter-spacing,word-spacing: inherit;
```

- `line-height` 文本行高

```css
line-height: normal; /*默认值*/
line-height: 1.5; /*基于当前字体尺寸的倍数*/
line-height: 150%; /*基于当前字体尺寸的比列数*/
line-height: inherit;
```

- `text-align` 文本对齐

```css
text-align: left;
text-align: right;
text-align: center;
text-align: justify; /*两端对齐*/
text-align: inherit;
```

- `vertical-align` 垂直对齐

```css
vertical-align: baseline; /*父元素基线（默认值）*/
vertical-align: top;
vertical-align: middle;
vertical-align: bottom;
vertical-align: text-top; /*文本顶*/
vertical-align: text-bottom; /*文本底*/
vertical-align: super; /*文本上标*/
vertical-align: sub; /*文本下标*/
vertical-align: inherit;
```

- `text-indent` 首行缩进

```css
text-indent: 5px; /*允许负值*/
text-indent: 10%; /*基于父元素宽度的百分比*/
text-indent: inherit;
```

- `text-transform` 文本大小写

```css
text-transform: none; /*不转换（默认值）*/
text-transform: capitalize; /*每单词首字母大写*/
text-transform: uppercase; /*转大写*/
text-transform: lowercase; /*转小写*/
text-transform: inherit;
```

- `white-space` 空白处理

```css
white-space: normal; /*忽略（默认值）*/
white-space: pre; /*保留*/
white-space: nowrap; /*不换行*/
white-space: pre-wrap; /*换行*/
white-space: pre-line; /*合并*/
white-space: inherit;
```

- `text-decoration`

```css
text-decoration: none; /*标准文本（默认值）*/
text-decoration: underline; /*下划线*/
text-decoration: overline; /*上划线*/
text-decoration: line-through; /*删除线*/
text-decoration: blink; /*闪烁*/
text-decoration: underline overline dotted red; /*线 线类型 颜色*/
text-decoration: inherit;
```

- `text-shadow` 文本阴影

```css
/* <h-shadow水平> <v-shadow垂直> [blur模糊] [color颜色] */
text-shadow: 2px 2px 4px red;
```

### 字体（font）

- `font-family` 字体家族

```css
font-family: "Times New Roman"; /*具体字体名称（family-name）：items、courier、arial等*/
font-family: serif; /*通常字体名称（generic-family）：sans-serif、cursive、fantasy、monospace等*/
font-family: 仿宋,宋体; /*可设置多个家族以逗号分隔，浏览器按顺序优先选用*/
font-family: inherit;
```

- `font-style` 字体样式

```css
font-style: normal; /*默认值*/
font-style: italic; /*字库斜体*/
font-style: oblique; /*非字库斜体也能倾斜*/
font-style: inherit;
```

- `font-size` 字体大小

```css
font-size: 12px;
font-size: 0.8em;
font-size: 80%;
/* 模量大小*/
font-size: xx-small;
font-size: xx-large;
font-size: x-small;
font-size: x-large;
font-size: small;
font-size: medium;
font-size: large;
font-size: smaller;
font-size: larger;
font-style: inherit;
```

- `font-weight` 字体粗细

```css
font-weight: normal; /*默认值*/
font-weight: 700; /*由细到粗 100 200 ... 900*/
font-weight: bold; /*粗体*/
font-weight: bolder;
font-weight: lighter;
font-weight: inherit;
```

- `font-variant` 字体变形

```css
font-variant: normal; /*默认值*/
font-variant: small-caps; /*转为大写字母，并保持原小写字母的大小*/
font-variant: inherit;
```

- `font` 字体综合

```css
/* font-style font-variant font-weight font-size/line-height font-family */
font: italic bold 12px/30px Georgia, serif;
```

### 列表（list）

```html
<!-- 无序 ul -->
<ul><li></li><li></li></ul>
<!-- 有序 ol -->
<ol><li></li><li></li></ol>
```

- `list-style-type` 列表项标记类型

```css
/*无序*/
list-style-type: none;
list-style-type: disc; /*实心圆*/
list-style-type: circle; /*空心圆*/
list-style-type: square; /*实心方块*/
/*有序*/
list-style-type: decimal; /*数字 1 2 3*/
list-style-type: decimal-leading-zero; /*数字 01 02 03*/
list-style-type: lower-roman; /*小写罗马数字 i ii iii*/
list-style-type: upper-roman; /*大写罗马数字 I II III*/
list-style-type: lower-alpha; /*小写英文字母 a b c*/
list-style-type: upper-alpha; /*大写英文字母 A B C*/
list-style-type: lower-latin; /*小写拉丁字母*/
list-style-type: upper-latin; /*大写拉丁字母*/
list-style-type: lower-greek; /*小写希腊字母 alpha、beta、gamma*/
```

- `list-style-position` 列表项标记位置

```css
list-style-position: outside; /*文本不以标记对齐（默认值）*/
list-style-position: inside; /*文本以标记对齐*/
list-style-position: inherit;
```

- `list-style-image` 列表项标记图像

```css
list-style-image: none; /*默认值*/
list-style-image: url('xxx.gif');
list-style-image: inherit;
```

- `` 列表项标记综合

```css
/* list-style-type list-style-position list-style-image */
list-style: disc inside none;
```

### 表格（table）

```html
<table>
    <caption>标题</caption>
    <tr><th>列名</th><th>列名</th></tr>
    <tr><td>内容</td><td>内容</td></tr>
</table>
```

- `caption-side` 标题位置

```css
caption-side: top;
caption-side: bottom;
```

- `table-layout` 表格布局

```css
table-layout: auto; /*自适应内容*/
table-layout: fixed; /*固定大小*/
```

- `border-collapse` 单元格边框

```css
border-collapse: seqarate; /*分离，拥有各自的边框*/
border-collapse: collapse; /*折叠，相连的边框共用，border-spacing和empty-cells被忽略*/
```

- `border-spacing` 单元格间距

```css
border-spacing: 10px 5px; /*x y*/
```

- `empty-cells` 空单元格

```css
empty-cells: hide; /*隐藏*/
empty-cells: show; /*显示*/
```

### 尺寸（dimension）

- `width` 宽
- `height` 高
- `max-width` 最大宽度
- `max-height` 最大高度
- `min-width` 最小宽度
- `min-height` 最小高度
- `line-height` 行高

### 显示（display）

```html
<!-- 块元素 -->
<h1></h1>
<p></p>
<div></div>
<!-- 内联元素 -->
<span></span>
<a></a>
```

- `display` 显示样式

```css
display: none; /*掩藏元素，不占用布局空间*/
display: block; /*块元素，独占整行*/
display: inline; /*内联元素，与相连元素在同一行*/
display: inline-block; /*内联块元素，可设置块属性，如列表li元素在同行显示*/
display: list-item; /*列表项*/
display: table-cell; /*表格单元格*/
```

- `visibility` 可见性

```css
visibility: hidden; /*掩藏元素，占用布局空间*/
visibility: visible; /*可见*/
visibility: collapse; /*折叠，相当于hidden*/
```

### 定位（position）

- `top` 偏移
- `right`
- `bottom`
- `left`
- `position` 定位方式

```css
position: static; /*静态（默认值）正常文档流，无定位 top、right、bottom、left 失效*/
position: fixed; /*固定，相对浏览器窗口固定位置，且不随窗口滚动，相当于浮动层，不占用布局空间*/
position: relative; /*相对，基于元素原本布局所占用空间的相对偏移，原占空间不变*/
position: absolute; /*绝对，相对于最近已定位父元素的绝对偏移，相当于浮动层，不占用布局空间*/
position: sticky; /*粘性，随窗口滚动至浏览器边界后不再跟随滚动、反方向滚动时再粘回原位置随着滚动*/
position: inherit;
```

- `z-index` 图层堆叠

```css
/*前提（position:absolute|relative|fixed）*/
z-index: auto;
z-index: 100; /*图层号 -1 1 100 值大置顶*/
z-index: inherit;
```

- `cursor` 光标形状

```css
cursor: auto; /*默认值 default 鼠标移入元素边界范围内时*/
cursor: url('xxx.gif') auto; /*为避免未获取到自定义光标，需在最后追加其他有效值*/
cursor: crosshair; /*十字*/
cursor: pointer; /*手形*/
cursor: text; /*竖线*/
cursor: wait; /*沙漏*/
cursor: help; /*问号*/
cursor: move; /*可移动*/
```

- `clip` 裁剪

```css
clip: auto; /*默认值*/
clip: rect(0px,50px,100px,0px); /* rect(top,right,bottom,left) */
clip: inherit;
```

- `overflow` 溢出
- `overflow-x`
- `overflow-y`

```css
overflow: auto; /*默认值*/
overflow: scroll; /*滚动*/
overflow: hidden; /*掩藏*/
overflow: visible; /*可见，显示在框外*/
overflow: inherit;
```

- `float` 浮动

```css
float: none;
float: left; /*向左浮动*/
float: right; /*向右浮动*/
float: inherit;
```

- `clear` 清除浮动

```css
clear: none; /*允许两侧*/
clear: left; /*不允许左侧*/
clear: right; /*不允许右侧*/
clear: both; /*两侧都不允许*/
clear: inherit;
```

### 盒子模型（box model）

#### 盒子模型术语

- `outline` 轮廓（其宽度不计算在元素尺寸内）
- `margin` 外边距
- `border` 边框
- `padding` 内边距
- `content` 内容

#### 赋值逻辑

- `x` 上右下左
- `x y` 上下 左右
- `x y z` 上 左右 下
- `top right bottom left` 上 右 下 左

#### 盒子属性

- `border-style` 边框类型
- `border-top-style`
- `border-right-style`
- `border-bottom-style`
- `border-left-style`

```css
border-style: none; /*无边框*/
border-style: hidden; /*隐藏*/
border-style: dotted; /*点状*/
border-style: dashed; /*虚线*/
border-style: solid; /*实线*/
border-style: double; /*双线*/
border-style: groove; /*凹槽*/
border-style: ridge; /*垄状*/
border-style: inset; /*内嵌*/
border-style: outset; /*外凸*/
border-style: inherit;
```

- `border-width` 边框宽度
- `border-top-width`
- `border-right-width`
- `border-bottom-width`
- `border-left-width`

```css
border-width: thin; /*细*/
border-width: medium; /*中等*/
border-width: thick; /*粗*/
border-width: 5px;
border-width: inherit;
```

- `border-color` 边框颜色
- `border-top-color`
- `border-right-color`
- `border-bottom-color`
- `border-left-color`

```css
border-color: #ff0000; /*rgb()、transparent*/
border-color: invert; /*反色*/
border-color: inherit;
```

- `border` 边框综合
- `border-top`
- `border-right`
- `border-bottom`
- `border-left`

```css
/* border-width border-style border-color */
border: 5px solid red;
```

- `outline` 轮廓
- `outline-style` 轮廓类型
- `outline-width` 轮廓宽度
- `outline-color` 轮廓颜色

```css
/* outline-width outline-style outline-color */
outline: 1px dotted gray;
```

- `margin` 外边距
- `margin-top`
- `margin-right`
- `margin-bottom`
- `margin-left`

```css
margin: auto;
margin: 5px; /*px pt em 允许负值*/
margin: 120%;
```

- `padding` 内边距
- `padding-top`
- `padding-right`
- `padding-bottom`
- `padding-left`

```css
padding: 5px; /*px pt em 允许负值*/
padding: 120%;
```

### 对齐（align）

```css
/* 元素水平居中 */
display: block; /*非块元素需设置*/
margin: auto;
width: 50%;
```

```css
/* 文本水平居中 */
text-align: center;
```

```css
/* 左右对齐，同时设置left和right为0相当于居中 */
position: absolute;
left: 0px;
right: 0px;
```

```css
/* 左右浮动对齐 */
width: 200px;
float: left;
float: right;
```

```css
/* 垂直居中 */
padding: 70px 0;
```

```css
/* 垂直居中 */
height: 200px;
line-height: 200px;
```

```css
/* 多行文本垂直居中 */
display: inline-block;
line-height: 1.5;
vertical-align: middle;
```
