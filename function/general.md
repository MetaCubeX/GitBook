---
cover: ../.gitbook/assets/bannera.jpg
coverY: 0
---

# 基础配置

#### **监听设置**：

```yaml
#此处省略部分设置#

# port: 7890 # HTTP(S) 代理服务器端口
# socks-port: 7891 # SOCKS5 代理端口
mixed-port: 10801 # HTTP(S) 和 SOCKS 代理混合端口
# redir-port: 7892 # 透明代理端口，用于 Linux 和 MacOS

# Transparent proxy server port for Linux (TProxy TCP and TProxy UDP)
# tproxy-port: 7893

allow-lan: true # 允许局域网连接
bind-address: "*" # 绑定 IP 地址，仅作用于 allow-lan 为 true，'*'表示所有地址
mode: rule

log-level: debug # 日志等级 silent/error/warning/info/debug

ipv6: true # 开启 IPv6 总开关，关闭阻断所有 IPv6 链接和屏蔽 DNS 请求 AAAA 记录

tls:
  certificate: string # 证书 PEM 格式，或者 证书的路径
  private-key: string # 证书对应的私钥 PEM 格式，或者私钥路径

external-controller: 0.0.0.0:9093 # RESTful API 监听地址
external-controller-tls: 0.0.0.0:9443 # RESTful API HTTPS 监听地址，需要配置 tls 部分配置文件
# secret: "123456" # `Authorization:Bearer ${secret}`

external-ui: /path/to/ui/folder # 配置 WEB UI 目录，使用 http://{{external-controller}}/ui 访问

# interface-name: en0 # 设置出口网卡

# routing-mark:6666 # 配置 fwmark 仅用于 Linux

# 类似于 /etc/hosts, 仅支持配置单个 IP
hosts:
# '*.clash.dev': 127.0.0.1
# '.dev': 127.0.0.1
# 'alpha.clash.dev': '::1'

profile:
  # 存储 select 选择记录
  store-selected: false

  # 持久化 fake-ip
  store-fake-ip: true
#此处省略部分设置#
```

#### **Geodata 配置 ：**

```yaml
geodata-mode: true         #【Meta专属】使用geoip.dat数据库(默认：false使用mmdb数据库)

#自定义 geodata url
geox-url:
  geoip: "https://cdn.jsdelivr.net/gh/Loyalsoldier/v2ray-rules-dat@release/geoip.dat"
  geosite: "https://cdn.jsdelivr.net/gh/Loyalsoldier/v2ray-rules-dat@release/geosite.dat"
  mmdb: "https://cdn.jsdelivr.net/gh/Loyalsoldier/geoip@release/Country.mmdb"
```

**geodata-mode**：当为`true`时使用geoip.dat数据库，默认(可不写)为`false`,使用Country.mmdb数据库。（<mark style="color:red;">使用启动参数 -m 时，等同geodata-mode：true</mark>）

{% hint style="info" %}
* Meta使用 [**Loyalsoldier** ](https://github.com/Loyalsoldier/geoip)的 <mark style="color:blue;">\*\*\*\*</mark> <mark style="color:blue;">geoip</mark> 作为默认数据库，首次运行会自动下载对应数据库到clash主目录，受github.com访问现状的限制，建议自行下载到本地再运行Meta；
* [**Country.mmdb下载**](https://raw.githubusercontent.com/Loyalsoldier/geoip/release/Country.mmdb) | [**geoip.dat下载**](https://raw.githubusercontent.com/Loyalsoldier/geoip/release/geoip.dat)\*\*\*\*
{% endhint %}

```yaml
#此处省略部分设置#
#  find-process-mode has 3 values:always, strict, off
#  - always, 开启，强制匹配所有进程
#  - strict, 默认，由 clash 判断是否开启
#  - off, 不匹配进程，推荐在路由器上使用此模式
find-process-mode: strict

tcp-concurrent: true         #【Meta专属】TCP连接并发，如果域名解析结果对应多个IP，
                             # 并发所有IP，选择握手最快的IP进行连接

#此处省略部分设置#
```

**tcp-concurrent**：当为`true`时，如果域名解析结果对应多个IP，并发请求所有IP，选择握手最快的IP进行通讯。

#### **全局客户端指纹**：

```yaml
# 全局 TLS 指纹，优先低于 proxy 内的 client-fingerprint
# 可选： "chrome","firefox","safari","ios","random","none" options.
# Utls is currently support TLS transport in TCP/grpc/WS/HTTP for VLESS/Vmess and trojan.
global-client-fingerprint: chrome
```

{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">基础配置</mark>内容请参阅 [**完整示例**](broken-reference/) ，或者请查阅 [**Clash Wiki** ](https://lancellc.gitbook.io/clash/clash-config-file/general)。
{% endhint %}
