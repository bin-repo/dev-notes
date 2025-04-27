# javascript

## 保留字

```text
    arguments   break      case    catch     class   const       continue  debugger
    default     delete     do      else      enum    eval        export    extends
    false       finally    for     function  if      implements  import    in
    instanceof  interface  let     new       null    package     private   protected
    public      return     static  super     switch  this        throw     true
    try         typeof     var     void      while   with        yield     -
```

## 数据类型

### 基本类型（primitive type）

- 数值（number）整数、浮点、特殊值
- 字符（string）多行文本时在行尾加反斜杠`\`
- 布尔（boolean）真值

```js
var str = "hello";
var i = 10; // 0x0A 0b1010 0o12
var f = 3.14; // 314e-2
var n = NaN;
var m = Infinity;
var b = true;
```

```js
// 123 16 3 NaN
var i = parseInt('123') || parseInt('0x10') || parseInt('3.14') || parseInt('abc')
// 3.14 3.14 NaN
var f = parseFloat('3.14') || parseFloat('314e-2') || parseFloat('abc')
// 非数值
function myIsNaN_1(value) { return typeof value === 'number' && isNaN(value); }
function myIsNaN_2(value) { return value !== value; }
// 有效数值
isFinite(null) === true && isFinite(123) === true
```

### 合成类型（complex type）

- 对象（object）属性名为字符，属性值可任意类型
- 数组（object）元素可任意类型，元素间可不同型
- 函数（function）

```js
// 对象（四种定义方式）
var o = new Object();
o = { name:'张三', age: 16 };
o = {};
o = null;
// 返回属性名数组 ['name', 'age']
Object.keys(o);
// 两种对象属性访问方式等同
typeof o === 'object' && o instanceof Array === false && o.name === '张三' && o['age'] === 16

// 删除属性
delete obj.age
// 对象是否包含某属性、toString为继承属性
'name' in obj && obj.hasOwnProperty('toString')
// 遍历自身属性
for (var key in obj) { if (obj.hasOwnProperty(key)) { obj[key] } }
// 遍历属性
for(var attr in obj) { print(attr + ":" + obj[attr]); }
// 属性名含.符时取属性值
obj["self.ref"].value
```

```js
// 数组（三种定义方式）
var a = new Array('foo', 'bar', 'zoo');
a = ['one', 'two', 'three'];
a = [];
// 返回脚标数组 ['0', '1', '2']，相当于 {0: 'one', 1: 'two', 2: 'three'}
Object.keys(a)       
// length可读可写
typeof a === 'object' && a instanceof Array === true && a.length && a[0] === 'one'
```

```js
// 函数（两种定义方式，前者不常用）
var func = new Function('x', 'y', 'return(x+y)');
func = function(x,y) { return x+y; };
// 函数名称、参数个数
typeof func === 'function' && func.name === 'func' && func.length === 2
```

### 特殊值

- `NaN` 非数字（Not a Number）
- `Infinity` 无穷
- `true` 布尔值（真）
- `false` 布尔值（假）
- `null` 空值（0）
- `undefined` 未定义（NaN）

### 类型判断

- typeof
- instanceof

## 运算符

- 算术运算
  - 加法（`+`）
  - 减法（`-`）
  - 乘法（`*`）
  - 除法（`/`）
  - 指数（`**`）
  - 余数（`%`）
  - 自增（`++`）
  - 自减（`--`）

- 比较运算
  - 大于（`>`）
  - 小于（`<`）
  - 小等（`<=`）
  - 大等（`>=`）
  - 相等（`==`）
  - 严格相等（`===`）
  - 不相等（`!=`）
  - 严格不相等（`!==`）

- 布尔运算
  - 非（`!`）
  - 且（`&&`）
  - 或（`||`）
  - 三元（`?:`）

- 位运算
  - 或（`|`）
  - 与（`&`）
  - 取反（`~`）
  - 异或（`^`）
  - 左移右补0（`<<`）
  - 右移正数左补0负数左补1（`>>`）
  - 右移左补0（`>>>`）

## `this`指针

- 在传统OO语言中类内声明表示对象本身
- 在JavaScript中表示对调用者的引用

### 绑定this的方法

```js
// 独立参数列表
Function.prototype.call()
// 数组参数列表
Function.prototype.apply()
// 当出现多层嵌套时，如函数内再定义函数，this指向容易混淆，须绑定
Function.prototype.bind()
```

```js
var jack = {name:'jack', age:18};
var sun  = {name:'sun',  age:20};
function context() { return this.name; }

context.call(jack, 'p1', 'p2');    // this->jack
context.apply(sun, ['p1', 'p2']);  // this->sun

var counter = {count:0, inc: function() { this.count++; }};
var func = counter.inc.bind(counter);
func();
```

## `new`操作符

- 先创建空对象`{}`
- 然后用函数的`apply`方法将该空对象传入
- 函数内部的`this`将指代该对象

```js
var triangle = new Shape("triangle");
// 等效
var triangle = {};
Shape.apply(triangle, ["triangle"]);
```

## 对象声明三种方式

- `new Object`构造新对象，再动态添加属性

```js
var obj = new Object();
obj.name = "name";
```

- 先构建类原型，再构造对象

```js
function Address(street, xno) {
    this.street = street || 'AA Road';
    this.xno = xno || 40;
}
function Person(name, addr) {
    this.name = name || 'unknown';
    this.addr = addr || new Address(null, null);
}
var person = new Person("zhangsan", null);
```

- `JSON`对象表示法

```js
var person = {
    name: "zhangsan",
    addr: new Address("BB", 23)
};
```

## 引用

- 始终指向最终对象而非引用本身

```js
var obj = {};
var ref = obj;
obj.name="A";
obj=["B"];
ref.name
```

## 原型继承

- 解释器在对象中未查找到某属性时，将在其内部对象`prototype`上继续搜索

```js
xxx.prototype = new yyy();
```

## 严格模式（strict mode）

```js
'use strict';
```

- 老版本引擎会把它当作一行普通字符串加以忽略
- 新版本引擎会进入严格模式
- 可用于函数内部
- 亦可用于整个脚本

## 定时器

```js
// 定时毫秒后执行函数或代码，返回一个整数，表示定时器编号，多余参数将作为将执行的函数参数传入
setTimeout(func|code, delay)
// 每间隔毫秒后执行函数或代码，循环任务
setInterval()
// 取消指定的定时任务
clearTimeout(id)
// 取消指定的循环任务
clearInterval(id)
```

```js
setTimeout(function(){}, 1000);
// 任务不会立即执行，而会延迟到下一轮任务调度
setTimeout(function(){}, 0);
```
