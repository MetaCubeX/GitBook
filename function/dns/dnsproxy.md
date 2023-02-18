# 代理服务器解析DNS

&#x20;示例：

```yaml
dns:
    #此处省略部分设置#
  proxy-server-nameserver:
    - tls://1.0.0.1:853
    #此处省略部分设置#   
```

**proxy-server-nameserver：**当proxy里的server为域名时，使用该列表里的dns服务器解析。

例：`- tls://1.0.0.1:853`      支持UDP/TCP/DoT/DoH/DoQ

{% hint style="info" %}
* 当配置文件无此字段的时候，使用nameserver列表里的dns解析；
* 请务必确保此处的dns无污染，可正常使用，否则节点可能无法连接。
{% endhint %}



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">DNS配置</mark>内容请参阅 [**完整示例**](../../example/ex1.md#dns-pei-zhi) ，或者请查阅 [Clash Wiki ](https://lancellc.gitbook.io/clash/clash-config-file/dns)。
{% endhint %}
