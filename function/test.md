---
description: 配置 TLS 相关配置
cover: ../.gitbook/assets/bannera.jpg
coverY: 0
---

# TLS

例：

```yaml
#  global-client-fingerprint: 全局 TLS 指纹,优先低于proxy内的 client-fingerprint
#  支持 "chrome","firefox","safari","ios","random","none" options.
#  支持基于 TCP/grpc/WS/HTTP 传输的 VLESS/Vmess/Trojan 的 TLS 流量
global-client-fingerprint: chrome

# ---分割线---

external-controller-tls: 0.0.0.0:9443 # RESTful API HTTPS 监听地址，需要配 `tls` 部分配置文件
tls:
  certificate: string # 用于 external-controller-tls 证书 PEM 格式，或者 证书的路径
  private-key: string # 用于 external-controller-tls 证书对应的私钥 PEM 格式，或者私钥路径
  # 自定义证书验证，将加入 Clash 证书验证中，绝大多数 TLS 相关支持，如：DNS，节点
  # 可用于自定义证书的验证
  custom-certificates:
    - certificate: string # 证书 PEM 格式，或者 证书的路径
      private-key: string # 证书对应的私钥 PEM 格式，或者私钥路径
```



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">基础配置</mark>内容请参阅 [**完整示例**](../example/ex1.md#ji-chu-pei-zhi) ，或者请查阅 [**Clash Wiki** ](https://lancellc.gitbook.io/clash/clash-config-file/general)。
{% endhint %}
