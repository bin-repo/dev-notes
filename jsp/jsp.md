# JSP

## 定义

- JSP（Java Server Pages）是一种动态网页技术标准

## 形式

- 在HTML文件中插入Java程序段（Scriptlet）和JSP标记（tag），形成JSP文件（*.jsp）

## 实现

- JSP页面第一次被访问时会被转换（*_jsp.java）和编译（*_jsp.class），最终作为Servlet响应请求

## 语法

### 注释

- `<!-- HTML注释 -->` 其间语句执行后作为注释发往客户端

```jsp
<!-- 页面加载时间为 <%= (new java.util.Date()).toString() %> -->
```

- `<%-- JSP注释 --%>` 其间语句不执行且不会发往客户端
- `// Java单行注释`
- `/* Java多行注释 */`

### 指令`<%@ page 属性="值" %>`

- `language="java"`
- `import="java.util.*"` 导入多个类时以逗号分隔
- `pageEncoding="GB18030"` 编码方式
- `isErrorPage="true"` 页面异常时是否转向errorPage指定的错误页
- `errorPage="404_err.jsp"` 重定向到一个URL
- `contentType="text/html; charset=UTF-8"` 编码方式
- `isELIgnored="true"` 是否忽略EL表达式，如${param.username}

### 指令`<%@ include file="文件" %>`

- 文件类型：JSP网页、HTML网页、文本文件、Java程序
- 模块化设计、代码复用

### 指令`<%@ taglib uri="tagURI" prefix="tagPrefix" %>`

- 引用标签库

```jsp
<%@ taglib uri="http://java.sun.com/jstl/core" prefix="c" %>
<c:out value="renliang"></c:out>
```

```jsp
<%@ taglib uri="/WEB-INF/struts-logic.tld" prefix="logic" %>
```

### 代码`<%! 声明 %>`

```jsp
<%! int count=0; %>
```

### 代码`<%= 表达式 %>`

```jsp
<%= new java.util.Date() %>
<%= request.getRemoteHost() %>
```

### 动作标签`<jsp:动作 属性="值">`

```jsp
<!-- 作为<jsp:forward>、<jsp:include>的子标签结合使用 -->
<!-- 目标页面request.getParameter("参数名")取值 -->
<jsp:param name="" value="">

<!-- 页面重定向 -->
<jsp:forward page="重定向" />

<!-- 文件包含 -->
<jsp:include page="相对路径的静态或动态文件" flush="true" />

<!-- 创建一个Bean实例 -->
<jsp:UseBean id="" scope="page|request|session|application" class="" type="" />

<!-- 读取属性 -->
<jsp:getProperty name="Bean实例" property="" />

<!-- 设置属性 -->
<jsp:setProperty name="Bean实例" property="" />

<!-- 执行指定插件，浏览器将其转换成<object>或<embed>元素 -->
<jsp:plugin type="bean|applet" code="" ... />
```

## 内置对象（9个）

- request（请求）
- response（响应）
- session（会话）
- application（应用）
- out（输出）
- page（页面）
- pageContext（页面上下文）
- config（配置）
- exception（异常）
