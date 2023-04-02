# 懒人配置

by [汐殇](http://localhost:5000/u/3eOHDxrQBnMwW5CB7DtVSHLFgKL2 "mention")

```yaml
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
  proxy-server-naneserver:
  - https://doh.pub/dns-query
  nameserver-policy:
    "geosite:cn,private":
    - https://doh.pub/dns-query
    - https://dns.alidns.com/dns-query
  "+.atri.ink":
    - https://doh.pub/dns-query

proxies:
p: &p
  {type: http, interval: 3600, health-check: {enable: true, url: https://www.gstatic.com/generate_204, interval: 300}}
pr: &pr
  {type: select, proxies: [默认, 香港, 台湾, 日本, 新加坡, 美国, 其它地区, 全部节点, 自动选择, DIRECT]}

u: &u
  type: select
  use:
  - provider1
  - provider2

proxy-providers:
  provider1:
    <<: *p
    url: ""
    path: ./proxy_providers/provider1.yaml

  provider2:
    <<: *p
    url: ""
    path: ./proxy_providers/provider2.yaml

proxy-groups:

  - {name: 默认, type: select, proxies: [DIRECT, 香港, 台湾, 日本, 新加坡, 美国, 其它地区, 全部节点, 自动选择 ]}

  - {name: dns, type: select, proxies: [自动选择, DIRECT, 默认, 香港, 台湾, 日本, 新加坡, 美国, 其它地区, 全部节点]}

  - {name: Google, <<: *pr}

  - {name: Telegram, <<: *pr}

  - {name: Twitter, <<: *pr}

  - {name: pixiv, <<: *pr}

  - {name: ehentai, <<: *pr}

  - {name: 哔哩哔哩, <<: *pr}

  - {name: 哔哩哔哩api, <<: *pr}

  - {name: 哔哩东南亚, <<: *pr}

  - {name: 巴哈姆特, <<: *pr}

  - {name: YouTube, <<: *pr}

  - {name: NETFLIX, <<: *pr}

  - {name: Spotify, <<: *pr}

  - {name: github, <<: *pr}

  - {name: 国内, type: select, proxies: [DIRECT, 默认, 香港, 台湾, 日本, 新加坡, 美国, 其它地区, 全部节点, 自动选择]}

  - {name: 其他, <<: *pr}

#分隔，下面是地区分组
  - {name: 香港, <<: *u,filter: "(?i)港|hk|hongkong|kong kong"}

  - {name: 台湾, <<: *u, filter: "(?i)台|tw|taiwan"}

  - {name: 日本, <<: *u, filter: "(?i)日本|jp|japan"}

  - {name: 美国, <<: *u, filter: "(?i)美|us|unitedstates|united states"}

  - {name: 新加坡, <<: *u, filter: "(?i)^(?!.*(?:us)).*(新|sg|singapore)"}

  - {name: 其它地区, <<: *u, filter: "(?i)^(?!.*(?:🇭🇰|🇯🇵|🇺🇸|🇸🇬|🇨🇳|港|hk|hongkong|台|tw|taiwan|日|jp|japan|新|sg|singapore|美|us|unitedstates)).*"}

  - {name: 全部节点, <<: *u}

  - {name: 自动选择, proxies: [DIRECT], <<: *u, tolerance: 2, type: url-test}

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
