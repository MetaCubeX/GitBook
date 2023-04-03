# 懒人配置

proxy-providers写订阅就能用了(理论上)

```
######### 锚点 start #######
# proxy 相关
pr: &#x26;pr {type: select, proxies: [默认, 香港, 台湾, 日本, 新加坡, 美国, 其它地区, 全部节点, 自动选择, DIRECT]}

#这里是订阅更新和延迟测试相关的
p: &#x26;p {type: http, interval: 3600, health-check: {enable: true, url: https://www.gstatic.com/generate_204, interval: 300}}

use: &#x26;use
  type: select
  use:
  - provider1
  - provider2
  
######### 锚点 end #######

# url里填写自己的订阅,名称不能重复,path(文件位置)不能重复
proxy-providers:
  provider1:
    &#x3C;&#x3C;: *p
    url: ""
    path: ./proxy_providers/provider1.yaml

  provider2:
    &#x3C;&#x3C;: *p
    url: ""
    path: ./proxy_providers/provider2.yaml

mixed-port: 7890
unified-delay: false
geodata-mode: true
tcp-concurrent: false
find-process-mode: strict
global-client-fingerprint: chrome

allow-lan: true
mode: rule
log-level: info
ipv6: true

external-controller: 0.0.0.0:9090
#external-ui: ui
secret: ""

geox-url:
  geoip: "https://testingcf.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@release/geoip.dat"
  geosite: "https://testingcf.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@release/geosite.dat"
  mmdb: "https://testingcf.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@release/country.mmdb"

profile:
  store-selected: true
  store-fake-ip: true

sniffer:
  enable: false
  sniff:
    TLS:
      ports: [443, 8443]
    HTTP:
      ports: [80, 8080-8880]
      override-destination: true

tun:
  enable: true
  stack: system
  dns-hijack:
    - 'any:53'
  auto-route: true
  auto-detect-interface: true

dns:
  enable: true
  listen: 0.0.0.0:1053
  ipv6: true
  enhanced-mode: fake-ip
  fake-ip-range: 28.0.0.1/8
  fake-ip-filter:
  - '*'
  - '+.lan'
  default-nameserver:
  - 223.5.5.5
  nameserver:
  - 'tls://8.8.4.4#dns'
  - 'tls://1.0.0.1#dns'
  proxy-server-nameserver:
  - https://doh.pub/dns-query
  nameserver-policy:
    "geosite:cn,private":
    - https://doh.pub/dns-query
    - https://dns.alidns.com/dns-query

proxies:


proxy-groups:

  - {name: 默认, type: select, proxies: [DIRECT, 香港, 台湾, 日本, 新加坡, 美国, 其它地区, 全部节点, 自动选择 ]}

  - {name: dns, type: select, proxies: [自动选择, DIRECT, 默认, 香港, 台湾, 日本, 新加坡, 美国, 其它地区, 全部节点]}

  - {name: Google, &#x3C;&#x3C;: *pr}

  - {name: Telegram, &#x3C;&#x3C;: *pr}

  - {name: Twitter, &#x3C;&#x3C;: *pr}

  - {name: pixiv, &#x3C;&#x3C;: *pr}

  - {name: ehentai, &#x3C;&#x3C;: *pr}

  - {name: 哔哩哔哩, &#x3C;&#x3C;: *pr}

  - {name: 哔哩哔哩api, &#x3C;&#x3C;: *pr}

  - {name: 哔哩东南亚, &#x3C;&#x3C;: *pr}

  - {name: 巴哈姆特, &#x3C;&#x3C;: *pr}

  - {name: YouTube, &#x3C;&#x3C;: *pr}

  - {name: NETFLIX, &#x3C;&#x3C;: *pr}

  - {name: Spotify, &#x3C;&#x3C;: *pr}

  - {name: github, &#x3C;&#x3C;: *pr}

  - {name: 国内, type: select, proxies: [DIRECT, 默认, 香港, 台湾, 日本, 新加坡, 美国, 其它地区, 全部节点, 自动选择]}

  - {name: 其他, &#x3C;&#x3C;: *pr}

#分隔，下面是地区分组
  - {name: 香港, &#x3C;&#x3C;: *use,filter: "(?i)港|hk|hongkong|kong kong"}

  - {name: 台湾, &#x3C;&#x3C;: *use, filter: "(?i)台|tw|taiwan"}

  - {name: 日本, &#x3C;&#x3C;: *use, filter: "(?i)日本|jp|japan"}

  - {name: 美国, &#x3C;&#x3C;: *use, filter: "(?i)美|us|unitedstates|united states"}

  - {name: 新加坡, &#x3C;&#x3C;: *use, filter: "(?i)^(?!.*(?:us)).*(新|sg|singapore)"}

  - {name: 其它地区, &#x3C;&#x3C;: *use, filter: "(?i)^(?!.*(?:🇭🇰|🇯🇵|🇺🇸|🇸🇬|🇨🇳|港|hk|hongkong|台|tw|taiwan|日|jp|japan|新|sg|singapore|美|us|unitedstates)).*"}

  - {name: 全部节点, &#x3C;&#x3C;: *use}

  - {name: 自动选择, proxies: [DIRECT], &#x3C;&#x3C;: *use, tolerance: 2, type: url-test}

rules:

  - GEOSITE,biliintl,哔哩东南亚
  - GEOSITE,ehentai,ehentai
  - GEOSITE,github,github
  - GEOSITE,twitter,Twitter
  - GEOSITE,youtube,YouTube
  - GEOSITE,google,Google
  - GEOSITE,telegram,Telegram
  - GEOSITE,netflix,NETFLIX
  - GEOSITE,bilibili,哔哩哔哩
  - GEOSITE,bahamut,巴哈姆特
  - GEOSITE,spotify,Spotify
  - GEOSITE,geolocation-!cn,其他

  - GEOIP,google,Google
  - GEOIP,netflix,NETFLIX
  - GEOIP,telegram,Telegram
  - GEOIP,twitter,Twitter
  - GEOSITE,CN,国内
  - GEOIP,CN,国内
  - MATCH,其他
```

****
