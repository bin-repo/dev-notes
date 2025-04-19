# python-function（函数）

## 字符串内建函数

```py
# 字符串长度
len(s)

# 截掉（左、右、左右）空格或指定字符
s.lstrip()
s.rstrip()
s.strip()

# 统计出现次数
s.count(str, beg=0,end=len(s))

# 取字符串中最大、最小字母
cmax,cmin = max(s),min(s)

# 生成字符映射转换表
trans = maketrans(src,des)

# 按转换表转换字符（可指定过滤字符）
s.translate(trans,deletechars='')

# 从左、右侧查找（返回索引或-1）
s.find(str,beg=0,end=len(s))
s.rfind(...)

# 从左、右侧查找（返回索引或异常）
s.index(str,beg=0,end=len(s))
s.rindex(...)

# 替换（max替换次数）
s.replace(old,new[,max])

# 分割（num分割段数）
s.split(str,num)

# 分割行（\r \r\n \n）
s.splitlines(keepends=True|False)

# 将序列中元素（字符串表示）进行连接
s.join(seq)

# 分区（以指定区域为界分为三元组）
s.rpartition(str) # '我爱你'.partition('爱')=('我','爱','你')

# 首字母大写
s.capitalize()

# 每单词首字母大写
s.title()

# 小写、大写、反转大小写
s.lower()
s.upper()
s.swapcase()

# TAB转为空格
s.expandtabs(tabsize=8)

# 右对齐、左填充0
s.zfill(width)

# 居中
s.center(width,fillchar)

# 左对齐|右对齐（可指定填充字符）
s.ljust(width[,fillchar])
s.rjust(...)

# 将字符流编码成字节流
b = s.encode(encoding='utf-8',errors='strict')

# 将字节流解码成字符流
s = b.decode(encoding='utf-8',errors='strict')

# 检测前缀、后缀
s.startswith(prefix,beg=0,end=len(s))
s.endswith(suffix,beg=0,end=len(s))

# 检测字母或数字
s.isalnum()

# 检测至少一个且均为字母
s.isalpha()

# 检测至少一个且均为数字
s.isdigit()
s.isnumeric()
s.isdecimal()

# 检测至少一个且均为空白
s.isspace()

# 检测每单词首字母大写
s.istitle()

# 格式化
'{0:10s},{1:8d}!'.format('hello','world')
```

## 列表内建函数

```py
# 将元组转换为列表
listx = list(seq)

# 列表元素个数、最大元素、最小元素
a, b, c = len(listx), max(listx), min(listx)

# 统计obj出现次数
listx.count(obj)

# 查找
listx.index(obj)

# 排序
listx.sort(cmp=None,key=None,reverse=False)

# 逆序
listx.reverse()

# 复制
listx.copy()

# 列表末尾追加单个值
listx.append(obj)

# 列表末尾追加多个值
listx.extend(seq)

# 插值
listx.insert(index,obj)

# 仅移除第一个匹配项
listx.remove(obj)

# 出栈
listx.pop([index=-1])

# 清空
listx.clear()
```

## 元组内建函数

```py
# 将列表转换为元组
tuplex = tuple(seq)

# 元组元素个数、最大元素、最小元素
a, b, c = len(tuplex), max(tuplex), min(tuplex)
```

## 字典内建函数

```py
# 函数方式构造字典（三种参数形式）
dictx = dict(1='a',2='b')
dicty = dict(zip([1,2],['a','b']))
dictz = dict([(1,'a'),(2,'b')])

# 以seq元素为键生成新字典,可指定默认值否则为None
dictx = dict.fromkeys(seq,default=None)

# 字典元素个数
len(dictx)

# 转化为字符串形式
str(dictx)

# 复制
dicty = dictx.copy()

# 将dicty中的键值更新到dictx里
dictx.update(dicty)

# 键、值列表
dictx.keys()
dictx.values()

# 以列表返回可遍历的（键,值）元组数组
dictx.items()

# 按键取值
dictx.get(key,default=None)

# 按键赋值（不存在则追加该键）
dictx.setdefault(key,default=None)

# 指定键出栈（移除）返回键值
dictx.pop(key[,default])

# 随机键出栈（移除）返回元组(键,值)
dictx.popitem()

# 清空
dictx.clear()
```

## 数据类型转换函数

