# CDN

## 概念

- 内容分发网络（Content Distribute Network，CDN）
- 内容交付网络（Content Delivery Network，CDN）
- 互联网数据中心（Internet Data Center，IDC）

## 模型

### 网络运营商（Network Operator）

- 电信、移动、联通等
- 各大网络互联节点数量少，分布不均，网络互通存在瓶颈

### 服务提供商（Service Provider）

- 各类应用服务（文本、图片、视音频等）

### 传统模型

- 客户端发起域名访问服务
- 本地DNS域名解析/DNS服务器域名解析 => 服务所在服务器IP
- 按服务IP访问主机 => 返回内容

客户端与主机可能分布在不同网络运营商网络节点上，存在跨网访问延时

### CDN模型

- 客户端发起域名访问服务
- 本地DNS域名解析/DNS服务器域名解析 => CDN全局/局部负载均衡服务器 => CDN缓存服务器IP
- 访问CDN缓存服务器 => 返回内容

所访问资源已事先缓存在边缘节点服务器内，大大缩短访问延时

## 架构

- 运营管理系统（客户管理、业务管理、计费管理、数据采集）
- 负载均衡系统（域名解析/全局负载均衡、区域负载均衡、本地负载均衡、流量管理）
- 分发服务系统（静态内容加速、动态内容加速、流媒体加速、应用协议加速、日志采集）
- 网络管理系统（设备管理、拓扑管理、链路监控、故障管理）

## 服务（示例）

### [jsdelivr](https://www.jsdelivr.com)

- A free CDN for Open Source
- 提供npm、GitHub、WordPress开源JS分发

```url
https://cdn.jsdelivr.net/npm/package@version/file
https://cdn.jsdelivr.net/gh/user/repo@version/file
https://cdn.jsdelivr.net/wp/plugins/project/tags/version/file
https://cdn.jsdelivr.net/wp/themes/project/version/file
```
