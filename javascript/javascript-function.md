# JavaScript 函数

## 函数对象

### 由Function构造（不常用）

- `Function([arg1,[..argN,]] body)` 任意多个参数，紧跟的是函数体

```js
var add = new Function("x", "y", "return(x+y)");
add(2, 4);
```

### 由`function`字面量创建（常用）

```js
function add(x, y) { return x+y; }
// 或
var add = function(x, y) { return x+y; }
```

## 函数参数

- 可以将任意个数的参数传递给函数，而无须顾忌函数声明时个数，未匹配到的参数会被处理为`undefined`
- 函数参数存于类似于数组的内部值`arguments`中
  - `arguments.length` 参数个数
  - `arguments[idx]` 按脚标取参数

## 函数使用

- 赋值给变量

```js
var func = function(x, y) { return x+y; };
```

- 赋值给对象属性

```js
var obj = { id: "obj1", method: func };
```

- 作为参数

```js
function test(str, handler) { handler(str); }
function up(str) { return str.toUpperCase(); }
test("x", up);
```

- 作为函数返回值

```js
function test() { return function() {} }
var func=  test();
var result = test()(); // func()
```

## 词法作用域

```js
for(var i=0; i<arguments.length; i++) {}
print(i); // i 依然有效
```

```js
var str = "xx";
function test() {
    print(str); // undefined
    var str = "local";
    print(str); // "local"
}
```

## `this` 指针

- 指代函数上下文
- 可用`call`和`apply`的第一个参数来替换
  - 函数名.call(调用者, 参数1, ..,参数n)
  - 函数名.apply(调用者, [参数1, ..,参数n])

```js
var jack = {
    name:"jack",
    age:18
};
var sun = {
    name:"sun",
    age:20
};
function context() {
    return this.name;
}
context.call(jack, "p1", "p2");
context.apply(sun, ["p1","p2"]);
```

## 高阶函数

- 以一个或多个函数作为参数的函数

## 匿名函数

- 匿名函数中`arguments.callee`表示函数的调用者，便于函数递归

```js
// 阶乘
(function(x) { return x == 0 ? 1 : x * arguments.callee(x-1); })(10); 
```

## 函数闭包

- 通常情况函数内可以访问函数外的全局变量，而函数外不能访问函数内局部变量
- 通过在函数内定义内部函数，然后return该内部函数，来达到访问内部函数的外层函数的局部变量，即为闭包函数
- 闭包后，被引用的外层函数的局部变量将会常驻内存，需特别注意

### 匿名自执行函数

- 仅执行一次
- 内部变量不污染全局

```js
var data = { table:[], tree:{} };

(function(dm) {
  dm.table.length = 2;
  for(var i=0; i<dm.table.length; i++) {
    dm.table.push(i);
  }
})(data);
```

### 缓存

- 不改变外部引用的值
- 当一个处理过程耗时严重时可采用

```js
var myHash = (function() {
  var cache = {}, count = [];

  return {
    genHash: function(str) {
      if(str in cache) {
        return cache[str];
      }
      var value = hash(str);
      cache[str] = value;
      count.push(str);
      if(count.length > 100) {
        delete cache[count.shift()];
      }
      return value;
    }
  };
})();

myHash.genHash("test");
```

### 实现封装

- 对象属性封装
- 可用于实现类机制
- 实例有独立成员及状态

```js
var person = function() {
  var name = "default";
  return {
    getName: function() { return name; },
    setName: function(newName) { name = newName; }
  }
}();

person.getName();
person.setName("jack");
// 直接访问时结果为 undefined
person.name; 
```

```js
function Person() {
  var name = "default";
  return {
    getName: function() { return name; },
    setName: function(newName) { name = newName; }
  }
}

var john = Person();
john.getName();
john.setName("jack");
```
