# xml dom

## XML DOM 对象属性

- `x.nodeName` x 的名称
- `x.nodeValue` x 的值
- `x.parentNode` x 的父节点
- `x.childNodes` x 的子节点
- `x.firstChild` x 的第一个子节点
- `x.lastChild` x 的最后一个子节点
- `x.previousSibling` x 的上一同胞节点
- `x.nextSibling` x 的下一同胞节点
- `x.attributes` x 的属性节点

## XML DOM 对象方法

- `x.getElementsByTagName(name)` 获取带有指定标签名称的所有元素
- `x.appendChild(node)` 向 x 插入子节点
- `x.removeChild(node)` 从 x 删除子节点

## 加载XML文档

```js
function loadXMLDoc(dname) {
    if (window.XMLHttpRequest) {
        // IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
        xhttp = new XMLHttpRequest();
    }
    else {
        // IE6, IE5 浏览器执行代码
        xhttp = new ActiveXObject("Microsoft.XMLHTTP");
    }

    xhttp.open("GET", dname, false);
    xhttp.send();

    return xhttp.responseXML;
}
```

```js
xmlDoc = loadXMLDoc("book.xml");
```

## 加载XML字符串

```js
function loadXMLString(txt) {
    if (window.DOMParser) {
        parser = new DOMParser();
        xmlDoc = parser.parseFromString(txt,"text/xml");
    }
    else {
        // Internet Explorer
        xmlDoc = new ActiveXObject("Microsoft.XMLDOM");
        xmlDoc.async = false;
        xmlDoc.loadXML(txt); 
    }

    return xmlDoc;
}
````

```js
xmlDoc = loadXMLString("<books><book><name>1</name><price>1.0</price></book><book><name>2</name><price>2.0</price></book></books>");
```
