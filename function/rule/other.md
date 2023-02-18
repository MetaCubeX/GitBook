# 子规则集

例：

```yaml
rules:
  - DOMAIN-SUFFIX,baidu.com,DIRECT
  - DOMAIN-KEYWORD,google,ss1
  - IP-CIDR,1.1.1.1/32,ss1
  - IP-CIDR6,2409::/64,DIRECT
  
  # 当满足条件是 TCP 或 UDP 流量时，使用名为 sub-rule-name1 当规则集
  - SUB-RULE,(OR,((NETWORK,TCP),(NETWORK,UDP))),sub-rule-name1 
  # 当定义多个子规则集时，规则将以分叉匹配
  - SUB-RULE,(AND,((NETWORK,UDP))),sub-rule-name2

#                                               google.com(not match)--> baidu.com(match)
#                                                /                                ｜
#                                               /                                 ｜
#  https://baidu.com  --> rule1 --> rule2 --> sub-rule-name1(match tcp)          使用 DIRECT
#
#
#                                              google.com(not match)--> baidu.com(not match)
#                                                /                            ｜
#                                               /                             ｜
#  dns 1.1.1.1  --> rule1 --> rule2 --> sub-rule-name1(match udp)         sub-rule-name2(match udp)
#                                                                             ｜
#                                                                             ｜
#                                                                 使用 REJECT <-- 1.1.1.1/32(match)
#

sub-rules:
  sub-rule-name1:
    - DOMAIN,google.com,ss1
    - DOMAIN,baidu.com,DIRECT
  sub-rule-name2:
    - IP-CIDR,1.1.1.1/32,REJECT
    - IP-CIDR,8.8.8.8/32,ss1
    - DOMAIN,dns.alidns.com,REJECT
```

**支持SUB-RULE规则：**定义多个子规则集，规则将以分叉匹配



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">规则配置</mark>内容请参阅 [**完整示例**](../../example/ex1.md#gui-ze-pei-zhi) ，或者请查阅 [Clash Wiki ](https://lancellc.gitbook.io/clash/clash-config-file/rules)。
{% endhint %}
