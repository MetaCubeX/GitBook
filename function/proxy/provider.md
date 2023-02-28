# Provider功能扩展

Meta对fallback部分增加了一些特性，更加方便使用：

例：

```yaml
proxy-providers:
  provider1:
    type: http
    #【Meta专属】URL支持解析V2rayN等工具使用的普通订阅
    url: "https://abc.com/xhYdgd"
    interval: 3600
    path: ./provider1.yaml
    health-check:
      enable: true
      interval: 600
      # lazy: true
      url: http://www.gstatic.com/generate_204

rule-providers:
  google:
    type: http
    behavior: classical
    path: ./rule1.yaml
    #【Meta专属】URL可根据rule设定匹配对应的策略，方便更新provider
    url: "https://raw.githubusercontent.com/../Google.yaml"
    interval: 600
    
rule:
  - DOMAIN-SUFFIX,githubusercontent.com,Proxy
  
```

**Proxy-Provider支持普通订阅：**prxoy-provider的url参数支持<mark style="color:blue;">直接解析V2rayN等客户端使用的普通订阅</mark>，无需使用SubConverter之类的订阅转换工具。

****

**Provider可通过代理通道更新：**Provider的URL自行依从<mark style="color:orange;">Clash的当前规则(rule)设定</mark>匹配对应<mark style="color:blue;">代理</mark>/<mark style="color:blue;">直连</mark>通道，无需手动干预，解决GitHub等库无法直连的尴尬。



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">代理配置</mark>内容请参阅 [**完整示例**](broken-reference) ，或者请查阅 [Clash Wiki](https://lancellc.gitbook.io/clash/clash-config-file/proxies) 。
{% endhint %}
