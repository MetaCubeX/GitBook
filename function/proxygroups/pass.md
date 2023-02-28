# PASS跳过策略

Meta增加新的代理类型PASS，用以临时跳过某项规则。

例：

```yaml
proxy-groups:
  - name: NoAD
    type: select
    proxies:
      - PASS
      - REJECT

rule:
  - DOMAIN-KEYWORD,admaster,NoAD
  - DOMAIN-KEYWORD,admaster,vless
```

**PASS：**意为跳过/忽略，当代理组策略为PASS时，Meta忽略本条规则，继续向下查询。

&#x20;         （示例中，当NoAD的代理组选择<mark style="color:blue;">PASS</mark>时，Meta会<mark style="color:orange;">忽略第一条规则</mark>，匹配第二条规则走vless节点）

{% hint style="info" %}
使用场景：

**去广告类规则：**通常国内外去广告站点都写在一个proxy-groups下，想临时关闭时候只能DIRECT/Proxy，当DIRECT时，国外广告不通，当Proxy时，国内广告出国。使用PASS时就可以忽略去广告规则，继续向下匹配，完美解决这种尴尬。

**CDN的IP规则：**全球CDN服务可能将一个IP给很多站点使用，如果无法域名分流时，想要做精确分流比较尴尬，这时可以使用PASS规则灵活变通。
{% endhint %}



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">代理组配置</mark>内容请参阅 [**完整示例**](broken-reference) ，或者请查阅 [Clash Wiki ](https://lancellc.gitbook.io/clash/clash-config-file/proxy-groups)。
{% endhint %}
