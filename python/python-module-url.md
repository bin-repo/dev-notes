# python-module-url（网络资源访问模块）

## 模块导入

```py
import urllib
```

## 模块使用

```py
# 无参GET
with urllib.request.urlopen(r'http://www.runoob.com') as response:
    for line in response:
        line = line.decode('utf-8')
        print(line)
```

```py
# 含参GET
dictx = {'user':'admin', 'pwd':'123456'}
data = urllib.parse.urlencode(dictx)
with urllib.request.urlopen(r'http://www.runoob.com/login'+'?'+data) as response:
    for line in response:
        line = line.decode('utf-8')
        print(line)
```

```py
# POST
dictx = {'user':'admin', 'pwd':'123456'}
data = urllib.parse.urlencode(dictx).encode('ascii')
request = urllib.request.Request(r'http://www.runoob.com/login', data)
request.add_header('Host', '') # 设置相关请求头属性
with urllib.request.urlopen(request) as response:
    for line in response:
        line = line.decode('utf-8')
        print(line)
```
