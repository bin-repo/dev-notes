# python-module-mysql（mysql数据库模块）

## 模块导入

```py
import pymysql
```

## 模块使用

```py
# 建立连接
db = pymysql.connect('localhost','user','pwd','sid')
```

```py
# 获取游标
cursor = db.cursor()
```

```py
# 删表
cursor.execute('''drop table if exists employee''')
```

```py
# 建表
cursor.execute('''
create table employee (
    first_name char(20) not null,
    last_name char(20),
    age int,
    sex char(1)
    income float)''')
```

```py
# 查询 fetchone()
cursor.execute('select version()')
'db version:{}'.format(cursor.fetchone())
```

```py
# 查询 fetchall()
cursor.execute('''select * from employee where income > 1000''')
if cursor.rowcount > 0:
    [row[0]+row[1]+str(row[2])+row[3]+str(row[4]) for row in cursor.fetchall()]
```

```py
# 新增
try:
    cursor.execute('''
    insert into employee(first_name,last_name,age,sex,income)
    values ('Mac','Mohan',20,'M',2000)''')
    db.commit()
except:
    db.rollback()
```

```py
# 更新
try:
    cursor.execute('''update employee set age=age+1 where sex='M' ''')
    db.commit()
except:
    db.rollback()
```

```py
# 删除
try:
    cursor.execute('''delete from employee where sex='M' ''')
    db.commit()
except:
    db.rollback()
```

```py
# 关闭连接
db.close()
```
