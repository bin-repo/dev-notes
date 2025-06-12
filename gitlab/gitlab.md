# gitlab

## 源安装

### 预安装HTTP和SSH服务

```sh
sudo yum install -y curl policycoreutils-python openssh-server
sudo systemctl enable sshd
sudo systemctl start sshd
sudo firewall-cmd --permanent --add-service=http
sudo systemctl reload firewalld
```

### 预安装POSTFIX邮件服务

```sh
sudo yum install postfix
sudo systemctl enable postfix
sudo systemctl start postfix
```

### 配置REPO源

```sh
cat > /etc/yum.repos.d/gitlab-ce.repo <<EOF
[gitlab-ce]
name=Gitlab CE Repository
baseurl=https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el$releasever/
gpgcheck=0
enabled=1
EOF
```

### 安装GitLab社区版

```sh
sudo yum makecache
sudo yum install gitlab-ce
```

### 配置GitLab

- 修改配置 `/etc/gitlab/gitlab.rb` 指定地址 `external_url 'http://172.16.10.20'`
- 更新配置

```sh
sudo gitlab-ctl reconfigure
```

### 备份和恢复

```sh
# 手动备份
sudo gitlab-rake gitlab:backup:create
```

```sh
# 恢复备份
sudo gitlab-ctl stop unicorn
sudo gitlab-ctl stop sidekiq
sudo gitlab-rake gitlab:backup:restore BACKUP=gitlab.bak
sudo gitlab-ctl reconfigure
```

## 镜像安装

### 拉取镜像

```sh
docker pull gitlab/gitlab-ce
```

### 运行容器

```sh
docker run -d -p 8443:443 -p 8099:80 --name gitlab --restart always \
-v /opt/gitlab/etc:/etc/gitlab \
-v /opt/gitlab/log:/var/log/gitlab \
-v /opt/gitlab/data:/var/opt/gitlab \
gitlab/gitlab-ce
```

### 容器状态

```sh
docker ps -a | grep gitlab
```

## 访问GitLab

- `http://172.16.10.20:8099`
- 按提示修改密码并登录
