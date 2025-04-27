# JavaScript DOM对象

## 接口

- `Node` 节点接口
- `NodeList` 节点集合接口
- `HTMLCollection` 节点集合接口
- `ParentNode` 父节点接口
- `ChildNode` 子节点接口

## Node 类型

- `Node.ELEMENT_NODE = 1` 元素节点（element）
- `Node.ATTRIBUTE_NODE = 2` 属性节点（attr）
- `Node.TEXT_NODE = 3` 文本节点（text）
- `Node.COMMENT_NODE = 8` 注释节点（Comment）
- `Node.DOCUMENT_NODE = 9` 文档节点（document）
- `Node.DOCUMENT_TYPE_NODE = 10` 文档类型节点（DocumentType）
- `Node.DOCUMENT_FRAGMENT_NODE = 11` 文档片断节点（DocumentFragment）

### Node 原型属性

- `Node.prototype.nodeType` 节点类型（r）
- `Node.prototype.nodeName` 节点名称（r）依赖于节点类型
  - `大写标签名` 1
  - `属性名称` 2
  - `#text` 3
  - `#comment` 8
  - `#document` 9
  - `文档类型` 10
  - `#document-fragment` 11
- `Node.prototype.nodeValue` 节点值（rw）依赖于节点类型
  - `文本值` 2/3/8
  - `null` 1/9/10/11
- `Node.prototype.textContent` 节点文本内容（rw）所含标签被忽略
- `Node.prototype.baseURI` 当前网页的绝对路径（r）
  - 若包含`<base href='$uri'>`标签则为该标签定义的绝对路径
- `Node.prototype.ownerDocument` 返回当前节点所在的顶层文档对象，即document对象
- `Node.prototype.nextSibling` 返回当前节点紧邻的下一个同级节点 | null
- `Node.prototype.previousSibling` 返回当前节点紧邻的上一个同级节点 | null
- `Node.prototype.parentNode` 返回当前节点的父节点 | null（![9|1|11]）
- `Node.prototype.parentElement` 返回当前节点的父元素节点 | null（![1]）
- `Node.prototype.firstChild` 返回当前节点的第一个子节点 | null
- `Node.prototype.lastChild` 返回当前节点的最后一个子节点 | null
- `Node.prototype.childNodes` 返回一个类似数组的对象（NodeList集合），成员包括当前节点的所有子节点
- `Node.prototype.isConnected` 返回一个布尔值，表示当前节点是否在文档之中（create but not append）

### Node 原型方法

```js
// 接受一个节点对象作为参数，将其作为最后一个子节点，插入当前节点，返回插入文档的子节点
Node.prototype.appendChild(node)

// 返回一个布尔值，表示当前节点是否有子节点
Node.prototype.hasChildNodes()

// 克隆一个节点，接受一个布尔值作为参数，表示是否同时克隆子节点，返回一个克隆出来的新节点
Node.prototype.cloneNode(true|false)

// 将某个节点插入父节点内部的指定位置，返回新插入的节点node
Node.prototype.insertBefore(node, target)

// 接受一个子节点作为参数，用于从当前节点移除该子节点，返回被移除的子节点
Node.prototype.removeChild(node)

// 将一个新的节点，替换当前节点的某一个子节点，返回被替换的子节点target
Node.prototype.replaceChild(node, target)

// 返回一个布尔值，'指定节点=当前节点|是当前节点的子节点|是当前节点的后代节点'时返回true
Node.prototype.contains(node)

// 返回与当前节点的关系，6bit值
// 0:  两个节点相同
// 1:  两节点不在同一文档，即其中一个尚未append进文档
// 2:  在当前节点前
// 4:  在当前节点后
// 8:  当前节点的父节点
// 16: 当前节点的子节点
// 32: 浏览器内部使用
Node.prototype.compareDocumentPosition(node) 

// 返回一个布尔值，用于检查两个节点是否相等，即两个节点的类型相同、属性相同、子节点相同
Node.prototype.isEqualNode()

// 返回一个布尔值，表示两个节点是否为同一个节点
Node.prototype.isSameNode()

// 用于清理当前节点内部的所有文本节点，去除空的文本节点，合并毗邻的文本节点
Node.prototype.normalize()

// 返回当前节点所在文档的根节点document
Node.prototype.getRootNode()
```

## NodeList 对象

