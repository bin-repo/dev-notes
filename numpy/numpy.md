# [numpy](https://numpy.org)

NumPy (Numerical Python) is an open source Python library that’s widely used in science and engineering.

## 安装

### use conda

```sh
# 私有环境
conda create -n my-env
conda activate my-env
conda install numpy
```

### use pip

```sh
pip install numpy
```

```sh
# 私有环境
python -m venv my-env
source my-env/bin/activate # windows系统下执行 my-env/Scripts/activate
pip install numpy
```

### verifying the installation

```py
import numpy as np
print(np.__version__)
```

## 用法

### 创建矩阵对象

```py
# [0, 1, 2, 3, 4, 5]
myarray = np.array([0,1,2,3,4,5])
# [0, 1, 2, 3, 4, 5]
myarray = np.array((0,1,2,3,4,5))
# [[0, 1, 2], [3, 4, 5]]
myarray = np.array([(0,1,2),[3,4,5]])
# [['1','First','97'],['2','Second','85'],['3','Third','59']]结构化数组
myarray = np.array([(1,'First',97),(2,'Second',85),(3,'Third',59)])
```

```py
# [[1., 0., 0.],[0., 1., 0.],[0., 0., 1.]] 单位矩阵
myarray = np.eye(3)
# [0., 0., 0.]
myarray = np.zeros(3)
# [[0., 0., 0.],[0., 0., 0.],[0., 0., 0.]]
myarray = np.zeros((3,3))
# [1., 1., 1.]
myarray = np.ones(3)
# [[1., 1., 1.],[1., 1., 1.],[1., 1., 1.]] 参数shape
myarray = np.ones((3,3))
```

```py
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
myarray = np.arange(0,10)
# [2, 5, 8, 11]
myarray = np.arange(2,12,3)
# [0., 0.2, 0.4, 0.6, 0.8, 1., 1.2, 1.4, 1.6, 1.8]
myarray = np.arange(0,2,0.2)
```

```py
# [0., 2.5, 5., 7.5, 10.] N-1等分
myarray = np.linspace(0,10,5)
```

```py
# 0-1间随机数，如[0.78923243, 0.45683003, 0.01209877]
myarray = np.random.random(3)
# 0-1间随机数，如[[0.85732137, 0.59010905], [0.4084541 , 0.20133099]]
myarray = np.random.random((2,2))
```

### 矩阵对象属性

```py
type(myarray)      # numpy.ndarray

myarray.dtype      # 元素类型
myarray.dtype.name #
myarray.ndim       # 维度（轴数）
myarray.size       # 元素个数
myarray.shape      # 型
myarray.itemsize   # 元素占字节数
myarray.nbytes     # 数组总字节数
myarray.flat       # 返回一个扁平化后的数组迭代器（视为一维数组）
myarray.real       # 复数数组的实部
myarray.imag       # 复数数组的虚部

myarray.tolist()   # 转换为Python的列表
```

### 矩阵对象方法

```py
# 一维拆二维（元素须对齐）
myarray.reshape(m,n)

# 拆维后生成新副本
myarray.reshape(m,n).copy()

# 二维合一维
myarray.ravel()

# 同ravel()但生成新副本
myarray.flatten()

# 同reshape()
myarray.shape = (m,n)

# 同ravel()
myarray.shape = (m*n)

# 转置矩阵T
myarray.transpose()
```

### 矩阵方法

```py
# 二维数组垂直连接
np.vstack((myarray,myarray))

# 二维数组水平连接
np.hstack((myarray,myarray))

# 二维数组深度连接（层叠为三维）
np.dstack((myarray,myarray))

# 同vstack()|hstack()
np.concatenatel((myarray,myarray),axis=0|1)

# 一维数组连接（元素按列填充）
np.column_stack((myarray,myarray,myarray))

# 一维数组连接（元素按行填充）
np.row_stack((myarray,myarray,myarray))

# 沿水平方向做垂直平均切分（|）
np.hsplit(myarray,m)

# 沿垂直方向做水平平均切分（—）
np.vsplit(myarray,m)

# 沿深度方向做层切分（/）
np.dsplit(myarray,m)

# 任意切分，[m,n]为指定的列索引(axis=1)或行索引(axis=0)
np.split(myarray,[m,n],axis=0|1)
```

### 遍历处理

```py
np.apply_along_axis(function,axis=0|1,arr=myarray)
```

```py
# 按列计算均值
np.apply_along_axis(np.mean,axis=0,arr=myarray)

# 按行计算均值
np.apply_along_axis(np.mean,axis=1,arr=myarray)
```

### 迭代处理

```py
# 一维迭代元素
for item in myarray: print(item)

# 二维迭代行
for row in myarray: print(row)

# 二维迭代元素
for item in myarray.flat: print(item)
```

### 条件和布尔数组 [True False]

```py
# 逐个元素比较得到布尔数组
myarray > 4

# 以布尔数组作为条件抽取元素
myarray[myarray>4]
```

### 切片处理

```py
# 连续切片（0:len(myarray):1）
myarray[起始索引:结束索引:步长]

# 离散切片
myarray[[索引1,索引2,...]]
```

```py
myarray[2:4]
myarray[::2]
myarray[[2,3]]
myarray[0:2,[0,2]] # 二维
```

### 索引处理

```py
# 正向索引（0:n-1）反向索引（n:-1）
myarray[idx]

# 二维行列
myarray[m,n]
```

```py
myarray[2] = 2
myarray[-1] = 2
myarray[1,2] = 2
```

### 矩阵运算

```py
# 和
myarray.sum()

# 最大值
myarray.max()

# 最小值
myarray.min()

# 幅度范围（max-min）
myarray.ptp()

# 中位数（元素个数为偶时取两个中位数的平均值）
myarray.median()

# 算术平均值
myarray.mean()

# 方差（各元素与算术平均值的离差平方和除以元素个数）
myarray.var()

# 标准差、均方差（方差的平方根）
myarray.std()

# 所有元素乘积
myarray.prod()

# 元素累积乘积
myarray.cumprod()
```

```py
# 加权平均值
np.average(myarray, weights=myarray)

# 相邻两个元素的差值（返回的元素个数少一）
np.diff(myarray)

# 返回满足条件的元素索引数组
np.where(myarray条件)

# 正弦函数
np.sin(myarray)

# 平方根
np.sqrt(myarray)

# 对数函数
np.log(myarray)

# 指数函数
np.exp(myarray)

# 矩阵乘法
np.dot(myarray,myarray)
```

### 矩阵运算符

- `+` 加
- `-` 减
- `*` 乘
- `**` 幂
- `/` 除浮点
- `//` 除整
- `%` 余数

### 矩阵运算机制（?为矩阵运算符）

- `myarray ? m` 逐个元素计算
- `myarray ? myarray` 对应元素计算

### 数据文件处理（数据持久化）

```py
# 从文本文件读取数组
np.genfromtxt(txtfile,delimiter=,names=True)

# 可进一步按列抽取拆分
np.loadtxt(txtfile,delimiter=,usecols=,unpack=True)

# 保存为文本
np.savetxt(txtfile,myarray)

# 二进制文件保存数组（filename.npy）
np.save(filename,myarray)

# 二进制文件读取数组（filename.npy）
myarray = np.load(filename.npy)
```

```py
myarray = np.genfromtxt('myarray.csv',delimiter=',',names=True)
x,y,z = np.loadtxt('myarray.csv',delimiter=',',usecols=(2,3,4))
np.savetxt('myarray.csv',myarray)
np.save('myarray',myarray)
myarray = np.load('myarray.npy')
```
