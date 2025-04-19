# html dom

## HTML DOM 对象方法

- `getElementsByTagName("tag_name")` 返回指定标签名的所有元素对象数组
- `getElementById("ID")` 返回带有指定 id=ID 的元素对象（唯一性）
- `getElementsByClassName("class_name")` 返回带有指定 class=ClassName 的所有元素对象数组
- `appendChild(node)` 追加为子节点
- `removeChild(node)` 删除子节点
- `replaceChild(node_new, node)` 替换为新子节点
- `insertBefore(node_new, node)` 在子节点前插入新子节点
- `createElement("element")` 创建元素节点
- `createAttribute()` 创建属性节点
- `createTextNode("text")` 创建文本节点
- `getAttribute("attr")` 获取属性值
- `setAttribute("attr", "value")` 设置属性值
- `document.write("text")` 文档流中输出内容（若文档加载完成后调用将覆盖文档）

## HTML DOM 对象属性

- `innerHTML` 文本内容
- `parentNode` 父节点
- `childNodes` 所有子节点（数组）
- `firstChild` 第一个子节点
- `lastChild` 最后一个子节点
- `attributes` 所有属性（数组）
- `nodeName` 节点名称（只读）：元素（标签名）属性（属性名）文本（#text）文档（#document）
- `nodeValue` 节点值：元素（undefined | null）文本（文本内容）属性（属性值）
- `nodeType` 节点类型：元素（1）属性（2）文本（3）注释（8）文档（9）
- `style` CSS样式：`style.color` `style.fontFamily` `style.fontSize` `style.backgroundColor` 等
- `id`、`name`、`class`、`src`、`href`、`height`、`width` 等显性属性

## HTML DOM 根节点属性

- `document.documentElement` 全部文档
- `document.body` 文档主体

## HTML DOM 事件

- `onload` 进入页面，可用于检查访客的浏览器类型和版本，以便基于这些信息来加载不同版本的网页
- `onunload` 离开页面
- `onchange` 改变，常用于输入字段的验证
- `onmouseover` 鼠标移入
- `onmouseout` 鼠标移出
- `onmousedown` 鼠标按下
- `onmouseup` 鼠标松开
- `onclick` 鼠标单击
- `ondblclick` 鼠标双击

## HTML DOM 对象（document）

### document 属性

- `document.anchors` 文档中所有锚（数组）`<a name="锚名"></a>` 区别于 `<a href="链接"></a>`
- `document.forms` 文档中所有表单（数组）`<form name="表单名"></form><form></form>`
- `document.images` 文档中所有图像（数组）`<img src="图像">`
- `document.links` 文档中所有链接（数组）指定 `href` 属性的所有元素
- `document.cookie` 文档相关的所有cookie键值对
- `document.domain` 服务器主机域名
- `document.lastModified` 文档最后修改时间
- `document.referrer` 文档引用地址
- `document.title` 文档标题
- `document.URL` 文档完整地址

### document 方法

- `document.open()`
- `document.write()`
- `document.writeln()`
- `document.close()`

```js
// 文档自我覆盖
var doc = document.open("text/html","replace");
doc.write("<!DOCTYPE html><html><body>新文档</body></html>");
doc.close();
```

```js
xmlDoc = loadXMLDoc("test.xml");
document.write(xmlDoc.getElementsByTagName("item")[0].nodeValue);
```
