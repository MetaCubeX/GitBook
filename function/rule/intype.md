# 入站类型规则

例：

```yaml
 rules:
  - IN-TYPE,SOCKS/HTTP,auto
```

**入站类型规则：**表示来自某入站类型的流量怎么走规则，支持（HTTP/HTTPS/SOCKS/TUN/TPROXY/REDIR/INNER）

例： `- IN-TYPE,SOCKS,PROXY`                   表示来自Socks端口的所有流量都走PROXY策略

&#x20;      `- IN-TYPE,TPROXY/INNER,PROXY`      表示来自`TPROXY和INNER`的所有流量都走PROXY策略

{% hint style="info" %}
INNER：表示来自Meta内部的请求，暂时只支持Provider更新。
{% endhint %}
