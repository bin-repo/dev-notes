# ajax

## 简介

- `Asynchronous JavaScript and XML` 异步的`javascript`和`xml`技术
- 主要依赖于4种技术（`JS`、`CSS`、`DOM`、`XMLHttpRequest`对象）

## 创建实例对象（xmlHttp）

```js
function createXMLHttpRequest() {
    if (window.ActiveXObject) {
        return new ActiveXObject("Microsoft.XMLHTTP");
    } else if (window.XMLHttpRequest) {
        return new XMLHttpRequest();
    }
}

const xmlHttp = createXMLHttpRequest();
```

## GET请求

```js
function request_get() {
    var url = "http://localhost/test?name=张三";
    xmlHttp.open("GET", url, true); // 是否异步
    xmlHttp.onreadystatechange = callback; // 回调函数
    xmlHttp.send(null);
}
```

## POST请求

```js
function request_post() {
    var params = "name=张三";
    var url = "http://localhost/test";
    xmlHttp.open("POST", url, true);
    xmlHttp.onreadystatechange = callback; // 回调函数
    xmlHttp.send(params);
}
```

## 回调函数

```js
function callback() {
    // 全部响应头参数
    var headers = xmlHttp.getAllResponseHeaders();
    console.log(`headers=${headers}`);
    // 特定响应头参数
    var header_expires = xmlHttp.getResponseHeader("expires");
    console.log(`header expires=${header_expires}`);

    if (xmlHttp.readyState == 4) {
        var str = xmlHttp.responseText;
        document.getElementById("xxx").innerHTML = "<p>" + str + "</p>";
        alert(xmlHttp.responseText);
    }
}
```

## jquery中使用ajax

```js
$.ajax({
    type: "GET",
    url: "http://localhost/test?name=张三",
    async: "true",
    dataType: "text",
    success: function(msg) {...}
});

$.ajax({
    type: "POST",
    url: "http://localhost/test",
    async: "true",
    data: "name=张三"
    dataType: "text",
    success: function(msg) {...}
});
```
