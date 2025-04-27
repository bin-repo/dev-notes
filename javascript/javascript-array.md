# JavaScript 数组

## 特点

- 同一数组中可含有不同类型的元素
- 数组属性`length`非只读，可通过改变该值自由缩放数组尺寸

## 创建

- 关键字new创建（空数组、指定长度、指定元素）
- 字面量创建（空数组、指定元素）

```js
var array = new Array();
var array = new Array(10);
var array = new Array("one", "two");
var array = [];
var array = ["one", "two", "three"];
```

## 脚标

- 数字脚标（元素）
- 字符脚标（属性）

```js
array[0] = 10;
array["pi"] = 3.1415926;
```

## 遍历

```js
// 遍历所有元素、属性
for(var xx in array) { print(array[xx]); }

// 遍历所有元素
for(var i=0; i<array.length; i++) { print(array[i]); }
array.forEach(function(element, index, array) {})
```

## 数组方法

- `concat` 与其它N个数组进行连接，相当于append追加

```js
var array1 = ["one"];
var array2 = ["two"];
var array3 = ["three"];
// ["one","two","three"]
array1.concat(array2, array3);
```

- `join` 数组元素按指定连接符进行连接，返回字符串

```js
// one|two|three
var str = array1.join("|");
```

- `push` 数组末尾添加一个或多个元素，返回新数组长度

```js
// len = 4 array1 = ["one","two","three","four"]
var len = array1.push("four");
```

- `pop` 删除并返回数组最后一个元素

```js
// last = "four" array1 = ["one","two","three"]
var last = array1.pop();
```

- `shift` 删除并返回数组第一个元素

```js
// first = "one" array1 = ["two","three"]
var first = array1.shift();
```

- `unshift` 数组开头添加一个或多个元素，返回新数组长度

```js
// len = 3 array1 = ["one","two","three"]
var len = array1.unshift("one");
```

- `slice` 数组切片，返回新数组（不是原数组的视图，而是新副本）
  - 参数 `[start,end)`

```js
// array4 = ["two", "three"]
var array4 = array1.slice(1,3); // 不包含脚标3的元素
```

- `splice` 删除元素，同时插入新元素，相当于replace替换
  - `array.splice(index,howmany,item1,.....,itemX)`

```js
// array4 = ["aa","bb","three"]
array4.splice(0,1,"aa","bb");
```

- `reverse` 数组中的元素反序（逆序）

```js
// array4 = ["three", "bb", "aa"]
array4.reverse(); 
```

- `sort` 数组中的元素进行排序（默认字母升序）
  - 对数值排序时须指定排序方法

```js
array.sort();
// 正序
array.sort(function(a,b) { return a-b; });
// 逆序
array.sort(function(a,b) { return b-a; });
```

- `valueOf` 返回数值对象的原始值（类似toString）

```js
array.valueOf();
```
