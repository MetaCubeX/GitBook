# Relay代理链支持UDP

Meta的Relay代理链支持UDP over TCP。

例：

```yaml
proxy-groups:
  - name: "relay"          #【Meta专属】relay支持UDP over TCP
    type: relay            #中继代理，不能中继套娃中继
    proxies:               #流量走向：clash <-> ss1 <-> vmess <-> Internet
      - ss
      - vmess
      
proxies:
  - name: "ss"
    type: ss
    server: server
    port: 443
    cipher: chacha20-ietf-poly1305
    password: "password"
    
  - name: "vmess"
    type: vmess
    server: server
    port: 443
    uuid: uuid
    alterId: 32
    cipher: auto
    udp: true             #落地代理必须启用UDP，并且支持UDP over TCP
       
```

{% hint style="info" %}
* Relay的UDP支持并非真UDP，是通过UDP over TCP实现；
* 无需手动添加参数，满足以下条件后自动启用：

&#x20;      Relay代理链的落地代理必须开启`udp：true`，且支持UDP over TCP。
{% endhint %}



{% hint style="danger" %}
本文内容只展示Meta专属特性，全部<mark style="color:blue;">代理组配置</mark>内容请参阅 [**完整示例**](../../example/ex1.md#dai-li-zu-pei-zhi) ，或者请查阅 [Clash Wiki](https://lancellc.gitbook.io/clash/clash-config-file/proxy-groups) 。
{% endhint %}
