# [pandas](https://pandas.pydata.org)

pandas is a fast, powerful, flexible and easy to use open source data analysis and manipulation tool,
built on top of the Python programming language.

## 安装

### use conda

```sh
conda create -c conda-forge -n name_of_my_env python pandas
```

### use pip

```sh
pip install pandas
```

```sh
# 私有环境
python -m venv my-env
source my-env/bin/activate # windows系统下执行 my-env/Scripts/activate
pip install pandas
```

### verifying the installation

```py
import pandas as pd
pd.test()
```

## 数据结构

- `Series` 一维序列`[[index][value]]`
- `DataFrame` 多维表格`[[index][column][column][..]]`

## 用法

### 导入依赖

```py
import numpy as np
import pandas as pd
```

### 创建Series

```py
# 固定索引0-N
series = pd.Series([-2,-1,0,1,2])

# 指定索引别名
series = pd.Series([-2,-1,0,1,2], index=['a','b','c','d','e'])

# 利用Numpy数组生成视图
series = pd.Series(np.array([-2,-1,0,1,2]))

# 利用Series对象生成新视图
series = pd.Series(series)

# 利用字典dict生成新视图
series = pd.Series({'red':200,'blue':100,'yellow':50,'orange':100})

# 从字典中部分抽取或追加NaN元素
series = pd.Series(mydict, index=['red','blue','orange','white'])
```

### Series属性

```py
# 取索引别名列（无别名时返回固定索引）
series.index
# 取值列
series.values
# 是否存在重复项，布尔型
series.index.is_unique
```

### Series处理

```py
# 元素选取
series[2] == series['c']

# 元素切片视图（固定索引与别名不能混用）
series[0:2] == series[[0,1]] == series[['a','b']]

# 布尔型条件抽取
series[series>0]

# 逐个元素算术运算（同Numpy）
series + - * ** / // % m

# 逐个元素应用Numpy基本数学函数
np.log(series)
```

### Series方法

```py
# 返回一个value去重后的数组
series.unique()

# 统计value出现次数（返回Series[[value][count]]）
series.value_counts()

# 检查元素是否np.NaN（返回Series[[index][boolean]]）
series.isnull()

# 检查元素是否np.NaN（返回Series[[index][boolean]]）
series.notnull()

# 检查元素是否属于集合（返回Series[[index][boolean]]）
series.isin([m,n,..])

# 删除单个元素
series.drop('red')

# 删除多个元素
series.drop(['blue','orange'])

# 最小索引
series.idxmin()

# 最大索引
series.idxmax()

# 筛选或追加新元素NaN
series.reindex(['red','yellow'])

# 缺项时按前值填充
series.reindex(range(6), method='ffill')

# 缺项时按后值填充
series.reindex(range(6), method='ffill')
```

### 创建DataFrame

```py
# 字典
dict = {'object':['ball','book','pen'],'color':['blue','white','red'],'price':[1.2,1.7,0.4]}

# 由字典生成对象视图
frame = pd.DataFrame(dict)

# 从字典中抽取或追加元素NaN
frame = pd.DataFrame(dict, columns=['object','price'])

# 指定索引别名
frame = pd.DataFrame(dict, index=['one','two','three'])
```

```py
# 字典
dict = {'red':{2012:22, 2013:33}, 'white':{2011:13, 2012:22, 2013:16}, 'blue':{2011:17, 2013:18}}

# 由嵌套字典生成对象视图
frame = pd.DataFrame(dict)
```

### DataFrame属性

```py
# 行索引别名
frame.index
# 列索引别名
frame.columns
# 元素矩阵
frame.values
# 指定行标签
frame.index.name = 'id'
# 指定列标签
frame.columns.name = 'items'
```

### DataFrame处理

```py
# 取列
frame['price']

# 取行
frame.loc['one']

# 取多行等效于frame.loc[[1,2]]
frame[1:3]

# 按列,行取单个元素
frame['price']['one']

# 转置（行列调换）
frame.T

# 返回False、True布尔矩阵
frame.isin([m,n,..])

# 元素筛选
frame[frame < 5]
frame[frame.isin([..])]
```

### DataFrame元素新增或删除

