# python-module-socket（套接字模块）

## 模块导入

```py
import socket
```

## 模块使用

```py
# 创建套接字，类型（TCP:SOCK_STREAM | UDP:SOCK_DGRAM）
s = socket.socket([family[,type[,proto]]])
```

```py
# 地址绑定
s.bind((host,port))
```

```py
# 开始TCP监听
s.listen(backlog)
```

```py
# 接受TCP连接
s.accept()
```

```py
# 向服务端发起TCP连接，出错时抛异常
s.connect((host,port))
```

```py
# 向服务端发起TCP连接（扩展版），出错时返回错误码
s.connect_ex((host,port))
```

```py
# 接收TCP数据
s.recv(size)
```

```py
# 发送TCP数据
s.send()
```

```py
# 发送TCP数据（成功返回None，失败异常）
s.sendall()
```

```py
# 接收UDP数据，返回(data,address)
s.recvfrom()
```

```py
# 发送UDP数据
s.sendto((ipaddr,port))
```

```py
# 关闭套接字
s.close()
```

```py
# 远程地址，返回(ipaddr,port)
s.getpeername()
```

```py
# 本地地址，返回(ipaddr,port)
s.getsockname()
```

```py
# 设置套接字选项的值
s.setsockopt(level,optname,value)
```

```py
# 获取套接字选项的值
s.getsockopt(level,optname[,buflen])
```

```py
# 设置超时时间（秒）
s.settimeout(timeout)
```

```py
# 获取超时时间（秒）
s.gettimeout()
```

```py
# 返回套接字文件描述符
s.fileno()
```

```py
# 设置阻塞模式（0非阻塞，否则阻塞）
s.setblocking(flag)
```

```py
# 创建一个与该套接字相关连的文件
s.makefile()
```

## 服务端示例

```py
# 服务端示例
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.bind((socket.gethostname(), 9999))
s.listen(5)
while True:
    client,addr = s.accept()
    client.send('hello'.encode('utf-8'))
    client.close()
else:
    s.close()
```

## 客户端示例

```py
# 客户端示例
c = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
c.connect((socket.gethostname(), 9999))
msg = c.recv(1024).decode('utf-8')
c.close()
```
