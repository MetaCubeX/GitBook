---
description: 配置clash的tun模式
---

# tun模式

## 配置示例

<pre><code>tun:
  enable: true
  stack: system
  auto-detect-interface: true
  auto-route: true
  dns-hijack:
  - any:53
  # mtu: 9000
  # strict_route: true
  # inet4_route_address:
  # - 0.0.0.0/1
  # - 128.0.0.0/1
<strong>  # inet6_route_address:
</strong>  # - "::/1"
  # - "8000::/1"
  # endpoint_independent_nat: false
  # include_uid:
  # - 0
  # include_uid_range:
  # - 1000-99999
  # exclude_uid:
  #- 1000
  # exclude_uid_range:
  # - 1000-99999
  # include_android_user:
  # - 0
  # - 10
  # include_package:
  # - com.android.chrome
  # exclude_package:
  # - com.android.captiveportallogin
</code></pre>

### enable

是否启用tun模式来路由全局流量

```
enable: true
```

### stack

tun模式堆栈,可选system/gvisor/lwip,如无使用问题,只建议使用`system`栈

{% hint style="info" %}
## 协议栈之间的区别

system栈使用系统堆栈,可以提供更稳定/全面的tun体验,且占用相对其他堆栈更低

gvisor

lwip
{% endhint %}

```
stack: system
```

### auto-route

自动设置全局路由,可以自动将全局流量路由进入tun网卡

```
auto-route: true
```

### auto-detect-interface

自动选择流量出口接口,多出口网卡同时连接的设备建议手动指定出口网卡

```
auto-detect-interface: true
```

### dns-hijack

dns劫持,一般设置为 `any:53` 即可,即劫持所有53端口的udp流量

{% hint style="warning" %}
MACOS    无法自动劫持发往局域网的 dns 请求

ANDROID 如开启私人dns则无法自动劫持dns
{% endhint %}

```
dns-hijack:
- any:53
- tcp://any:53
```
