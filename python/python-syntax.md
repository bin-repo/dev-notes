# python-syntax（语法）

## 脚本文件

- 脚本后缀 `.py`
- 脚本执行 `python3 xxx.py`
- 脚本解释器 `#!/usr/bin/python3`
- 脚本编码定义 `-*- coding: utf-8 -*-`

## `__name__`属性

```py
if __name__ == '__main__':
    print('程序自身在运行')
else:
    print('程序被另一模块import而运行')
```

## 保留字

- 可通过`keyword`模块查看保留字列表

```py
import keyword
print(keyword.kwlist)
```

## 注释符

- 单行注释（`# 单行注释`）
- 多行注释（`'''多行注释'''` 或 `"""多行注释"""`）

## 代码块

- 以行缩进区分代码块结构

## 灵活赋值

- 无需指明数据类型，python自动识别

```py
a = 1
a = b = 1
a,b = 1,'2'
```

## 运算符

- 算术运算符 `+`加 `-`减 `*`乘 `/`浮点除 `//`整除 `%`余 `**`幂
- 比较运算符 `==` `!=` `>` `<` `>=` `<=`
- 按位运算符 `&`与 `|`或 `^`异或 `~`非 `<<`左移 `>>`右移
- 逻辑运算符 `and`且 `or`或 `not`非
- 成员运算符 `in`属于 `not in`不属于
- 身份运算符 `is`是 `is not`不是

## 六种标准数据类型

- 其中string、list、tuple属于sequence序列

### Number（数字，值不可变）

- 整型 `int=1` `int=0b10101` `int=0o777` `int=0xa2`
- 浮点 `float=3.14` `float=314e-2`
- 复数 `complex=3+4j` `complex=complex(3,4)`
- 真值 `bool=True|False` `is_busy,has_value=True,False`

### String（字符，值不可变）

- 普通字符 `'str1'` `"str2"` `'''str3'''` `"""str4"""`
- 转义字符 `'\o12'`八进制 `'\xab'`十六进制 `'\000'`空；等

### List（列表，值可变）

- 数组 `[]` `[1,2,3]` `[[1,2,3],[4,5,6]]`

### Tuple（元组，值不可变）

- 元组 `()` `(1,)` `(1,2,3)` `1,2,3`

### Set（集合，值不可变，无序、自动去重复）

- 集合 `set()` `{1,2,3}`

### Dict（字典，值可变）

- 字典 `{}` `{1:'a',2:'b'}`

## 数据类型识别

- 认为子类是一种父类类型 `isinstance(a,A)`
- 认为子类和父类不是一种类型 `type(a)==A`

## 数据运算与操作

### Number数值运算

- 算术运算 `+` `-` `*` `/` `//` `%` `**`

### String字符串操作

- 切片 `str[start:end]`（左0起，右-1起）
- 连接 `str1 + str2`
- 重复 `str3 * 2`
- 关闭`\`转义 `r'read\nbook'`

### List列表操作

- 切片 `list[start:end]`（左0起，右-1起）
- 连接 `list1 + list2`
- 重复 `list3 * 2`

### Tuple元组操作

- 切片 `tuple[start:end]`（左0起，右-1起）
- 连接 `tuple1 + tuple2`
- 重复 `tuple3 * 2`

### Set集合操作

- 差集 `-`
- 并集 `|`
- 交集 `&`
- 非交集 `^`
- 元素测试 `element in set`

### Dict字典操作

- 所有键 `dict.keys()`
- 所有值 `dict.values()`

## 条件与循环语句

### 模式

- `if : elif : else :`
- `while : else :`
- `for : else :`

### 控制

- 继续 `continue`
- 中断 `break`
- 终止 `pass`（等待键盘中断信号Ctrl+C）

## 内置函数生成整数数列 `range([start,]end[,step])`

```py
for i in range(5)
for i in range(5,9)
for i in range(0,10,3)
```

## 迭代器函数 `iter()` `next()`

```py
it = iter([1,2,3,4])
next(it)
for i in it : next(i)
```

## 生成器函数 `yield()`

- 生成可供迭代的节点

## 列表作为堆栈/队列的用法

### 堆栈

```py
list.append()
list.pop()
```

### 队列

```py
from collections import deque
queue = deque(list)
queue.append()
queue.popleft()
```

## 遍历技巧

### 遍历字典

```py
for k,v in dict.items():
    print(k,v)
```

### 遍历序列

```py
for i,v in enumerate(list):
    print(i,v)
```

### 遍历多个序列

```py
for ex,ey in zip(listx,listy):
    print(ex,ey)
```

## 读取键盘输入

```py
str = input('请输入：')
```

## 读写文件

```py
# 默认文本只读，二进制数据读写须附加b字符
f = open(filename, mode='r')
f.write(s)
f.read([size])
f.readline([size])
f.readlines([size])
f.close()
```

![文件模式](./img/open-file-mode.png '文件模式')

## 序列化和反序列化（`pickle`模块）

```py
import pickle

# 序列化，open(filename, mode='wb')
pickle.dump(obj, file [,protocol])

# 反序列化，open(filename, mode='rb')
obj = pickle.load(file)
```

## 异常处理

- 抛出异常 `raise ex`
- 捕获异常 `try: XX; except ex: YY; else: ZZ`

## `with`语句

- 可以保证诸如文件之类的对象在使用完之后一定会正确的执行它的清理方法

```py
# 代码执行完毕后，即使处理过程出现问题，文件总是会关闭
with open('tt.txt') as tt:
```

## 网络编程

- `HTTP` `port=80` [`httplib`, `urllib`, `xmlrpclib`] 网页
- `NNTP` `port=119` [`nntplib`] 阅读和张贴新闻文章“帖子”
- `FTP` `port=20` [`ftplib`, `urllib`] 文件传输
- `SMTP` `port=25` [`smtplib`] 发送邮件
- `POP3` `port=110` [`poplib`] 接收邮件
- `IMAP4` `port=143` [`imaplib`] 获取邮件
- `TELNET` `port=23` [`telnetlib`] 命令行
- `GOPHER` `port=70` [`gopherlib`, `urllib`] 信息查找

## 使用技巧

### for语句

```py
knights = {'gallahad': 'the pure', 'robin': 'the brave'}
for k, v in knights.items():
    print(k, v)
```

```py
# i=0,1,2
for i, v in enumerate(['tic', 'tac', 'toe']):
    print(i, v)
```

```py
questions = ['name', 'quest', 'favorite color']
answers = ['lancelot', 'the holy grail', 'blue']
for q, a in zip(questions, answers):
    print('{0}={1}'.format(q, a))
```

```py
# 9 7 5 3 1
for i in reversed(range(1, 10, 2)):
    print(i, end=' ')
```

```py
# 去重后排序 apple banana orange pear
basket = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']
for f in sorted(set(basket)):
    print(f, end=' ')
```

```py
# {2: 4, 4: 16, 6: 36}
{x:x**2 for x in (2, 4, 6)}
```

```py
# {'d', 'r'}
{x for x in 'abracadabra' if x not in 'abc'}
```
