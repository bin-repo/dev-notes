# JavaScript 标准库

## Object

```js
// 返回属性数组
Object.keys()
// 返回属性数组（包含不可枚举属性，如length）
Object.getOwnPropertyNames()
// 获取某个属性的描述对象
Object.getOwnPropertyDescriptor()
// 通过描述对象，定义某个属性
Object.defineProperty()
// 通过描述对象，定义多个属性
Object.defineProperties()
// 防止对象扩展
Object.preventExtensions()
// 判断对象是否可扩展
Object.isExtensible()
// 禁止对象配置
Object.seal()
// 判断一个对象是否可配置
Object.isSealed()
// 冻结一个对象
Object.freeze()
// 判断一个对象是否被冻结
Object.isFrozen()
// 该方法可以指定原型对象和属性，返回一个新的对象
Object.create()
// 获取对象的Prototype对象
Object.getPrototypeOf()
// 返回当前对象对应的值
Object.prototype.valueOf()
// 返回当前对象对应的字符串形式
Object.prototype.toString()
// 返回当前对象对应的本地字符串形式
Object.prototype.toLocaleString()
// 判断某个属性是否为当前对象自身的属性，还是继承自原型对象的属性
Object.prototype.hasOwnProperty()
// 判断当前对象是否为另一个对象的原型
Object.prototype.isPrototypeOf()
// 判断某个属性是否可枚举
Object.prototype.propertyIsEnumerable()
```

## Array

```js
// 判断数组
Array.isArray()
// 
Array.prototype.valueOf()
// 
Array.prototype.toString()
// 尾压入
Array.prototype.push()
// 尾移出
Array.prototype.pop()
// 首移出
Array.prototype.shift()
// 首压入
Array.prototype.unshift()
// 将元素连接成字符串，未指定连接符时默认逗号
Array.prototype.join()
// 将两个或多个数组合并
Array.prototype.concat()
// 反向排序
Array.prototype.reverse()
// 抽取元素生成新数组
Array.prototype.slice(start, end)
// 删除指定序号开始的指定个数元素，同时可以添加新元素
Array.prototype.splice(start, count, item1, ..., itemN)
// 正向排序
Array.prototype.sort()
// 遍历每个元素执行操作后返回新元素生成新数组
Array.prototype.map(function(e,i,a){return e;})
// 遍历每个元素执行操作无返回
Array.prototype.forEach(function(e,i,a){...}, [])
// 遍历每个元素执行操作，满足条件的元素生成新数组
Array.prototype.filter(function(e,i,a){return e;}, [])
// 有元素满足条件返回true
Array.prototype.some(function(e,i,a){return true;})
// 所有元素满足条件返回true
Array.prototype.every(function(e,i,a){return true;})
// 顺序对每个元素处理，处理结果作为下一元素初始值
Array.prototype.reduce(function(r,e){return r+e;}, iv)
// 从最后一个元素开始，r为累加值，e为当前元素，iv为初始值
Array.prototype.reduceRight(function(r,e){return r+e;}, iv)
// 第一次出现，未匹配返回-1
Array.prototype.indexOf()
// 最后一次出现
Array.prototype.lastIndexOf()
```

## Number

```js
// 正的无限，指向Infinity
Number.POSITIVE_INFINITY
// 负的无限，指向-Infinity
Number.NEGATIVE_INFINITY
// 非数值，指向NaN
Number.NaN
// 表示最小的正数（即最接近0的正数，在64位浮点数体系中为5e-324），最接近0的负数为-Number.MIN_VALUE
Number.MIN_VALUE
// 表示能够精确表示的最大整数，即9007199254740991
Number.MAX_SAFE_INTEGER
// 表示能够精确表示的最小整数，即-9007199254740991
Number.MIN_SAFE_INTEGER
//
Number.prototype.toString()
// 先将数转为指定位数的小数，然后返回这个小数字符串
Number.prototype.toFixed()
// 转为科学计数法后的字符串
Number.prototype.toExponential()
// 转为指定位数的有效数字字符串
Number.prototype.toPrecision()
// 转本地化
Number.prototype.toLocaleString()
```

