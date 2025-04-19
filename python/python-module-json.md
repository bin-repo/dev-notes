# python-module-json（JSON数据处理模块）

## 模块导入

```py
import json
```

## 模块使用

```py
# 字典类型转成JSON格式字符串（键/值可能非字符型）
json.dumps(dict)
```

```py
# JSON格式字符串转字典类型（键/值均为字符型）
json.loads(json_str)
```

```py
# 字典类型转成JSON格式数据并写入文件
json.dump(dict,file)
```

```py
# 从文件读取JSON格式数据并转换为字典类型
json.load(file)
```

## 示例代码

```py
# repr(dictx) = "{1: 'one', 2: 'two', 3: 'three'}"
dictx = {1:'one',2:'two',3:'three'}
```

```py
# '{"1": "one", "2": "two", "3": "three"}'
json_str = json.dumps(dictx)
```

```py
# repr(dicty) = "{'1': 'one', '2': 'two', '3': 'three'}"
dicty = json.loads(json_str)
```

```py
with open('data.json', 'w') as f:
    json.dump(dictx, f)
```

```py
with open('data.json', 'r') as f:
    dicty = json.load(f)
```
