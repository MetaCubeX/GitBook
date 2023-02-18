# Vless节点支持

Meta增加了Vless协议支持，具体格式如下：

#### <mark style="color:blue;">Vless-TCP</mark>

例：

```yaml
proxies:
  - name: "vless-tcp"
    type: vless
    server: server
    port: 443
    uuid: uuid
    network: tcp
    servername: example.com # AKA SNI
    # flow: xtls-rprx-direct # xtls-rprx-origin  # enable XTLS
    # skip-cert-verify: true

```



#### <mark style="color:blue;">Vless-WS</mark>

例：

```yaml
 proxies:   
  - name: "vless-ws"
    type: vless
    server: server
    port: 443
    uuid: uuid
    udp: true
    tls: true
    network: ws
    servername: example.com # priority over wss host
    # skip-cert-verify: true
    ws-opts:
      path: "/"
      headers:
        Host: example.com
```



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">代理配置</mark>内容请参阅 [**完整示例**](../../example/ex1.md#dai-li-pei-zhi) ，或者请查阅 [Clash Wiki](https://lancellc.gitbook.io/clash/clash-config-file/proxies) 。
{% endhint %}