## String

```js
// 由多个单字符组成字符串
String.fromCharCode()
// 字符串长度
String.prototype.length
// 按序号取字符
String.prototype.charAt()
// 按序号取字符的编码（10进制数）
String.prototype.charCodeAt()
// 将两个字符串连接成一个新字符串
String.prototype.concat()
// 抽取
String.prototype.slice(start, end)
// 子串
String.prototype.substring(start, end)
// 子串
String.prototype.substr(start, count)
// 检索
String.prototype.indexOf()
// 右检索
String.prototype.lastIndexOf()
// 去除两端空白符
String.prototype.trim()
// 转小写
String.prototype.toLowerCase()
// 转大写
String.prototype.toUpperCase()
// 匹配，返回数组
String.prototype.match()
// 匹配，返回索引或-1
String.prototype.search()
// 替换，s替换为r
String.prototype.replace(s, r)
// 分割，返回数组
String.prototype.split()
// 字符串大小比较
String.prototype.localeCompare()
```

## Math

```js
// 常数e
Math.E
// 2 的自然对数
Math.LN2
// 10 的自然对数
Math.LN10
// 以 2 为底的e的对数
Math.LOG2E
// 以 10 为底的e的对数
Math.LOG10E
// 常数π
Math.PI
// 0.5 的平方根
Math.SQRT1_2
// 2 的平方根
Math.SQRT2

// 绝对值
Math.abs()
// 向上取整
Math.ceil()
// 向下取整
Math.floor()
// 最大值
Math.max()
// 最小值
Math.min()
// 幂运算
Math.pow()
// 平方根
Math.sqrt()
// 自然对数
Math.log()
// e的指数
Math.exp()
// 四舍五入
Math.round()
// 随机数
Math.random()
// 返回参数的正弦（参数为弧度值）
Math.sin()
// 返回参数的余弦（参数为弧度值）
Math.cos()
// 返回参数的正切（参数为弧度值）
Math.tan()
// 返回参数的反正弦（返回值为弧度值）
Math.asin()
// 返回参数的反余弦（返回值为弧度值）
Math.acos()
// 返回参数的反正切（返回值为弧度值）
Math.atan()
```

## RegExp

```js
// 正则匹配，返回布尔值
RegExp.prototype.test()
// 正则匹配，返回数组
RegExp.prototype.exec()
```

## JSON

```js
// 将对象转为JSON字符串
JSON.stringify()
// 由JSON字符串还原为对象
JSON.parse()
```

## 示例

```js
var obj = { name: '张三', age: 16 };
var arr = ['foo', 'bar', 'zoo'];

Object.keys(obj);
Object.keys(arr);

Array.isArray(obj);
Array.isArray(arr);

// 堆栈
arr.push('mmm');
arr.pop();

// 队列
arr.push('mmm');
arr.shift();

arr.join('|');
arr.concat(['mmm']);

arr = [1, 2, 3].map(function(e,i,a) { return e*e; });

// this->arr
[1, 2, 3].forEach(function(e,i,a) { this.push(e*e); }, arr);

[1, 2, 3, 4, 5].filter(function(e,i,a){return i % 2 === 0;});

// this->{MAX: 3}
[1, 2, 3, 4, 5].filter(function(e,i,a){if (e > this.MAX) return true;}, {MAX: 3});

// true
[1, 2, 3, 4, 5].some(function(e,i,a){return e >= 3;});
// false
[1, 2, 3, 4, 5].every(function(e,i,a){return e >= 3;});

// '10.00'
(10).toFixed(2)

var regex = new RegExp('xyz', 'i');
// 等效于
var regex = /xyz/i;

// true
regex.test('abcxyzdef');
// ['xyz']
regex.exec('abcxyzdef');

var obj = JSON.parse('{"name":"张三", "age": "16"}');
var str = JSON.stringify(obj);
```
