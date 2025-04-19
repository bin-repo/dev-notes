# python-class（类）

## 面向对象（类Class）

### 类实例

类方法必须有一个额外的第一参数，按照惯例为 `self`，代表类的实例，而不是类

### 类本身

类实例属性 `self.__class__`

### 类私有变量

双下划线开头的变量 `__xxx`

### 类私有方法

双下划线开头的方法 `__xxx()`

## 类的专有方法

- 构造函数 `__init__()`
- 析构函数 `__del__()`
- 打印转换 `__repr__()`
- 按照索引赋值 `__setitem__()`
- 取值 `__getitem__()`
- 获得长度 `__len__()`
- 比较运算 `__cmp__()`
- 函数调用 `__call__()`
- 加 `__add__()`
- 减 `__sub__()`
- 乘 `__mul__()`
- 除 `__div__()`
- 余 `__mod__()`
- 幂 `__pow__()`

## 示例

```py
class Person:
    '''构造函数'''
    def __init__(self, name, sex, income):
        self.name = name or 'hello'
        self.sex = sex or 'male'
        self.__income = income or 10.0 # private

    '''类方法'''
    def script(self):
        print(self.name + ' is ' + self.sex + ' income is {:.2f}'.format(self.__income))
```

```py
p = Person(None,None,None)
p.script()
p.name
# p.__income #不能访问
```

```py
class Male(Person):
    def __init__(self, name, income):
        '''调用父类构造器，注意须传入self参数'''
        Person.__init__(self, name, 'male', income)

    '''方法重载'''
    def script(self):
        print(self.name + ' is ' + self.sex)
```

```py
m = Male('Yang', 12)
m.script()
```

```py
# 调用父类被覆盖的方法
super(Male,m).script()
```
