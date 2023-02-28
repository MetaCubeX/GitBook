# 域名规则

例：

```yaml
rules:
  #目的域名后缀规则
  - DOMAIN-SUFFIX,google.com,auto
  - DOMAIN-SUFFIX,ad.com,REJECT
  - DOMAIN-SUFFIX,bilibili.com,DIRECT,tcp    #【Meta专属】可指定协议类型(tcp/udp)
  
  #目的域名规则
  - DOMAIN,google.com,auto
  
  #目的域名关键字规则
  - DOMAIN-KEYWORD,google,auto
```

**指定协议类型：**可直接直接在规则最后跟协议类型(tcp/udp)，表示该规则只对指定协议生效。

例：`- DOMAIN-SUFFIX,bilibili.com,DIRECT,`<mark style="color:blue;">`tcp`</mark>



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">规则配置</mark>内容请参阅 [**完整示例**](broken-reference) ，或者请查阅 [Clash Wiki ](https://lancellc.gitbook.io/clash/clash-config-file/rules)。
{% endhint %}
