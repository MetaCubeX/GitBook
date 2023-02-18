---
cover: ../.gitbook/assets/bannera.jpg
coverY: 0
---

# 实验性配置

例：

```yaml
#此处省略部分设置#
experimental:
  # 具体配置待定
  # 证书指纹,SHA256格式,补充校验TLS证书
  # 可使用 openssl x509 -noout -fingerprint -sha256 -inform pem -in yourcert.pem 获取
  fingerprints:
    - "8F111FA9AD3CD8E917A118522CAC39EA33741B3BBE73F91CECE548D5CCB0E5E8" # 忽略大小写
#此处省略部分设置#
```

**fingerprints：**证书指纹,SHA256格式,补充校验TLS证书，为所有协议添加指纹（<mark style="color:red;">可使用 openssl x509 -noout -fingerprint -sha256 -inform pem -in yourcert.pem 获取</mark>）

{% hint style="warning" %}
若协议已经配置独立的指纹，将忽略 experimental.fingerprints
{% endhint %}

{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">基础配置</mark>内容请参阅 [**完整示例**](../example/ex1.md#ji-chu-pei-zhi) ，或者请查阅 [**Clash Wiki** ](https://lancellc.gitbook.io/clash/clash-config-file/general)。
{% endhint %}
