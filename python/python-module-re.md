# python-module-re（regex正则模块）

## 模块导入

```py
import re
```

## 模块方法（`re`）

```py
# 从字符串起始位置匹配一个模式返回一个匹配的对象
re.match(pattern,string,flags=0)
```

```py
# 扫描整个字符串并返回第一个成功的匹配
re.search(pattern,string,flags=0)
```

```py
# 检索和替换（repl为替换的字符串或一个替换函数）
re.sub(pattern,repl,string,count=0)
```

```py
# 匹配所有，并把它们作为一个迭代器返回
re.finditer(pattern,string,flags=0)
```

```py
# 按能够匹配的子串将字符串分割后返回列表
re.split(pattern,string[,maxsplit=0,flags=0])
```

```py
# 编译正则表达式生成一个正则表达式（Pattern）对象
pattern = re.compile(pattern[,flags])
```

## 对象方法（`pattern`）

```py
# 类似 re.match()
pattern.match(string[,pos[,endpos]])
```

```py
# 类似 re.search()
pattern.search(string[,pos[,endpos]])
```

```py
# 匹配所有
pattern.findall(string[,pos[,endpos]])
```

## 正则表达式`flags`修饰符定义

- `re.I` 不区分大小写
- `re.L` 做本地化识别匹配
- `re.M` 多行匹配，影响`^`和`$`
- `re.S` 使`.`匹配包括换行在内的所有字符
- `re.U` 根据Unicode字符集解析字符，影响`\w` `\W` `\b` `\B`
- `re.X` 灵活更易于理解的格式

## 正则表达式特殊模式定义

- `^` 匹配字符串的开头
- `$` 匹配字符串的末尾
- `.` 除换行符外的任意字符，当设置`re.S`后表示任意字符
- `[...]` 匹配一组字符内任意字符，如`[amk]`匹配`a`或`m`或`k`
- `[^...]` 匹配一组字符外任意字符，如`[^amk]`匹配除这三个字母外的任意字符
- `re*` 匹配0个或多个re定义的表达式
- `re+` 匹配1个或多个re定义的表达式
- `re?` 匹配0个或1个re定义的表达式
- `re{n}` 仅匹配n个re定义的表达式
- `re{n,}` 匹配至少n个re定义的表达式
- `re{n,m}` 匹配至少n个、至多m个re定义的表达式
- `a|b` 匹配a或b
- `(re)` 分组匹配
- `(?imx)` 区域匹配，区域内开启`re.I`、`re.M`、`re.X`修饰符
- `(?-imx)` 区域匹配，区域内关闭`re.I`、`re.M`、`re.X`修饰符
- `(?:re)` 类似(...)，但不表示一个组
- `(?imx:re)`
- `(?-imx:re)`
- `(?#...)` 注释匹配
- `(?=re)` 前向肯定界定符
- `(?!re)` 前向否定界定符
- `(?>re)` 匹配的独立模式，省去回溯
- `\w` 匹配数字字母下划线
- `\W` 匹配非数字字母下划线
- `\s` 匹配任意空白字符`\t` `\n` `\r` `\f`
- `\S` 匹配任意非空白字符
- `\d` 匹配任意数字 [0-9]
- `\D` 匹配任意非数字
- `\A` 匹配字符串开始
- `\Z` 匹配字符串结束，若存在换行仅匹配到换行前的结束字符串
- `\z` 匹配字符串结束
- `\G` 匹配最后匹配完成的位置
- `\b` 匹配单词边界，即单词与空格间的位置
- `\B` 匹配非单词边界
- `\n\t等` 匹配换行符、制表符等常规转义符
- `\1..\9` 匹配第n个分组的内容
- `\10` 匹配第n个分组的内容，若无匹配则为八进制字符

## 示例代码

