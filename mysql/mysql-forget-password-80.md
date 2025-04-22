# mysql-forget-password-80

MySQL 8.0 resolved when forget `root` password

## 停止服务

```sh
# linux
systemctl stop mysqld

# windows
net stop mysql80
```

## 以不检查密码的方式启动

```sh
mysqld --console --skip-grant-tables --shared-memory
```

## 另开一个终端登录

```sh
mysql -u root
```

## 重设密码

```sh
ALTER USER 'root'@'localhost' IDENTIFIED BY 'root-password';
```

## 刷新权限

```sh
FLUSH PRIVILEGES;
```

## 重启服务

```sh
# linux
systemctl start mysqld

# windows
net start mysql80
```
