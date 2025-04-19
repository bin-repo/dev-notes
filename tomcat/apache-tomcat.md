# apache-tomcat

## 版本系列

- apache-tomcat-7.0.100 ( JDK6、JDK7 )
- apache-tomcat-8.5.51 ( JDK7 )
- apache-tomcat-9.0.31 ( JDK8 )

## 解压安装

```sh
# 解压
tar xzvf apache-tomcat-x.x.x.tar.gz -C /usr/local
ln -s /usr/local/apache-tomcat-x.x.x /usr/local/tomcat

# 环境变量（/etc/profile）
export TOMCAT_HOME=/usr/local/tomcat
export PATH=$PATH:$TOMCAT_HOME/bin

# 环境更新
source /etc/profile
```

## 配置

### 全局配置

- $TOMCAT_HOME/bin/{catalina.bat,catalina.sh}

### 个性化配置

- $TOMCAT_HOME/bin/{setenv.bat,setenv.sh}

```bat
set JAVA_HOME=D:\java\jdk-x.x.x
set CATALINA_HOME=D:\tomcat\apache-tomcat-x.x.x
set "JAVA_OPTS=-server -Xms256m -Xmx256m
```

```sh
#!/bin/sh
# 使用的jdk目录
export JAVA_HOME=/usr/local/jdk-x.x.x
# 使用的Tomcat目录
export CATALINA_HOME=/usr/local/tomcat-x.x.x
# JAVA_OPTS参数需要CATALINA_PID参数
export CATALINA_PID="$CATALINA_HOME/tomcat.pid"
# Tomcat的JVM参数设置
export JAVA_OPTS="-server -Xms256m -Xmx256m"
```

## 启动

- $TOMCAT_HOME/bin/{startup.bat,startup.sh}

## 停止

- $TOMCAT_HOME/bin/{shutdown.bat,shutdown.sh}
