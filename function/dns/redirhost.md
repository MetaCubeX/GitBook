# Reidr Host恢复域名传递

{% hint style="info" %}
官方原版Clash于[v1.80](https://github.com/Dreamacro/clash/releases/tag/v1.8.0)版本后，为了防止单IP对应多域名情况下mapping失败，停止了Redir Host模式下向远端VPS传递域名的行为（这样无法通过VPS进行远端DNS解析，导致<mark style="color:orange;">跨国多CDN网站无法就近解析</mark>/机场的<mark style="color:orange;">Netflix的DNS解锁失效</mark>等问题）；
{% endhint %}

Meta回滚了Redir Host部分代码，仍然保留官方v1.70以前的Redir Host模式的域名传递行为，配合Meta独有的 [**Sniffer域名嗅探器**](sniffer.md) ，可完美解决上文所述问题。



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">DNS配置</mark>内容请参阅 [**完整示例**](broken-reference) ，或者请查阅 [Clash Wiki ](https://lancellc.gitbook.io/clash/clash-config-file/dns)。
{% endhint %}
