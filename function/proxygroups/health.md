# 主动健康检测

Meta支持urltest/fallback的主动健康检测：当TCP连接<mark style="color:blue;">**5秒内5次**</mark>握手失败，主动触发健康检测机制（进行URL-Test），自动切换节点。



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">代理组配置</mark>内容请参阅 [**完整示例**](../../example/ex1.md#dai-li-zu-pei-zhi) ，或者请查阅 [Clash Wiki ](https://lancellc.gitbook.io/clash/clash-config-file/proxy-groups)。
{% endhint %}
