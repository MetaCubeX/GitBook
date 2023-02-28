---
cover: ../../.gitbook/assets/bannere.jpg
coverY: 0
---

# 规则配置

{% hint style="info" %}
本目录下的内容只展示Meta专属特性，全部<mark style="color:blue;">规则配置</mark>内容请参阅 [**完整示例**](broken-reference) ，或者请查阅 **Clash** [**Wiki**](https://lancellc.gitbook.io/clash/clash-config-file/rules) **** 。
{% endhint %}

#### 规则模块：

* 支持规则 GEOSITE
* 支持入站类型规则 IN-TYPE
* 支持<mark style="color:blue;">规则集 RULE-SET</mark>
* 支持规则 SRC-PORT 和 DST-PORT 的<mark style="color:blue;">多端口条件</mark>
* 支持规则对<mark style="color:blue;">TCP</mark> / <mark style="color:blue;">UDP分别管控</mark>
* 支持 Network 规则, 支持匹配网络类型 ( TCP / UDP )
* <mark style="color:blue;">支持逻辑判断规则</mark> ( NOT / OR / AND )
* 支持所有规则的源 IPCIDR 条件，只需附加到末尾即可
* 支持GEODATA MODE切换，mmdb / dat
* 支持切换GEODATA LOADER模式切换  ， 普通 / 小内存模式
* 支持GeoSite延迟加载 （无Geosite规则，getsite.dat不下载）
* GEOIP / GEOSITE 数据库基于 Loyalsoldier/v2ray-rules-dat
