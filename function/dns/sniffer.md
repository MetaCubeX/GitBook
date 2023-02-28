# Sniffer域名嗅探器

Clash使用Mapping机制解决透明代理情况下，无法通过Redir端口传递域名的问题；但此机制会导致如果不使用Clash内置的DNS解析服务，就无法准确还原域名，进行域名分流的问题。

Meta内置了Sniffer域名嗅器，通过读取握手包内的域名字段，将IP还原成域名，有效解决Mapping机制的短板。

#### <mark style="color:blue;">配置示例：</mark>

```yaml
sniffer:
  enable: true
  sniffing:
    - tls
    - http
  skip-domain:
    - 'Mijia Cloud'
    - 'dlg.io.mi.com'
    - '+.apple.com'
  # - '*.baidu.com'
    
  force-domain:
  # - '+'
    - 'google.com'
    
  port-whitelist:
    - 443
    - 8000-9000
```

**sniffing：**需要嗅探的协议类型

{% hint style="info" %}
支持tls/http的嗅探，后续跟进其他类型
{% endhint %}



**skip-domain：**遇到sni字段为列表中的内容，保留mapping结果，不使用嗅探的内容覆盖mapping结果（主要解决部分站点sni字段非域名，导致嗅探结果异常的问题，支持通配符）

例：`- 'Mijia Cloud'`      米家设备SNI，建议添加

&#x20;      `- '+.apple.com'`      苹果站点，建议添加



**force-domain：**需要强制嗅探的域名（默认只对IP进行嗅探，支持通配符）\
（<mark style="color:orange;">优先级低于skip-sni，skip-sni内的域名不会被强制嗅探</mark>）

例：`- '+'`                           强制全局嗅探

&#x20;      `- 'google.com'`  &#x20;

&#x20;     `- '*.`netflix.com`.com'`  &#x20;

{% hint style="info" %}
* force-domain列表的响应内容为原mapping结果的域名；
* 使用全局嗅探时，注意维护<mark style="color:blue;">skip-domain</mark>名单，否则可能因apple/Mijia等部分域名的<mark style="color:orange;">sni字段非域名</mark>，导致相关站点访问异常。
{% endhint %}



**port-whitelist：**端口白名单，只对名单内的端口进行嗅探还原域名（不写为全端口）。

例：`- 443`                       单个端口

&#x20;      `- 8000-9000`          端口范围



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">DNS配置</mark>内容请参阅 [**完整示例**](broken-reference) ，或者请查阅 [Clash Wiki ](https://lancellc.gitbook.io/clash/clash-config-file/dns)。
{% endhint %}
