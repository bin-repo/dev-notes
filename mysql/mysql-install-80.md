# mysql-install-80

Installing MySQL 8.0 on Unix/Linux Using Generic Binaries.

## download

- 官网下载（`mysql-8.0.32-linux-glibc2.12-x86_64.tar.xz`）

### pre-install

- 检查`glibc`版本（应不低于安装包所依赖版本）

```sh
ldd --version
```

- 安装`libaio`库

```sh
yum install -y libaio # apt-get
```

- 用户及组

```sh
groupadd mysql
useradd -r -g mysql -s /bin/false mysql
```

### install

- 解压安装包，包含子目录（bin, docs, man, include, lib, share, support-files）

```sh
tar xvf mysql-8.0.32-linux-glibc2.12-x86_64.tar.xz -C /usr/local 
ln -s /usr/local/mysql-8.0.32-linux-glibc2.12-x86_64 /usr/local/mysql
```

```sh
# 解压的等效命令
xz -dc mysql-8.0.32-linux-glibc2.12-x86_64.tar.xz | tar x -C /usr/local
```

- 查看系统参数及默认值

```sh
bin/mysqld --verbose --help
# 安装目录
bin/mysqld --verbose --help | grep basedir
# 数据目录（schema）会自动创建
bin/mysqld --verbose --help | grep datadir
# 数据目录（import、export）需手动创建
bin/mysqld --verbose --help | grep secure-file-priv
```

- 调整系统参数设置（`/etc/my.cnf`）

```text
[mysqld]
basedir=/usr/local/mysql
datadir=/var/lib/mysql
secure_file_priv=/var/lib/mysql-files
lower_case_table_names=1
#default_authentication_plugin=mysql_native_password
```

- 准备数据目录（根据`secure_file_priv`配置）

```sh
mkdir -p /var/lib/mysql-files
chown mysql:mysql /var/lib/mysql-files
chmod 750 /var/lib/mysql-files
```

- 数据库初始化

```sh
# root random password（建议）
bin/mysqld --initialize --user=mysql
```

```sh
# root no password（不建议）
bin/mysqld --initialize-insecure --user=mysql
```

```sh
# special basedir and datadir（按需）
bin/mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/var/lib/mysql
```

```sh

# special default configure file（按需）
bin/mysqld --defaults-file=/path-to/my.cnf --initialize --user=mysql
```

- 安装公钥证书

```sh
# when default_authentication_plugin=caching_sha2_password
bin/mysql_ssl_rsa_setup
```

- 启动数据库服务

```sh
bin/mysqld_safe --user=mysql &
```

- 注册系统服务

```sh
cp support-files/mysql.server /etc/init.d/mysql.server
systemctl start mysqld
```

### post-install

- 设置环境变量（`/etc/profile`）

```sh
export MYSQL_HOME=/usr/local/mysql
export PATH=$PATH:$MYSQL_HOME/bin
```

- 激活环境变量

```sh
source /etc/profile
```

- 修改`root`口令

```sh
# if mysqld --initialize
sudo grep 'temporary password' /var/log/mysqld.log
mysql -uroot -p
```

```sh
# if mysqld --initialize-insecure
mysql -u root --skip-password
```

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'root-password';
```

- 创建用户

```sql
CREATE USER 'user'@'127.0.0.1' IDENTIFIED BY 'user-password';
CREATE USER 'user'@'localhost' IDENTIFIED BY 'user-password';
CREATE USER 'user'@'%' IDENTIFIED BY 'user-password';
```