- 通过`Node.prototype.childNodes()`、`document.querySelectorAll()`等节点搜索方法获得

### NodeList 原型属性

- `NodeList.prototype.length`

### NodeList 原型方法

```js
// 遍历执行
NodeList.prototype.forEach(function(item, i, list){...}, this)

// 返回指定序号的成员，等效于nodelist[i]
NodeList.prototype.item(i)

// 返回键名迭代器
NodeList.prototype.keys()

// 返回键值迭代器
NodeList.prototype.values()

// 返回键名键值对迭代器
NodeList.prototype.entries()
```

## HTMLCollection 集合

- 集合只能包含元素节点
- 通过`document.links`、`document.forms`、`document.images`等获得

### HTMLCollection 原型属性

- `HTMLCollection.prototype.length`

### HTMLCollection 原型方法

```js
 // 返回指定序号的成员，等效于htmlCollection[i]
HTMLCollection.prototype.item(i)

// 返回指定id或name属性的成员 | null
HTMLCollection.prototype.namedItem(id|name)
```

## ParentNode 父节点

- 当前节点作为父节点可用的属性和方法

### ParentNode 属性

- `ParentNode.children` 返回一个HTMLCollection实例，其成员为当前节点的所有元素子节点
- `ParentNode.firstElementChild` 返回第一个子元素节点 | null
- `ParentNode.lastElementChild` 返回最后一个元素节点 | null
- `ParentNode.childElementCount` 返回子元素节点数 | 0

### ParentNode 方法

```js
// 为当前节点追加一个或多个子节点（元素|文本），位置是最后一个元素子节点的后面，无返回
ParentNode.append()

// 为当前节点追加一个或多个子节点（元素|文本），位置是在第一个元素子节点的前面，无返回
ParentNode.prepend()
```

## ChildNode 子节点

- 当前节点作为父节点可用的属性和方法

### ChildNode 方法

```js
// 从父节点移除当前节点
ChildNode.remove()

// 用于在当前节点的前面，插入一个或多个同级节点（元素|文本）
ChildNode.before()

// 用于在当前节点的后面，插入一个或多个同级节点（元素|文本）
ChildNode.after()

// 将当前节点替换为指定节点（元素|文本）
ChildNode.replaceWith()
```

## Document 文档节点

- document对象继承了EventTarget接口、Node接口、ParentNode接口
- 对像获取方式
  - 正常网页（document | window.document）
  - iframe框架里面的网页（iframe节点的contentDocument属性）
  - ajax操作返回的文档（XMLHttpRequest对象的responseXML属性）
  - 内部节点（节点ownerDocument属性）

### 快捷方式属性

- `document.defaultView` 返回document对象所属的window对象 | null
- `document.doctype` 文档类型节点，HTML文档则为`<!DOCTYPE html>` | null
- `document.documentElement` 文档根元素节点（root），HTML文档则为`<html>`
- `document.head` 文档`<head>`节点
- `document.body` 文档`<body>`节点
- `document.scrollingElement` 返回文档滚动元素
  - 标准模式下返回`<html>`
  - 兼容模式下返回`<body>`
- `document.scrollingElement.scrollTop = 0;` 页面滚动到浏览器顶部
- `document.activeElement` 返回获得当前焦点（focus）的DOM元素
  - 通常为`<input>`、`<textarea>`、`<select>`等表单元素|`<body>`|null
- `document.fullscreenElement` 返回当前以全屏状态展示的DOM元素，如'全屏播放视频'时的元素

### 节点集合属性

- `document.links` 返回一个HTMLCollection实例，成员为当前文档所有设定了href属性的`<a>`和`<area>`节点
- `document.forms` 返回一个HTMLCollection实例，成员为当前文档所有`<form>`表单节点
- `document.images` 返回一个HTMLCollection实例，成员为当前文档所有`<img>`图像节点
- `document.embeds` 返回一个HTMLCollection实例，成员为当前文档所有`<embed>`节点
- `document.plugins` 返回一个HTMLCollection实例
- `document.scripts` 返回一个HTMLCollection实例，成员为当前文档所有`<script>`节点
- `document.styleSheets` 返回一个StyleSheetList实例，成员为当前文档所有内嵌或引入的CSS样式表

### 静态信息属性

