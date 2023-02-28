# GEO规则

例：

```yaml
rules:
    #【Meta专属】GEOSITE规则
  - GEOSITE,category-ads-all,REJECT
  - GEOSITE,icloud@cn,DIRECT
  - GEOSITE,apple@cn,DIRECT
  - GEOSITE,apple-cn,DIRECT
  - GEOSITE,microsoft@cn,DIRECT
  - GEOSITE,facebook,PROXY
  - GEOSITE,youtube,PROXY
  - GEOSITE,geolocation-cn,DIRECT
  - GEOSITE,geolocation-!cn,PROXY
  
  #GEOIP规则  
  - GEOIP,telegram,PROXY,no-resolve
  - GEOIP,private,DIRECT,no-resolve
  - GEOIP,cn,DIRECT
```

**支持GeoSite规则：**Meta支持V2ray的GeoSite数据库，可直接在rules里引用。

例：`- GEOSITE,microsoft@cn,DIRECT`

{% hint style="info" %}
* Meta使用 [**Loyalsoldier**](https://github.com/Loyalsoldier/v2ray-rules-dat) 的 [**geosite.dat**](https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geosite.dat) 作为默认数据库，当有geosite规则时自动下载到clash主目录；
* 受github.com访问现状的限制，建议自行下载到本地再运行Meta。
{% endhint %}



**更换Geoip默认数据库：**Meta默认使用 [**Loyalsoldier** ](https://github.com/Loyalsoldier/geoip)的增强数据库替换原有的的 [Maxmind](https://www.maxmind.com/en/home) 数据库，分组更全，cn更精确。（Meta可使用geoip.dat作为默认数据库，详看 [**geodata-mode**](../general.md) **）**





{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">规则配置</mark>内容请参阅 [**完整示例**](broken-reference) ，或者请查阅 [Clash Wiki ](https://lancellc.gitbook.io/clash/clash-config-file/rules)。
{% endhint %}
