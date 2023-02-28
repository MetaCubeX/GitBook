# IP规则

例：

```yaml
rules:
  #目的IP规则
  - IP-CIDR,127.0.0.0/8,DIRECT
  - IP-CIDR,122.122.0.0/8,DIRECT,no-resolve #no-resolve:不解析，可应用于GEOIP, IP-CIDR
  
  #来源IP规则
  - SRC-IP-CIDR,192.168.1.201/32,DIRECT
```

**指定协议类型：**可直接直接在规则最后跟协议类型(tcp/udp)，表示该规则只对指定协议生效。

例： `- IP-CIDR,127.0.0.0/8,DIRECT,`<mark style="color:blue;">`tcp`</mark>



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">规则配置</mark>内容请参阅 [**完整示例**](broken-reference) ，或者请查阅 [Clash Wiki ](https://lancellc.gitbook.io/clash/clash-config-file/rules)。
{% endhint %}