```py
# 新增列（指定元素相同取值）
frame['size'] = 12

# 新增列（指定元素不同取值）
frame['count'] = [1,2,3]

# 新增列（从序列中选取元素）
frame['status']= pd.Series([0,1,0], index=['one','two','three'])

# 删除单行/多行
frame.drop('one')
frame.drop(['one','two'])

# 删除单列/多列
frame.drop('color',axis=1)
frame.drop(['color','price'],axis=1)

# 删除列
del frame['status']
```

### DataFrame元素基本计算

```py
# 按列行索引别名对齐后运算（add/sub/div/mul），未匹配时NaN填充
frame.add(frame)

# 按列|行对元素执行function（可自定义）操作
frame.apply(function, axis=0|1)

# sum、mean等统计函数
frame.sum() / frame.mean()

# 计算多个统计量（sum、mean等）
frame.describe()
```

### DataFrame的等级索引（与Series类似）

```py
# 指定列标签组、列名
frame.columns.names = ['group', 'column']、
# 指定行标签组、行名
frame.index.names = ['group', 'index']
# 行交换等级
frame.swaplevel('group', 'index')
# 按层级进行排序
frame.sortlevel('group|index')
# 按层级进行统计
frame.sum(level='group|index')
```

### 类型转换

```py
# 将frame转化为等级索引的series（类似于分组）
series = frame.stack()

# 将等级索引的series展开为frame（类似于解除分组）
frame = series.unstack()

# 按组索引选取
series['idx1']

# 按二级索引选取
series[:,'idx2']

# 选取指定元素
series['idx1','idx2']
```

### 处理NaN元素

```py
# 过滤掉NaN元素
series.dropna()

# 过滤掉NaN元素
series[series.notnull()]

# 删除NaN所在的行/列
frame.dropna()

# 行/列全为NaN时删除行/列
frame.dropna(how='all')

# 所有NaN替换统一值
frame.fillna(m)

# 特定列NaN替换特定值
frame.fillna({'price':0,'color':red})
```

### 数据相关性

```py
# 两个序列的相关性
series.corr(series)

# 两个序列的协方差
series.cov(series)

# 单个frame的相关性
frame.corr()

# 单个frame的协方差
frame.cov()

# frame与series的相关性
frame.corrwith(series)

# 两个frame的相关性
frame.corrwith(frame)
```

### 排序

```py
# 升序
series.sort_index()

# 降序
series.sort_index(ascending=False)

# 行序排序
frame.sort_index()

# 列序排序
frame.sort_index(axis=1)

# 元素排序
series.order()

# 按单列元素排序
frame.sort_index(by='price')

# 按多列元素排序
frame.sort_index(by=['price','color'])
```

### 数据文件处理（持久化）

#### 文件格式（csv、excel、hdf、sql、json、html、pickle等）

#### 特殊字符

- `.` 换行符以外的单个字符
- `\d` 数字
- `\D` 非数字
- `\s` 空白字符（空格或制表符）
- `\S` 非空白字符
- `\n` 换行符
- `\t` 制表符
- `\uxxxx` 用十六进制数字xxxx表示的Unicode字符
- `*` 表示0~N次重复
- `+` 表示1~N次重复

```py
# 首行作为列标签
frame = pd.read_csv('file.csv')

# 首行作为元素
frame = pd.read_csv('file.csv',header=None)

# 指定列标签
frame = pd.read_csv('file.csv',names=[,,])

# 指定层级
frame = pd.read_csv('file.csv',index_col=[,,])

# 跳过几行，读取m行
frame = pd.read_csv('file.csv',skiprows=[],nrows=m)

# 每m行一组进行分割
frame = pd.read_csv('file.csv',chunksize=m)

# 指定分隔符的文本
frame = pd.read_table('file.txt',sep='|')

pd.to_csv('file.csv',na_rep='NaN',index=False,header=False)
```

```py
# 解析文件中所有table标签段，返回列表（支持网络文件）
frames = pd.read_html('file.html')
frames = pd.read_html('http://www.xxx.com/file.html') 

# 生成<table>...</table>标签段
s = ['html']
s.append('<head><title>title</title></head>')
s.append('<body>')
s.append(frame.to_html())
s.append('</body></html>')

html = ''.join(s)
html_file = open('file.html', 'w')
html_file.wirte(html)
html_file.close()
```
