---
cover: ../.gitbook/assets/bannera.jpg
coverY: 0
---

# 基础配置

例：

```yaml
#此处省略部分设置#
geodata-mode: true         #【Meta专属】使用geoip.dat数据库(默认：false使用mmdb数据库)
tcp-concurrent: true         #【Meta专属】TCP连接并发，如果域名解析结果对应多个IP，
                             # 并发所有IP，选择握手最快的IP进行连接
#此处省略部分设置#
```

**geodata-mode：**当为`true`时使用geoip.dat数据库，默认(可不写)为`false`,使用Country.mmdb数据库。（<mark style="color:red;">使用启动参数 -m 时，等同geodata-mode：true</mark>）

{% hint style="info" %}
* Meta使用 [**Loyalsoldier** ](https://github.com/Loyalsoldier/geoip)的 <mark style="color:blue;">****</mark> <mark style="color:blue;"></mark><mark style="color:blue;">geoip</mark> 作为默认数据库，首次运行会自动下载对应数据库到clash主目录，受github.com访问现状的限制，建议自行下载到本地再运行Meta；
* [**Country.mmdb下载**](https://raw.githubusercontent.com/Loyalsoldier/geoip/release/Country.mmdb)  |  [**geoip.dat下载**](https://raw.githubusercontent.com/Loyalsoldier/geoip/release/geoip.dat)****
{% endhint %}



**tcp-concurrent：**当为`true`时，如果域名解析结果对应多个IP，并发请求所有IP，选择握手最快的IP进行通讯。



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">基础配置</mark>内容请参阅 [**完整示例**](../example/ex1.md#ji-chu-pei-zhi) ，或者请查阅 [**Clash Wiki** ](https://lancellc.gitbook.io/clash/clash-config-file/general)。
{% endhint %}
