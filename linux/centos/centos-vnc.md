# CentOS桌面环境

## 系统最小化安装（Minimal Install）

## 安装桌面系统（GNOME Desktop）

```sh
# 系统提供的环境组
yum group list

# 安装桌面环境
yum group install "GNOME Desktop"

# 安装列表
rpm -qa | grep gnome
```

## 启动模式

```sh
systemctl get-default

# 图形化
systemctl set-default graphical.target

# 命令行
systemctl set-default multi-user.target
```

## 切换模式

```sh
# 命令行
init 3

# 图形化
init 5

# 图形化
startx
```

## 远程桌面

```sh
# epel源
yum list epel*
yum install epel-release

# 远程桌面协议（由epel源提供）
yum install xrdp

# VNC服务
yum install tigervnc tigervnc-server

# 系统服务
systemctl enable xrdp
systemctl start xrdp

# 防火墙（开放远程桌面端口）
firewall-cmd --permanent --zone=public --add-port=3389/tcp
firewall-cmd --reload
```

## 桌面环境设置

### 命令行设置（gsetting）

```sh
# 查询
gsettings list-schemas | grep org.gnome.desktop.wm

# 查询配置项（schema）
gsettings list-keys org.gnome.desktop.wm.preferences

# 查看（schema key）
gsettings get org.gnome.desktop.wm.preferences theme

# 设置（schema key value）
gsettings set org.gnome.desktop.wm.preferences theme 'Adwaita'
```

### 图形化设置（dconf）

```sh
# 安装并启动dconf
yum install dconf-editor
dconf-editor
```

### 恢复默认设置

```sh
# 清理用户设置
rm -rf ~/.config/dconf/user

# 重新创建（编译失败时会导致桌面异常，如黑屏、无最大最小化关闭按钮等）
/usr/bin/glib-compile-schemas /usr/share/glib-2.0/schemas
```

## 启动相关窗口

```sh
# 打开设置窗口
gnome-control-center

# 打开应用安装窗口
gpk-application
```
