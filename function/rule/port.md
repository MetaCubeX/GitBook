# 端口规则

例：

```yaml
rules:
  #目的端口规则
  - DST-PORT,123/136/137-139,DIRECT         #【Meta专属】可指定端口范围
  
  #来源端口规则
  - SRC-PORT,123/136/137-139,DIRECT,udp     #【Meta专属】可指定端口范围
```

**支持多端口复合写法：**允许一条规则定义多个端口。

&#x20;例： `- DST-PORT,`<mark style="color:blue;">`123/136`</mark>`,DIRECT`      表示：123和136，两个端口  (“/”表示 "和")

&#x20;        `- SRC-PORT,`<mark style="color:blue;">`137-139`</mark>`,DIRECT`    表示：137到139，三个端口  (“-”表示 "至")

&#x20;        `- SRC-PORT,123/136/137-139,DIRECT`    表示 123和136以及137到139，共5个端口



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">规则配置</mark>内容请参阅 [**完整示例**](../../example/ex1.md#gui-ze-pei-zhi) ，或者请查阅 [Clash Wiki ](https://lancellc.gitbook.io/clash/clash-config-file/rules)。
{% endhint %}