```py
import re

match = re.match('www','www.runoob.com')        # <_sre.SRE_Match object; span=(0, 3), match='www'>
match.group()                                   # 'www'
match.start()                                   # 0 匹配项起始索引
match.end()                                     # 3 匹配项结束索引
match.span()                                    # (0,3) 匹配项索引元组
match = re.match('com','www.runoob.com')        # None

# groups()|group()|start()|end()|span()         # 是_sre.SRE_Match对象的方法

re.search('www','www.runoob.com')               # <_sre.SRE_Match object; span=(0, 3), match='www'>
re.search('com','www.runoob.com')               # <_sre.SRE_Match object; span=(11, 14), match='com'>

re.sub(r'#.*$','','400-888-8888 # tel')         # '400-888-8888 ' 删除注释

[match.span() for match in re.finditer(r'\d+','12a32bc43jf3')]  # [(0, 2), (3, 5), (7, 9), (11, 12)]
[match.group() for match in re.finditer(r'\d+','12a32bc43jf3')] # ['12', '32', '43', '3']

re.split('\W+', 'one, two, three.')             # ['one', 'two', 'three', ''] 不含模式分割符
re.split('(\W+)', 'one, two, three.')           # ['one', ', ', 'two', ', ', 'three', '.', '']

pattern = re.compile(r'\d+')                    # <_sre.SRE_Pattern object; re.compile(r'\d+', re.UNICODE)>
pattern.match('one12twothree34four')            # None
pattern.match('one12twothree34four',3)          # <_sre.SRE_Match object; span=(3, 5), match='12'>
pattern.search('one12twothree34four')           # <_sre.SRE_Match object; span=(3, 5), match='12'>
pattern.findall('one12twothree34four')          # ['12', '34']

pattern = re.compile(r'([a-z]+) ([a-z]+)',re.I) # 忽略大小写
match = pattern.match('Hello World Wide Web')   # <_sre.SRE_Match object; span=(0, 11), match='Hello World'>
[match.groups(),match.group(1),match.group(2)]  # [('Hello', 'World'), 'Hello', 'World']
[match.span(),match.span(1),match.span(2)]      # [(0, 11), (0, 5), (6, 11)]
[match.start(),match.end(),match.start(1),match.end(1),match.start(2),match.end(2)] # [0, 11, 0, 5, 6, 11]
```

```py
import re

[re.match(r'[Pp]ython',s).group() for s in ['Python','python']]    # ['Python', 'python']
re.match(r'[0-9]','0123456789').group()                            # '0'
re.match(r'[a-z]','abcdefghijklmnopqrstuvwxyz').group()            # 'a'
re.match(r'[A-Z]','ABCDEFGHIJKLMNOPQRSTUVWXYZ').group()            # 'A'
re.search(r'[a-zA-Z0-9]','__main__').group()                       # 'm'
re.search(r'[^abc]ook','aook book cook dook').group()              # 'dook'
re.search(r'[^0-9]', '0123456789abcd').group()                     # 'a'
re.match(r'.*','__main\nly__').group()                             # '__main'
[re.match(r'bo*k',s).group() for s in ['bk','bok','book','boook']] # ['bk', 'bok', 'book', 'boook']
[re.match(r'bo+k',s).group() for s in ['bok','book','boook']]      # ['bok', 'book', 'boook']
[re.match(r'bo?k',s).group() for s in ['bk','bok']]                # ['bk', 'bok']
re.match(r'bo{2}k','book').group()                                 # 'book'
[re.match(r'bo{2,}k',s).group() for s in ['book','boook']]         # ['book', 'boook']
[re.match(r'bo{1,3}k',s).group() for s in ['bok','book','boook']]  # ['bok', 'book', 'boook']
re.match(r'\w+','__init__(self):').group()                         # '__init__'
re.search(r'\W+','__init__(self):').group()                        # '('
re.search(r'\s','THIS\r IS\n A\t BOOK\f about python').group()     # '\r'
re.search(r'\S','THIS\r IS\n A\t BOOK\f about python').group()     # 'T'
re.search(r'\d','abc123def456').group()                            # '1'
re.search(r'\D','abc123def456').group()                            # 'a'
re.search(r'er\b', 'never').group()                                # 'er'
re.search(r'er\B', 'verb').group()                                 # 'er'
re.match(r'(\d{4}/\d{1,2}/\d{1,2}) (\d{1,2}:\d{1,2})','2018/7/12 18:21').groups() # ('2018/7/12', '18:21')
```
