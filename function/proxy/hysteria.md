# Hysteria节点支持

Meta增加了Hysteria协议支持，具体格式如下：

```yaml
proxies:
  - name: "hysteria"
    type: hysteria
    server: server.com
    port: 443
    auth_str: yourpassword
    #obfs: yourpassword
    alpn:
      - h3  #1.13.2以上版本变更为数组
    protocol: udp          #支持udp/wechat-video/faketcp
    up: '30 Mbps'          #若不写单位，默认为Mbps
    down: '200 Mbps'       #若不写单位，默认为Mbps
    #sni: server.com
    #skip-cert-verify: false
    #recv_window_conn: 12582912
    #recv_window: 52428800
    #auth_str: "yubiyubi"
    #ca: "./my.ca"
    #ca_str: "xyz"
    #disable_mtu_discovery: false
```

更多内容请参阅 [**Hysteria Wiki**](https://github.com/HyNetwork/hysteria/wiki/%E9%AB%98%E7%BA%A7%E7%94%A8%E6%B3%95#%E5%AE%A2%E6%88%B7%E7%AB%AF) **** 。



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">代理配置</mark>内容请参阅 [**完整示例**](../../example/ex1.md#dai-li-pei-zhi) ，或者请查阅 [Clash Wiki](https://lancellc.gitbook.io/clash/clash-config-file/proxies) 。
{% endhint %}
