---
description: clash的dns模块配置
---

# DNS

## 示例

以下的拆分说明皆是 dns: 下的配置项

```yaml
dns:
  enable: true
  prefer-h3: true
  listen: 0.0.0.0:1053
  ipv6: true
  default-nameserver:
    - 114.114.114.114
    - 8.8.8.8
    - tls://1.12.12.12:853
    - tls://223.5.5.5:853
  enhanced-mode: fake-ip
  fake-ip-range: 198.18.0.1/16
  fake-ip-filter:
    - '*.lan'
    - localhost.ptlogin2.qq.com
  nameserver-policy:
    'www.baidu.com': '114.114.114.114'
    '+.internal.crop.com': '10.0.0.1'
    'geosite:cn': https://doh.pub/dns-query
  nameserver:
    - https://doh.pub/dns-query
    - https://dns.alidns.com/dns-query
  fallback:
    - tcp://1.1.1.1
    - 'tcp://1.1.1.1#
  proxy-server-nameserver:
    - https://doh.pub/dns-query
  fallback-filter:
    geoip: true
    geoip-code: CN
    geosite:
      - gfw
    ipcidr:
      - 240.0.0.0/4
    domain:
      - '+.google.com'
      - '+.facebook.com'
      - '+.youtube.com'
```

### enable

可选值 `true/false`

是否启用,如为false，则使用系统dns解析

```
dns:
  enable: true
```

### prefer-h3

可选值 `true/false`

是否开启DOH的http/3

```
prefer-h3: true
```

### listen

dns服务监听

```
listen: 0.0.0.0:1053
```

### IPV6

可选值 `true/false`

是否解析IPV6,如为false,则回应AAAA的空解析

```
ipv6: true
```

### enhanced-mode

可选值 `fake-ip / redir-host`

clash的dns处理模式

```
enhanced-mode: fake-ip
```

### fake-ip-range

格式为 `ip/掩码`

fakeip下的IP段设置, tun网卡的默认ip也使用此值

```
fake-ip-range: 198.18.0.1/16
```

### fake-ip-filter

fakeip过滤,以下地址不会下发fakeip映射用于连接

```
fake-ip-filter:
  - '*.lan'
  - localhost.ptlogin2.qq.com
```

### use-hosts

可选值 `true/false`

是否查询系统hosts

```
use-hosts: true
```

### default-nameserver

默认dns,用于解析 DNS服务器 的域名

必须为ip,可为加密dns

```
default-nameserver:
  - 114.114.114.114
  - 8.8.8.8
  - tls://223.5.5.5:853
  - https://223.5.5.5/dns-query
```

### nameserver-policy

指定域名查询的解析服务器,可使用 geosite,优先于`nameserver/fallback 查询`

`可书写多个,并发查询,以下仅作为书写演示`

```
nameserver-policy:
  'www.baidu.com': '114.114.114.114'
  '+.internal.crop.com': '10.0.0.1'
  'geosite:cn': https://doh.pub/dns-query
  'geosite:geolocation-!cn': [https://doh.pub/dns-query, https://dns.alidns.com/dns-query]
  'geosite:gfw':
  - tls://8.8.4.4
  - tls://1.0.0.1
```

### nameserver

默认的域名解析服务器,如不配置 `fallback/proxy-server-nameserver` ,则所有域名都由nameserver解析

```
nameserver:
  - tls://dot.pub
  - https://dns.alidns.com/dns-query
```

### proxy-server-nameserver

代理节点域名解析服务器,仅用于解析代理节点的域名

```
 proxy-server-nameserver:
   - https://doh.pub/dns-query
```

### fallback

后备域名解析服务器,一般情况下使用境外DNS,保证结果可信

配置`fallback`后默认启用`fallback-filter`,`geoip-code`为cn

```
fallback:
  - tls://dns.google
  - https://1.0.0.1/dns-query
```

### fallback-filter

后备域名解析服务器筛选,满足条件的将使用`fallback`结果或只使用`fallback`解析

#### geoip

可选值为 `true/false`

是否启用fallback filter

#### geoip-code

可选值为 国家缩写,默认值为 `CN`

除了 `geoip-code` 配置的国家IP,其他的IP结果会被视为污染

`geoip-code` 配置的国家的结果会直接采用,否则将采用`fallback`结果

#### geosite

可选值为对于的geosite内包含的集合

geosite列表的内容被视为已污染,匹配到geosite的域名,将只使用`fallback`解析,不去使用`nameserver`

#### ipcidr

书写内容为 `IP/掩码`

这些网段的结果会被视为污染,`nameserver`解析出这些结果时将会采用`fallback`的解析结果

#### domain

这些域名被视为已污染,匹配到这些域名,会直接使用`fallback`解析,不去使用`nameserver`

```
fallback-filter:
    geoip: true
    geoip-code: CN
    geosite:
      - gfw
    ipcidr:
      - 240.0.0.0/4
    domain:
      - '+.google.com'
      - '+.facebook.com'
      - '+.youtube.com'
```