- `document.documentURI` 返回文档地址，继承于Document接口，可用于所有文档
- `document.URL` 返回文档地址，继承于HTMLDocument接口，只能用于HTML文档
- `document.domain` 返回当前文档的域名，不包含协议和端口
- `document.location` 返回Location对象
- `document.lastModified` 返回表示当前文档最后修改的时间的字符串（不同浏览器的返回的日期格式不一致）

```js
var lastVisitedDate = Date.parse('01/01/2018');
if (Date.parse(document.lastModified) > lastVisitedDate) {'网页已经变更'};
```

- `document.title` 返回当前文档的标题，默认为`<title>`节点的值
- `document.characterSet` 返回当前文档的编码，如UTF-8、ISO-8859-1等
- `document.referrer` 返回一个字符串，表示当前文档的访问者来自哪里，与HTTP头信息的Referer字段保持一致，注意拼写不同
- `document.dir` 返回一个字符串，表示文字方向，'rtl'右到左，如阿拉伯文，'ltr'左到右，如中文、英文等大多数文字
- `document.compatMode` 返回浏览器处理文档的模式，值为BackCompat（向后兼容模式）或CSS1Compat（严格模式）

### 状态信息属性

- `document.hidden` 返回一个布尔值，表示当前页面是否可见（窗口最小化、浏览器切换Tab都会导致页面不可见）
- `document.visibilityState` 返回文档的可见状态，四种可能值
  - `visible` 页面可见
  - `hidden` 页面不可见
  - `prerender` 页面处于正在渲染状态
  - `unloaded` 页面从内存里卸载了
- `document.readyState` 返回当前文档的状态，三种可能值
  - `loading` 加载HTML代码阶段（尚未完成解析）
  - `interactive` 加载外部资源阶段
  - `complete` 加载完成

### 其他属性

- `document.cookie` 用来操作浏览器Cookie
- `document.designMode` 控制当前文档是否可编辑，值为on|off，默认off不可编辑
- `document.currentScript` 当前`<script>`元素节点
- `document.implementation` 返回一个DOMImplementation对象，该对象有三个方法，主要用于创建独立于当前文档的新文档对象

```js
// 创建一个 XML 文档
DOMImplementation.createDocument()

// 创建一个 HTML 文档
DOMImplementation.createHTMLDocument()

// 创建一个 DocumentType 对象
DOMImplementation.createDocumentType()
```

### 文档方法

```js
// 清除当前文档所有内容，使得文档处于可写状态，供document.write方法写入内容
document.open()

// 用来关闭document.open()打开的文档
document.close()

// 向当前文档写入内容
document.write()

// 向当前文档写入内容，尾部添加换行符'\n'（源代码换行），注意页面内容换行需显示写入<br>
document.writeln()

// 接受一个 CSS 选择器作为参数，返回首次匹配该选择器的元素节点
document.querySelector()

// 返回一个NodeList对象，包含所有匹配给定选择器的节点
document.querySelectorAll()

// 返回一个HTMLCollection实例，成员为tag符合条件的元素（该方法可在任何元素节点上调用）
document.getElementsByTagName()

// 返回一个HTMLCollection实例，成员为class符合条件的元素（该方法可在任何元素节点上调用）
document.getElementsByClassName()

// 返回一个NodeList实例，成员为name属性符合条件的元素
document.getElementsByName()

// 返回匹配指定id属性的元素节点（具有唯一性）
document.getElementById()

// 返回位于页面指定位置最上层的元素节点，相对于当前窗口视图左上角的横坐标和纵坐标
document.elementFromPoint(x,y)

// 返回位于页面指定位置的所有元素节点
document.elementsFromPoint(x,y)

// 生成元素节点，并返回该节点
document.createElement()

// 生成文本节点，并返回该节点，用户输入内容不会被浏览器当作HTML代码渲染，避免 XSS 攻击
document.createTextNode()

// 生成属性节点，并返回该节点
document.createAttribute()

var attr = document.createAttribute('name');
attr.value = '张三';

// 生成注释节点，并返回该节点，参数为注释内容
document.createComment()

// 生成一个空的文档片段对象（DocumentFragment实例）
document.createDocumentFragment()

// 生成一个事件对象（Event实例），该对象可以被element.dispatchEvent方法使用，触发指定事件
document.createEvent()

// 继承自EventTarget接口，添加事件监听器
document.addEventListener()

// 继承自EventTarget接口，移除事件监听器
document.removeEventListener()

// 继承自EventTarget接口，触发事件
document.dispatchEvent()

// 返回一个布尔值，表示当前文档之中是否有元素被激活或获得焦点
document.hasFocus()

// 将指定节点从原文档中剥离出来，形成尚未append状态的新节点
document.adoptNode()

// 将指定节点从原文档中拷贝出来，形成尚未append状态的新节点
document.importNode()

// 返回一个子节点遍历器（NodeFilter实例），参数分别为要遍历的根节点和节点类型
// NodeFilter.SHOW_ALL     所有节点
// NodeFilter.SHOW_ELEMENT 元素节点
// NodeFilter.SHOW_TEXT    文本节点
// NodeFilter.SHOW_COMMENT 注释节点
document.createNodeIterator(root, type)

NodeFilter.nextNode() // 下一节点
NodeFilter.previousNode() // 上一节点

// 返回一个 DOM 的子树遍历器（TreeWalker实例）
document.createTreeWalker()

// 文档可编辑或元素可编辑状态时，该方法改变内容的样式
document.execCommand()

// 返回一个布尔值，表示浏览器是否支持document.execCommand()的某个命令
document.queryCommandSupported()

// 返回一个布尔值，表示当前是否可用document.execCommand()的某个命令
document.queryCommandEnabled()

// 方法指向window.getSelection()
document.getSelection()
```

