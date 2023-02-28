# DNS 按策略解析

&#x20;示例：

```yaml
dns:
    #此处省略部分设置#
  nameserver-policy:
    'www.baidu.com':'114.114.114.114'
    '+.internal.crop.com':'10.0.0.1'
    "geosite:cn": 
      - https://doh.pub/dns-query
      - https://dns.alidns.com/dns-query
    #此处省略部分设置#   
```

**nameserver-policy:**  按指定策略分流 DNS ，可以使用 geosite 分流 DNS 解析。

例：

```yaml
"geosite:cn":   
  - https://doh.pub/dns-query
  - https://dns.alidns.com/dns-query      支持UDP/TCP/DoT/DoH/DoQ
```

{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">DNS配置</mark>内容请参阅 [**完整示例**](broken-reference) ，或者请查阅 [Clash Wiki ](https://lancellc.gitbook.io/clash/clash-config-file/dns)。
{% endhint %}
