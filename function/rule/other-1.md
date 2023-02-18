# 其他

例：

```yaml
 rules:
  #Rule Provider规则
  - RULE-SET,apple,REJECT                  # Meta支持RULE-SET规则
  
  #兜底规则
  - MATCH,auto
```

**支持RULE-SET规则：**Meta支持Clash Premium核心的Rule Provider，用法同原版一致。



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">规则配置</mark>内容请参阅 [**完整示例**](../../example/ex1.md#gui-ze-pei-zhi) ，或者请查阅 [Clash Wiki ](https://lancellc.gitbook.io/clash/clash-config-file/rules)。
{% endhint %}