## Element 元素节点

- Element对象继承了Node接口
- 不同元素因功能差异除Element对象属性和方法，可能存在各自独有的属性和方法

### 元素特性相关属性

- `Element.id` id属性
- `Element.tagName` 标签名
- `Element.dir` 文字方向
- `Element.accessKey` 快捷键（Alt组合键）
- `Element.draggable` 当前元素是否可拖动（布尔值）
- `Element.lang` 当前元素的语言设置
- `Element.tabIndex` Tab键遍历时的顺序号（-1不遍历）
- `Element.title` title属性，鼠标悬浮时弹出的文字提示框

### 元素状态相关属性

- `Element.hidden` hidden属性，用来控制当前元素是否可见（布尔值）
- `Element.contentEditable` contentEditable属性，元素的内容可编辑
- `Element.isContentEditable` 检查是否可编辑（布尔值）

### 元素其他属性

- `Element.attributes` 返回一个类似数组的对象，成员是当前元素节点的所有属性节点
- `Element.className` 读写当前元素的class属性，形式'c1 c2'
- `Element.classList` 读写当前元素的class属性，形式['c1', 'c2']

```js
// 增加一个 class
classList.add()

// 移除一个 class
classList.remove()

// 检查当前元素是否包含某个 class
classList.contains()

// 将某个 class 移入或移出当前元素
classList.toggle()

// 返回指定索引位置的 class
classList.item()

// 将 class 的列表转为字符串
classList.toString()
```

- `Element.dataset` 读写自定义的'data-'属性
  - 属性 data-xxxx-yyyy
  - 访问方式 e.dataset.xxxxYyyy
- `Element.innerHTML` 读写该元素包含的所有HTML代码，文本中的`& < >`会被转义为`&amp; &lt; &gt;`
- `Element.outerHTML` 读写该元素及包含的所有HTML代码，与innerHTML的区别在于包含了元素本身
- `Element.clientHeight` 块级元素有效，'本身 + padding - 滚动条'，不包含border & margin
- `Element.clientWidth` 块级元素有效
- `Element.clientLeft` 元素left边框宽度，不含padding & margin
- `Element.clientTop`元素top边框的宽度
- `Element.scrollHeight` 在client的基础上 + 溢出容器当前不可见的部分，即内容实际所需占位
- `Element.scrollWidth`
- `Element.scrollLeft` 滚动条向右滚动的像素数量
- `Element.scrollTop` 滚动条向下滚动的像素数量
- `Element.offsetParent` 返回最靠近当前元素、并且 CSS 的position属性不等于static的上层元素
- `Element.offsetHeight` 本身 + padding + border + 滚动条，不含margin
- `Element.offsetWidth`
- `Element.offsetLeft` 相对于Element.offsetParent的位移，通常为相对父节点的位移
- `Element.offsetTop`
- `Element.style` 每个元素节点都有style用来读写该元素的行内样式信息
- `Element.children` 返回HTMLCollection实例，包含当前元素节点的所有子元素
- `Element.childElementCount` 子元素数量，等同于Element.children.length
- `Element.firstElementChild` 第一个子元素
- `Element.lastElementChild` 最后一个子元素
- `Element.nextElementSibling` 下一个同级元素
- `Element.previousElementSibling` 上一个同级元素

