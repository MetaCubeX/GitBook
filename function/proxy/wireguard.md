# Wireguard节点支持

Meta增加了Wireguard协议支持，具体格式如下：

```yaml
proxies:
  - name: "wg"
    type: wireguard
    server: 162.159.192.1
    port: 2480
    ip: 172.16.0.2
    ipv6: fd01:5ca1:ab1e:80fa:ab85:6eea:213f:f4a5
    private-key: eCtXsJZ27+4PbhDkHnB923tkUn2Gj59wZw5wFA75MnU=
    public-key: Cr8hWlKvtDt7nrvf+f0brNQQzabAqrjfBvas9pmowjo=
    udp: true
    # reserved: 'U4An'
```

配置格式同步官方核心，并支持双栈。 ipv6 为meta特性配置项&#x20;



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">代理配置</mark>内容请参阅 [**完整示例**](../../example/ex1.md#dai-li-pei-zhi) ，或者请查阅 [Clash Wiki](https://lancellc.gitbook.io/clash/clash-config-file/proxies) 。
{% endhint %}
