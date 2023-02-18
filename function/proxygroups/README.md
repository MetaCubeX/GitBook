---
cover: ../../.gitbook/assets/bannerd.jpg
coverY: 0
---

# 代理组配置

{% hint style="info" %}
本目录下的内容只展示Meta专属特性，全部<mark style="color:blue;">代理组配置</mark>内容请参阅 [**完整示例**](../../example/ex1.md#dai-li-zu-pei-zhi) ，或者请查阅 [**Clash Wiki**](https://lancellc.gitbook.io/clash/clash-config-file/proxy-groups) **** 。
{% endhint %}

#### **代理模块：**

* 支持<mark style="color:blue;">PASS ( 跳过 )规则</mark>
* <mark style="color:blue;">Relay代理链支持UDP over TCP</mark>
* 支持<mark style="color:blue;">策略组正则筛选</mark>
* 主动健康检测urltest/fallback（基于tcp握手，限定时间内多次失败会主动触发健康检测使用节点）