### 元素方法

- 属性相关方法

```js
// 读取某个属性的值
Element.getAttribute()

// 返回当前元素的所有属性名
Element.getAttributeNames()

// 写入属性值
Element.setAttribute(k, v)

// 某个属性是否存在
Element.hasAttribute()

// 当前元素是否有属性
Element.hasAttributes()

// 删除属性
Element.removeAttribute()
```

- 元素选择方法

```js
// 返回父元素的第一个匹配的子元素
Element.querySelector()

// 返回NodeList实例，包含所有匹配的子元素
Element.querySelectorAll()

// 返回HTMLCollection实例，成员是当前元素节点的所有具有指定 class 的子元素节点
Element.getElementsByClassName()

// 返回HTMLCollection实例，成员是当前节点的所有匹配指定标签名的子元素节点
Element.getElementsByTagName()

// 接受一个 CSS 选择器作为参数，返回匹配该选择器的、最接近当前节点的一个祖先节点（包括当前节点本身）
Element.closest()

// 返回布尔值，表示当前元素是否匹配给定的 CSS 选择器
Element.matches()
```

- 事件方法

```js
// 添加事件的回调函数
Element.addEventListener()

// 移除事件监听函数
Element.removeEventListener()

// 触发事件
Element.dispatchEvent()
```

- 其他方法

```js
// 滚动当前元素，进入浏览器的可见区域
Element.scrollIntoView()

// 返回一个对象，提供当前元素节点的大小、位置等信息，基本上就是 CSS 盒状模型的所有信息
Element.getBoundingClientRect()

// 由于元素相对于视口（viewport）的位置，会随着页面滚动变化，因此表示位置的四个属性值，都不是固定不变的
// 如果想得到绝对位置，可以将left属性加上window.scrollX，top属性加上window.scrollY
boundingClientRect = {
    x:      '元素左上角相对于视口的横坐标',
    y:      '元素左上角相对于视口的纵坐标',
    height: '元素高度',
    width:  '元素宽度',
    left:   '元素左上角相对于视口的横坐标，与x属性相等',
    right:  '元素右边界相对于视口的横坐标（等于x + width）',
    top:    '元素顶部相对于视口的纵坐标，与y属性相等',
    bottom: '元素底部相对于视口的纵坐标（等于y + height）',
}

// 除x,y坐标外的6个属性
Element.getClientRects()

// 在相对于当前元素的指定位置，插入一个新的节点
// beforebegin 当前元素之前
// afterbegin 当前元素内部的第一个子节点前面
// beforeend 当前元素内部的最后一个子节点后面
// afterend 当前元素之后
Element.insertAdjacentElement(position, element)

Element.insertAdjacentHTML(position, html)
Element.insertAdjacentText(position, text)

// 继承自 ChildNode 接口，用于将当前元素节点从它的父节点移除
Element.remove()

// 将焦点转移到当前元素
Element.focus()

// 将焦点从当前元素移除
Element.blur()

// 在当前元素上模拟一次鼠标点击，相当于触发了click事件
Element.click()
```

## Text 文本节点

- 代表元素节点（Element）和属性节点（Attribute）的文本内容

### Text 属性

- `Text.data` 等同于nodeValue
- `Text.wholeText`
- `Text.length`
- `Text.nextElementSibling` 下一个同级元素节点
- `Text.previousElementSibling` 上一个同级元素节点

### Text 方法

```js
// 节点尾部追加字符串
Text.appendData()

// 删除节点内部的子字符串，第一个参数为子字符串开始位置，第二个参数为子字符串长度
Text.deleteData()

// 在节点内插入字符串，第一个参数为插入位置，第二个参数为插入的子字符串
Text.insertData()

// 替换文本，第一个参数为替换开始位置，第二个参数为需要被替换掉的长度，第三个参数为新加入的字符串
Text.replaceData()

// 获取子字符串，第一个参数为子字符串开始位置，第二个参数为子字符串长度
Text.subStringData()

// 移除当前节点
Text.remove()

// 一分为二，参数为分割位置，返回后半段，原文本节点为前半段
Text.splitText()
```

## DocumentFragment 文档片段节点

- 完全继承Node节点和ParentNode接口，没有自身特有的属性和方法
