# Http Headers支持

Meta支持Http协议自定义Headers，用于伪造UA标识，进行免流等操作：

例：

```yaml
proxies:
  - name: "http"
    type: http
    server: server
    port: 443
      headers:
        X-T5-Auth: "1962xxxxx709"
        User-Agent: "okhttp/3.11.0 Dalvik/2.1.0 ...... "
```



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">代理配置</mark>内容请参阅 [**完整示例**](broken-reference) ，或者请查阅 [Clash Wiki](https://lancellc.gitbook.io/clash/clash-config-file/proxies) 。
{% endhint %}
