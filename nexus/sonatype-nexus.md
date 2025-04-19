# sonatype-nexus

## 下载

```sh
# window
wget http://download.sonatype.com/nexus/3/nexus-3.21.1-01-win64.zip
# linux
wget http://download.sonatype.com/nexus/3/nexus-3.21.1-01-unix.tar.gz
# macos
wget http://download.sonatype.com/nexus/3/nexus-3.21.1-01-mac.tgz
```

## 安装

```sh
# linux
tar -xzvf nexus-3.21.1-01-unix.tar.gz -C /usr/local
ln -s /usr/local/nexus-3.21.1-01-unix /usr/local/nexus
```

## 环境变量

```sh
# /etc/profile
export NEXUS_HOME=/usr/local/nexus
export PATH=$PATH:$NEXUS_HOME/bin
```

```sh
source /etc/profile
```

## 主要配置

### JAVA版本配置

- 使用全局版本（`JAVA_HOME`环境变量设定的默认版本）
- 使用特定版本（`$NEXUS_HOME/bin/nexus`脚本中`INSTALL4J_JAVA_HOME_OVERRIDE`设定）

### JVM虚拟机配置

- JVM参数（`$NEXUS_HOME/bin/nexus.vmoptions`）

### NEXUS配置

- 系统参数（`$NEXUS_HOME/etc/nexus-default.properties`）
- 默认端口（8081）
- 默认用户（admin/admin123）

## 运行

- 在前台运行

```sh
bin/nexus run # bin/nexus.exe /run
```

- 在后台运行

```sh
/bin/nexus start        # /bin/nexus.exe /start
/bin/nexus stop         # /bin/nexus.exe /stop
/bin/nexus restart      # /bin/nexus.exe /restart
/bin/nexus force-reload # /bin/nexus.exe /force-reload
/bin/nexus status       # /bin/nexus.exe /status
```

- 检查运行是否正常（`http://localhost:8081/`）

## 用户管理

![用户管理界面](./img/nexus-user.png '用户列表')

![用户管理界面](./img/nexus-user-add.png '用户新增')

## 仓库管理

![仓库管理界面](./img/nexus-repo.png '仓库列表')

### 仓库类型（proxy）——用于拉取远程仓库

![仓库管理界面](./img/nexus-repo-proxy.png 'proxy')

- 可代理Maven中央仓库（`https://repo1.maven.org/maven2/`）
- 可代理Aliyun仓库（`http://maven.aliyun.com/nexus/content/groups/public`）
- 等

### 仓库类型（host）——用于私有仓库（发行版、快照版）

![仓库管理界面](./img/nexus-repo-host-release.png 'host-release')

![仓库管理界面](./img/nexus-repo-host-snapshot.png 'host-snapshot')

### 仓库类型（group）——用于仓库分组

![仓库管理界面](./img/nexus-repo-group.png 'group')