```py
# 转整型
int(x[,base])

# 字符转整数
ord(x)

# 转浮点
float(x)

# 指定实部和虚部转复数
complex(real[,imag])

# 转布尔
bool()

# 转字符
str(x)

# 整数转字符
chr(x)

# 整数转十六进制字符
hex(x)

# 整数转八进制字符
oct(x)

# 转二进制字符
bin(x)

# 数字转字符
ascii(x)

# 对象转表达式字符
repr(x)

# 表达式字符转对象
eval(str)

# 序列转列表
list(seq)

# 序列转元组
tuple(seq)

# 序列转集合
set(seq)

# 序列转不可变集合
frozenset(s)

# 序列(key,value)元组转字典
dict(d)
```

## 其他内置函数

```py
# 打印属性及方法名
dir()

# 帮助
help(模块|类|方法)

# 打印
print(对象)

# 标准输入
input()

# 打开文件
open()

# 数据切片
slice(start,stop,step)

# 格式化
format()

# 长度、元素个数
len(字符|列表|元组|集合|字典|数组)

# 哈希值
hash(对象)

# 对象标识
id(对象)

# 类型
type(对象)

# 实例
isinstance(对象,类)

# 子类
issubclass(子类,类)

# 迭代器
iter()

# 迭代
next()

# 枚举索引
enumerate()

# 四舍五入
round()

# 范围取值
range()

# 全为真返回True
all()

# 任一为真返回True
any()

# 创建字节
bytes(size)

# 创建字节数组
bytearray(size)

# 创建空对象
object()

# 创建map对象用于迭代
map()

# 创建zip对象用于迭代
zip()

# 创建过滤器对象用于迭代
filter()

# 最大
max()

# 最小
min()

# 求和
sum()

# 平均值
vars()

# 求幂
pow(x,y)

# 求除数及余数
divmod(x,y)

# 绝对值
abs()

# 排序
sorted()

# 逆序
reversed()

# 属性
property()

# 包含属性
hasattr()

# 属性赋值
setattr()

# 属性取值
getattr()

# 删除属性
delattr()

# 本地
locals()

# 全局
globals()

# 父类
super()

compile()
exec()
callable()
staticmethod()
classmethod()
memoryview()
__import__()
```

## 数学函数（`math`）

```py
import math
```

### 数学常量

- 圆周率 `math.pi`
- 自然常数 `math.e`

### 数学函数

- 绝对值

```py
# 返回浮点
math.fabs(-1)=1.0 # 系统内置函数则返回整型 abs(-1)=1
```

- 取整数

```py
# 上取整
math.ceil(4.1) = 5
# 下取整
math.floor(4.9) = 4
```

- 求指数

```py
# e的x次幂
math.exp(x)
# x的y次幂
math.pow(x,y)
```

- 求对数

```py
# 可指明底数（默认10）
math.log(x[,y])
# 以10为底数
math.log10(x)
# 例
math.log(100,10) = math.log(100) = math.log10(100) = 2.0
```

- 求极值

```py
# 最大值
math.max(x,y,..)
# 最小值
math.min(x,y,..)
```

- 平方根

```py
# 平方根（返回浮点）
math.sqrt(4) = 2.0
```

- 浮点分割

```py
# 返回整数部分和小数部分
math.modf(x)
```

- 四舍五入

```py
# 可指定保留小数点后位数
math.round(x[,n])
```

### 三角函数

```py
# 正弦
math.sin(x)

# 余弦
math.cos(x)

# 正切
math.tan(x)

# 反正弦
math.asin(x)

# 反余弦
math.acos(x)

# 反正切
math.atan(x)

# 坐标点(x,y)的反正切
math.atan2(y,x)

# sqrt(x*x+y*y)欧几里德范数
math.hypot(x,y)

# 角度转弧度
math.radians(x)

# 弧度转角度，例：math.degrees(math.pi / 2) = 90.0
math.degrees(x)
```

## 随机数函数（`random`）

```py
import random

# 指定序列中随机抽取一个元素
random.choice(seq)

# 指定线性范围集合中抽取一个元素
random.randrange([start=1,]stop[,step])

# 将序列中的所有元素随机排序
random.shuffle(seq)

# 范围[0,1)内随机生成下一个实数
random.random()

# 范围[x,y]内随机生成下一个实数
random.uniform(x,y)

# 设定随机种子
random.seed([x])
```

## 自定义函数

- 参数均为形参，需要改变外部变量值时须在函数体内以global关键字标识

```py
def 函数名(参数列表):
    'Usage: 函数说明'
    函数体
```

```py
def 函数名(参数列表, *不定长参数元组列表):
    'Usage: 函数说明'
    函数体
```

```py
# 匿名函数定义
lambda 参数列表:函数体
```
