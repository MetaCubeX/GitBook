# Tuic 节点支持

Meta增加了Tuic协议支持，具体格式如下：

```yaml
proxies:
  - name: tuic
    server: www.example.com
    port: 10443
    type: tuic
    token: TOKEN
    # ip: 127.0.0.1 # for overwriting the DNS lookup result of the server address set in option 'server'
    # heartbeat-interval: 10000
    # alpn: [h3]
    # disable-sni: true
    reduce-rtt: true
    # request-timeout: 8000
    udp-relay-mode: native # Available: "native", "quic". Default: "native"
    # congestion-controller: bbr # Available: "cubic", "new_reno", "bbr". Default: "cubic"
    # max-udp-relay-packet-size: 1500
    # fast-open: true
    # skip-cert-verify: true
    # max-open-streams: 20 # default 100, too many open streams may hurt performance
```

{% hint style="warning" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">代理配置</mark>内容请参阅 [**完整示例**](broken-reference) ，或者请查阅 [Clash Wiki](https://lancellc.gitbook.io/clash/clash-config-file/proxies) 。
{% endhint %}

