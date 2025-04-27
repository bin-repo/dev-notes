# JavaScript 正则

## 元字符

- `^` 字符开始
- `$` 字符结束
- `*` 0-n次匹配
- `+` 1-n次匹配
- `?` 0-1次匹配
- `\b` 单词边界

## 特殊字符

- `\r` 回车
- `\n` 换行
- `\t` 制表
- `\f` 换页
- `\b` 退格
- `\x#` 十六进制数
- `\cX` 控制字符

## 匹配范围

- `[]` 范围内字符
- `[^]` 范围外字符
- `.` 非\n字符
- `\w` 单字（字母、数字、下划线）
- `\W` 非单字（\w补集）
- `\s` 空白符（空格、制表符）
- `\S` 非空白符（\s补集）
- `\d` 数字
- `\D` 非数字

## 匹配开关

- `i` 忽略大小写
- `g` 全局搜索
- `m` 多行搜索

## 分组匹配

- `()` 分组
- `\组号` 引用

```js
h(elp)?
var pattern = /(['"])[^\1]*\1/;
```

## 重复标记

- `{n}` 重复n次
- `{n,}` 至少重复n次
- `{n,m}` 至少重复n次，至多重复m次

## 对象创建

- RegExp对象
  - `var regex = new RegExp("模式", 匹配开关);`

- 字面量创建
  - `var regex = /模式/[匹配开关];`

## 对象方法

- test 测试是否能匹配到模式
- exec 执行匹配
- compile 编译正则表达式

```js
// 邮箱
var email = /^[\w-]+(\.[\w-]+)*@[\w-]+(\.[\w-]+)+$/;
var b = email.test("john.abruzzi@pl.kunming.china");
```

```js
var xx = /^[a-zA-Z_][a-zA-Z0-9_]*$/;
```

```js
// 纯数字身份证
var xx = /^[\d{15}|\d{18}$/;
```

```js
// 电话号码
var xx = /\d{3,4}-\d{7,8}/;
```

```js
// 手机号码
var xx = /\d{11}/;
```

```js
var pattern = /\w{4}(\d{4})(\w{2})/;
var ret = pattern.exec("yunn0871cg");
print(ret[1]); // 0871
```

```js
var pattern = /^javascript/m;
pattern.test("java\njavascript"); // true
```

## String中应用

- match 模式匹配，返回匹配数组

```js
var str = "it is a test";
// ret = ["it","a"]
var ret = str.match(/it|a/g);
```

- replace 模式替换，返回新串，原串不变

```js
var str = "<span>Welcome, John</span>";
// ret1 = "<div>Welcome, John</div>"
var ret1 = str.replace(/span/g, "div");
// ret2 = "<span>John, Welcome</span>"
var ret2 = str.replace(/(\w+),\s(\w+)/g, "$2,$1");
```

- split 模式分割，返回分割数组

```js
var str = "jon: tomorrow   :remove:file";
// ret = ["john","tomorrow","remove","file"]
var ret = str.split(/\s*:\s*/);
```

- search 模式查询，返回首次出现的位置

```js
var str = "Tomorrow is another day";
// idx = 12
var idx = str.search(/another/);
```
