# 代理组筛选

Meta支持对代理组名字进行筛选，过滤不需要的节点。

例：

```yaml
proxy-groups:
  - name: "proxy" 
    type: select
    proxies:
      - HK01
      - HK02
      - SG01
    filter: 'HK'
```

**filter：**筛选支持所有type（<mark style="color:blue;">url-test/fallback</mark>/<mark style="color:blue;">load-balance</mark>/<mark style="color:blue;">select</mark>)，支持正则表达式。

&#x20;         （示例中表示只显示HK01和HK02节点）

{% hint style="info" %}
使用筛选可能会在一定程度上增加CPU占用/转发延迟，尤其是使用较为复杂正则的情况下。
{% endhint %}



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">代理组配置</mark>内容请参阅 [**完整示例**](../../example/ex1.md#dai-li-zu-pei-zhi) ，或者请查阅 [Clash Wiki](https://lancellc.gitbook.io/clash/clash-config-file/proxy-groups) 。
{% endhint %}
