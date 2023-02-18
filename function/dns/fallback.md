# Fallback功能扩展

Meta对fallback部分增加了一些特性：

#### &#x20;<mark style="color:blue;">示例：</mark>

```yaml
dns:
    #此处省略部分设置#
  fallback:
    - quic://a.passcloud.xyz:784
    - 'tls://8.8.4.4:853#DNSg'
                                     
  fallback-filter:
    geosite:
      - gfw
```

**支持Dns over quic：**同时支持 nameserver/fallback

例：`- quic://a.passcloud.xyz:784`



**支持使用代理解析 ip：**允许DNS服务器通过代理节点通讯

例：`- 'tls://8.8.4.4:853#DNSg'`&#x20;

表示：这个dot的dns服务将会通过名为<mark style="color:orange;">DNSg</mark>的<mark style="color:blue;">代理组</mark>(proxy groups)访问

{% hint style="info" %}
* 使用该功能时，一定要注意正确使用引号；去掉引号#DNSg会被当成注释而无法正常代理；
* 请指定确认存在的<mark style="color:blue;">代理组</mark>(proxy groups)，错误的<mark style="color:blue;">代理组名称</mark>将会导致该DNS不可用。
{% endhint %}

****

**支持 Fallback-Filter 使用 Geosite：**Meta可使用geosite.dat作为默认规则数据库使用在rule或者fallback-filter中。

```yaml
fallback-filter:  
  geosite: 
    - gfw     #geosite中的gfw分类使用fallback内的dns解析
```

{% hint style="info" %}
* Meta使用 [**Loyalsoldier**](https://github.com/Loyalsoldier/v2ray-rules-dat) 的 [**geosite.dat**](https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geosite.dat) 作为默认数据库，当有geosite规则时自动下载到clash主目录；
* 受github.com访问现状的限制，建议自行下载到本地再运行Meta。
{% endhint %}

****

{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">DNS配置</mark>内容请参阅 [**完整示例**](../../example/ex1.md#dns-pei-zhi) ，或者请查阅 [Clash Wiki ](https://lancellc.gitbook.io/clash/clash-config-file/dns)。
{% endhint %}
