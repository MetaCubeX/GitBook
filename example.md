# 完整配置示例

{% hint style="info" %}
* 原开源Clash内核配置部分主要引自 [**Clash Wiki**](https://lancellc.gitbook.io/clash/clash-config-file/an-example-configuration-file) ，做了小部分调整和翻译；
* 注释标记<mark style="color:blue;">【Meta专属】</mark>内容为Meta核新特有功能，在其他Clash核心使用可能造成意想不到的后果。
{% endhint %}

## <mark style="color:blue;">基础配置</mark>

<pre class="language-yaml"><code class="lang-yaml"># port: 7890                 #本地http代理端口
# socks-port: 7891           #本地socks5代理端口
mixed-port: 7890             #本地混合代理(http和socks5合并）端口
# redir-port: 7892           #本地Linux/macOS Redir代理端口
# tproxy-port: 7893          #本地Linux Tproxy代理端口

# authentication:            # 本地SOCKS5/HTTP(S)代理端口认证设置
#  - "user1:pass1"
#  - "user2:pass2"

find-process-mode: strict     # always/ strict/ off 
                              #  进程匹配模式:
                              #  - always, 强制匹配所有进程
                              #  - strict, 默认，由 clash 判断是否开启
                              #  - off, 不匹配进程，推荐在路由器上使用此模式

# geodata-mode: true         #【Meta专属】使用geoip.dat数据库(默认：false使用mmdb数据库)
tcp-concurrent: true         #【Meta专属】TCP连接并发，如果域名解析结果对应多个IP，
                             # 并发所有IP，选择握手最快的IP进行连接

allow-lan: false                  #允许局域网连接(false/true)
bind-address:                     #监听IP白名单（当allow-lan：true），只允许列表设备
  '*'                             #全部设备
  # 192.168.122.11                #单个ip4地址
  # "[aaaa::a8aa:ff:fe09:57d8]"   #单个ip6地址
  
mode: rule                 #clash工作模式（rule/global/direct,meta暂不支持script）

log-level: info            #日志等级（info/warning/error/debug/silent）

ipv6: false                #ip6开关，当为false时，停止解析hostanmes为ip6地址


tls:                  # 面板 TLS
  certificate: string # 证书 PEM 格式，或者 证书的路径
  private-key: string # 证书对应的私钥 PEM 格式，或者私钥路径

external-controller: 0.0.0.0:9093 # RESTful API 监听地址
external-controller-tls: 0.0.0.0:9443 # RESTful API HTTPS 监听地址，需要配置 tls 部分配置文件

external-ui: folder                   #http服务路径，可以放静态web网页，如yacd的控制面板
                                      #可通过`http://{{external-controller}}/ui`直接使用
# secret: ""                          #控制器登录密码

# 全局 TLS 指纹，优先低于 proxy 内的 client-fingerprint
# 可选： "chrome","firefox","safari","ios","random","none" options.
# Utls is currently support TLS transport in TCP/grpc/WS/HTTP for VLESS/Vmess and trojan.
global-client-fingerprint: chrome

<strong># interface-name: en0        #出口网卡名称
</strong># routing-mark: 6666         #流量标记(仅Linux)

profile:                   #缓存设置(文件位置./cache.db)
  store-selected: false    #节点状态记忆（若不同配置有同代理名称,设置值共享）
  store-fake-ip: true      #fake-ip缓存
</code></pre>

## <mark style="color:blue;">TUN 配置</mark>

```yaml
tun:
  enable: false
  stack: system # system / gvisor / lwip
  dns-hijack:
    - 0.0.0.0:53               # 需要劫持的 DNS
  auto-detect-interface: true  # 自动识别出口网卡
  auto-route: true             # 配置路由表
  mtu: 9000                    # 最大传输单元
  # strict_route: true  # 将所有连接路由到tun来防止泄漏，但你的设备将无法其他设备被访问
```

## <mark style="color:blue;">DNS配置</mark>

```yaml
sniffer:                           #【Meta专属】sniffer域名嗅探器
  enable: false                    # 嗅探器开关       
                                   # 开启后对 redir-host 类型识别的流量进行强制嗅探
                                   # 包含 Tun、Redir 和 TProxy 或 DNS 为 redir-host
  # force-dns-mapping: false
  # parse-pure-ip: false           # 对所有未获取到域名的流量进行强制嗅探
  
  override-destination: false      # 是否使用嗅探结果作为实际访问，默认 true
                                   # 全局配置，优先级低于 sniffer.sniff 实际配置
  sniff: # TLS 默认如果不配置 ports 默认嗅探 443
    TLS:
      ports: [443, 8443]
    HTTP: # 需要嗅探的端口, 默认嗅探 80
      ports: [80, 8080-8880]
      override-destination: true # 可覆盖 sniffer.override-destination
  force-domain:
    - +.v2ex.com
  # 白名单，跳过嗅探结果
  skip-domain:
    - Mijia Cloud

hosts:                           #host，支持通配符（非通配符域名优先级高于通配符域名）
  # '*.clash.dev': 127.0.0.1     #例如foo.example.com>*.example.com>.example.com
  # '.dev': 127.0.0.1
  # 'alpha.clash.dev': '::1'
  
dns:
  enable: true                 #DNS开关(false/true)
  listen: 0.0.0.0:53           #DNS监听地址
  prefer-h3: true              # 开启 DoH 支持 HTTP/3，将并发尝试
  # ipv6: false                #IP6解析开关；如果为false，将返回ip6结果为空
  
  default-nameserver:          #解析非IP的dns用的dns服务器,只支持纯IP
    - 114.114.114.114
    - 8.8.8.8
    
  # 指定域名使用自定义DNS解析, 可以使用 geosite 分流 DNS 解析。
  # 将国内域名指定为国内 DOH 进行解析，其余 DNS 使用在 nameserver 使用境外/无污染 DOH 解析
  nameserver-policy:
    #   'www.baidu.com': '114.114.114.114'
    #   '+.internal.crop.com': '10.0.0.1'
    geosite:cn,private,apple:
      - https://doh.pub/dns-query
      - https://dns.alidns.com/dns-query
    "www.baidu.com,+.google.cn": [223.5.5.5, https://dns.alidns.com/dns-query]

  enhanced-mode: redir-host          #DNS模式(redir-host/fake-ip)
                                     #【Meta专属】redir-host传递域名，可远程解析
  # fake-ip-range: 198.18.0.1/16       #Fake-IP解析地址池
  # use-hosts: true                  #查询hosts配置并返回真实IP
  
  
  #proxy-server-nameserver:          #【Meta专属】解析代理服务器域名的dns
  # - tls://1.0.0.1:853              # 不写时用nameserver解析

  nameserver:                        #默认DNS服务器，支持udp/tcp/dot/doh/doq
    - https://dns.google/dns-query
    - https://dns.cloudflare.com/dns-query
    - https://doh.opendns.com/dns-query
    - https://doh.dns.sb/dns-query
    - https://[2001:4860:4860::8888]/dns-query
    - https://[2001:4860:4860::8844]/dns-query
    - https://[2001:4860:4860::6464]/dns-query
    - https://[2001:4860:4860::64]/dns-query
    # - tls://223.5.5.5:853 # DNS over TLS
    # - https://doh.pub/dns-query # DNS over HTTPS
    # - https://dns.alidns.com/dns-query#h3=true #【Meta专属】强制HTTP/3
    # - https://mozilla.cloudflare-dns.com/dns-query#DNS&h3=true #【Meta专属】指定策略组和使用 HTTP/3
    # - dhcp://en0 # dns from dhcp
    # - quic://dns.adguard.com:784 # DNS over QUIC
    # - '8.8.8.8#en0' # 兼容指定DNS出口网卡
    
  # fallback:                          #回落DNS服务器，支持udp/tcp/dot/doh/doq
  #   - https://doh.dns.sb/dns-query
  #   - tcp://208.67.222.222:443
  #   - quic://a.passcloud.xyz:784     #【Meta专属】Dns over quic
  #   - 'tls://8.8.4.4:853#DNSg'       #【Meta专属】"#DNSg"代表该DNS服务器通过
  #                                    # 名为"DNSg"的proxy Group访问
                                     
  # fallback-filter:                   #回落DNS服务器过滤
  #   geoip: true                      #为真时，不匹配为geoip规则的使用fallback返回结果
  #   geoip-code: CN                   #geoip匹配区域设定
  #   geosite:                         #【Meta专属】设定geosite某分类使用fallback返回结果
  #     - gfw
  #   ipcidr:                          #列表中的ip使用fallback返回解析结果
  #     - 240.0.0.0/4
  #   domain:                          #列表中的域名使用fallback返回解析结果
  #     - '+.google.com'
  #     - '+.facebook.com'
  #     - '+.youtube.com'
  
  # fake-ip-filter:                  #Fake-ip过滤，列表中的域名返回真实ip
  #   - "+.lan"
  #   # QQ Loopback
  #   - localhost.sec.qq.com
  #   - localhost.ptlogin2.qq.com
  #   - "+.linksys.com"
  #   - "+.pool.ntp.org"
  #   # Router
  #   - hiwifi.com
  #   - leike.cc
  #   - miwifi.com
  #   - my.router
  #   - peiluyou.com
  #   - phicomm.me
  #   - router.ctc
  #   - routerlogin.com
  #     # Tenda router
  #   - tendawifi.com
  #     # TP-Link router
  #   - tplinkwifi.net
  #     # Windows
  #   - “+.msftconnecttest.com”
  #   - “+.msftncsi.com”
  #     # 中興路由器
  #   - zte.home
  #     # Stun Services
  #   - "+.stun.*.*"
  #   - "+.stun.*.*.*"
  #   - "+.stun.*.*.*.*"
  #   - "+.stun.*.*.*.*.*"
  #     # Google Voices
  #   - "lens.l.google.com"
  #     # Nintendo Switch
  #   - "+.srv.nintendo.net"
  #     # PlayStation
  #   - "+.stun.playstation.net"
  #     # XBox
  #   - "xbox.*.*.microsoft.com"
  #   - "+.xboxlive.com"
  #     # Bilibili CDN
  #   - "+.mcdn.bilivideo.cn"
```

## <mark style="color:blue;">代理配置</mark>

```yaml
proxies:
    
    #【Meta专属】Hysteria
  - name: "hysteria"
    type: hysteria
    server: server.com
    port: 443
    auth_str: yourpassword
    # obfs: yourpassword
    alpn: h3
    protocol: udp          #支持udp/wechat-video/faketcp
    up: '30 Mbps'          #若不写单位，默认为Mbps
    down: '200 Mbps'       #若不写单位，默认为Mbps
    # sni: server.com
    # skip-cert-verify: false
    # recv_window_conn: 12582912
    # recv_window: 52428800
    # auth_str: "yubiyubi"
    # ca: "./my.ca"
    # ca_str: "xyz"
    # disable_mtu_discovery: false
    
    # fingerprint: xxxx #  使用 sha256 指纹
  
    #【Meta专属】tuic
  - name: tuic
    server: www.example.com
    port: 10443
    type: tuic
    token: TOKEN
    # ip: 127.0.0.1 # for overwriting the DNS lookup result of the server address set in option 'server'
    # heartbeat-interval: 10000
    # alpn: [h3]
    # disable-sni: true
    reduce-rtt: true
    # request-timeout: 8000
    udp-relay-mode: native # Available: "native", "quic". Default: "native"
    # congestion-controller: bbr # Available: "cubic", "new_reno", "bbr". Default: "cubic"
    # max-udp-relay-packet-size: 1500
    # fast-open: true
    # skip-cert-verify: true
    # max-open-streams: 20 # default 100, too many open streams may hurt performance
      
  #【Meta专属】Vless
  - name: "vless-tcp"
    type: vless
    server: server
    port: 443
    uuid: uuid
    network: tcp
    servername: example.com # AKA SNI
    # flow: xtls-rprx-direct # xtls-rprx-origin  # enable XTLS
    # skip-cert-verify: true
    # fingerprint: xxxx
    
  #【Meta专属】Vless   
  - name: "vless-ws"
    type: vless
    server: server
    port: 443
    uuid: uuid
    udp: true
    tls: true
    network: ws
    servername: example.com # priority over wss host
    # skip-cert-verify: true
    ws-opts:
      path: "/"
      headers:
        Host: example.com
    # fingerprint: xxxx
  
  # Wireguard         
  # 兼容官方核心配置，并支持双栈模式 
  - name: "wg"
    type: wireguard
    server: 1.2.3.4
    port: 1234
    ip: 172.16.0.2
    ipv6: fd01:5ca1:ab1e:80fa:ab85:6eea:213f:f4a5
    private-key: eCtXsJZ27+4PbhDkHnB923tkUn2Gj59wZw5wFA75MnU=
    public-key: Cr8hWlKvtDt7nrvf+f0brNQQzabAqrjfBvas9pmowjo=
    udp: true
    # reserved: 'U4An'
    
                                            
  # Shadowsocks
  # 加密支持:
  #   aes-128-gcm aes-192-gcm aes-256-gcm
  #   aes-128-cfb aes-192-cfb aes-256-cfb
  #   aes-128-ctr aes-192-ctr aes-256-ctr
  #   rc4-md5 chacha20-ietf xchacha20
  #   chacha20-ietf-poly1305 xchacha20-ietf-poly1305
  #【Meta专属】支持SS2022加密：
  #   2022-blake3-aes-128-gcm
  #   2022-blake3-aes-256-gcm
  #   2022-blake3-chacha20-poly1305
  - name: "ss1"
    type: ss
    server: server
    port: 443
    cipher: chacha20-ietf-poly1305
    password: "password"
    # udp: true

  - name: "ss2"
    type: ss
    server: server
    port: 443
    cipher: chacha20-ietf-poly1305
    password: "password"
    plugin: obfs
    plugin-opts:
      mode: tls # or http
      # host: bing.com

  - name: "ss3"
    type: ss
    server: server
    port: 443
    cipher: chacha20-ietf-poly1305
    password: "password"
    plugin: v2ray-plugin
    plugin-opts:
      mode: websocket # no QUIC now
      # tls: true # wss
      # skip-cert-verify: true
      # host: bing.com
      # path: "/"
      # mux: true
      # headers:
      #   custom: value

  # vmess
  # 加密支持 auto/aes-128-gcm/chacha20-poly1305/none
  - name: "vmess"
    type: vmess
    server: server
    port: 443
    uuid: uuid
    alterId: 32
    cipher: auto
    # udp: true
    # tls: true
    # skip-cert-verify: true
    # servername: example.com # priority over wss host
    # network: ws
    # ws-opts:
    #   path: /path
    #   headers:
    #     Host: v2ray.com
    #   max-early-data: 2048
    #   early-data-header-name: Sec-WebSocket-Protocol

  - name: "vmess-h2"
    type: vmess
    server: server
    port: 443
    uuid: uuid
    alterId: 32
    cipher: auto
    network: h2
    tls: true
    h2-opts:
      host:
        - http.example.com
        - http-alt.example.com
      path: /
  
  - name: "vmess-http"
    type: vmess
    server: server
    port: 443
    uuid: uuid
    alterId: 32
    cipher: auto
    # udp: true
    # network: http
    # http-opts:
    #   # method: "GET"
    #   # path:
    #   #   - '/'
    #   #   - '/video'
    #   # headers:
    #   #   Connection:
    #   #     - keep-alive

  - name: vmess-grpc
    server: server
    port: 443
    type: vmess
    uuid: uuid
    alterId: 32
    cipher: auto
    network: grpc
    tls: true
    servername: example.com
    # skip-cert-verify: true
    grpc-opts:
      grpc-service-name: "example"

  # socks5
  - name: "socks"
    type: socks5
    server: server
    port: 443
    # username: username
    # password: password
    # tls: true
    # skip-cert-verify: true
    # udp: true

  # http
  - name: "http"
    type: http
    server: server
    port: 443
    # username: username
    # password: password
    # tls: true # https
    # skip-cert-verify: true
    # sni: custom.com
    # headers:                      #【Meta专属】
    #   X-T5-Auth: "1962xxxxx709"
    #   User-Agent: "okhttp/3.11.0 Dalvik/2.1.0 ...... "

  # Snell
  # 不支持UDP
  - name: "snell"
    type: snell
    server: server
    port: 44046
    psk: yourpsk
    # version: 2
    # obfs-opts:
      # mode: http # or tls
      # host: bing.com

  # Trojan
  - name: "trojan"
    type: trojan
    server: server
    port: 443
    password: yourpsk
    # udp: true
    # sni: example.com # aka server name
    # alpn:
    #   - h2
    #   - http/1.1
    # skip-cert-verify: true

  - name: trojan-grpc
    server: server
    port: 443
    type: trojan
    password: "example"
    network: grpc
    sni: example.com
    # skip-cert-verify: true
    udp: true
    grpc-opts:
      grpc-service-name: "example"

  - name: trojan-ws
    server: server
    port: 443
    type: trojan
    password: "example"
    network: ws
    sni: example.com
    # skip-cert-verify: true
    udp: true
    # ws-opts:
      # path: /path
      # headers:
      #   Host: example.com

  # ShadowsocksR
  # 支持的加密: ss中的所有加密方法
  # 支持的obfses:
  #   plain http_simple http_post
  #   random_head tls1.2_ticket_auth tls1.2_ticket_fastauth
  # 支持的protocols:
  #   origin auth_sha1_v4 auth_aes128_md5
  #   auth_aes128_sha1 auth_chain_a auth_chain_b  
  - name: "ssr"
    type: ssr
    server: server
    port: 443
    cipher: chacha20-ietf
    password: "password"
    obfs: tls1.2_ticket_auth
    protocol: auth_sha1_v4
    # obfs-param: domain.tld
    # protocol-param: "#"
    # udp: true

```

## <mark style="color:blue;">代理组配置</mark>

```yaml
proxy-groups:
  - name: DNSg             #【Meta专属】DNS代理组，配合上文"DNS配置"使用
    type: url-test         #可任意name/type，此处仅做举例
    proxies:
      - ss1
      - ss2
      
  - name: "relay"          #【Meta专属】relay支持UDP over TCP
    type: relay            #中继代理，不能中继套娃中继     
    proxies:               #流量走向：clash <-> http <-> vmess <-> ss1 <-> Internet
      - http
      - vmess
      - ss1
      
  - name: "auto" 
    type: url-test         #通过httping URL 自动切换延迟最低的节点
    proxies:
      - ss1
      - ss2
      - vmess1
    # tolerance: 150       #容差值：节点差值低于设定值时，不自动切换
    # lazy: true           #为true时，未被使用时不进行测ping
    url: 'http://www.gstatic.com/generate_204'      #用来测ping的地址
    interval: 300          #测ping时间(秒)
    # disable-udp: true    #关闭UDP
    # filter: 'HK'         #【Meta专属】代理筛选

  - name: "fallback-auto"
    type: fallback         #通过httping URL，当没有ping值时，自动切换下一个节点
    proxies:
      - ss1
      - ss2
      - vmess1
    url: 'http://www.gstatic.com/generate_204'
    interval: 300
    # lazy: true
    # disable-udp: true
    # filter: 'HK'          #【Meta专属】代理筛选

  - name: "load-balance"
    type: load-balance      #负载均衡：同一域名(eTLD+1)使用同一代理
    proxies:
      - ss1
      - ss2
      - vmess1
    url: 'http://www.gstatic.com/generate_204'
    interval: 300
    # lazy: true
    # disable-udp: true
    # filter: 'HK'            #【Meta专属】代理筛选
    # strategy: round-robin   #策略：round-robin ：所有请求不使用同一代理
                              #consistent-hashing：同一有效顶级域名(eTLD)使用同一代理
                              
  - name: Proxy
    type: select              #手动代理组
    # disable-udp: true
    proxies:
      - PASS                  #【Meta专属】跳过：命中的规则会被忽略，继续向下查询
      - ss1
      - ss2
      - vmess1
      - auto
    # filter: 'HK'            #【Meta专属】代理筛选
 
  - name: en1
    type: select
    interface-name: en1       #指定网口
    proxies:
      - DIRECT 

  - name: UseProvider
    type: select
    use:
      - provider1
    # filter: 'HK'            #【Meta专属】代理筛选
    proxies:
      - Proxy
      - DIRECT

         
```

## <mark style="color:blue;">Providers 配置</mark>

```yaml
proxy-providers:
  provider1:
    type: http
    url: "https://abc.com/xhYdgd"    #【Meta专属】支持解析V2rayN等工具使用的普通订阅
    interval: 3600
    path: ./provider1.yaml
    health-check:
      enable: true
      interval: 600
      # lazy: true
      url: http://www.gstatic.com/generate_204
  test:
    type: file
    path: /test.yaml
    health-check:
      enable: true
      interval: 36000
      url: http://www.gstatic.com/generate_204

rule-providers:
  google:
    type: http
    behavior: classical
    path: ./rule1.yaml
    #【Meta专属】URL可根据rule设定匹配对应的策略，方便更新provider
    url: "https://raw.githubusercontent.com/../Google.yaml"
    interval: 600   
```

## <mark style="color:blue;">规则配置</mark>

```yaml
rules:
  #目的域名后缀规则
  - DOMAIN-SUFFIX,githubusercontent.com,auto
  - DOMAIN-SUFFIX,ad.com,REJECT
  - DOMAIN-SUFFIX,bilibili.com,DIRECT,tcp   #【Meta专属】可指定协议类型(tcp/udp)
  
  #目的域名规则
  - DOMAIN,google.com,auto
  
  #目的域名关键字规则
  - DOMAIN-KEYWORD,google,auto
  
  #目的IP规则
  - IP-CIDR,127.0.0.0/8,DIRECT
  - IP-CIDR,122.122.0.0/8,DIRECT,no-resolve #no-resolve:不解析，可应用于GEOIP, IP-CIDR
  
  #来源IP规则
  - SRC-IP-CIDR,192.168.1.201/32,DIRECT

  #目的端口规则
  - DST-PORT,123/136/137-139,DIRECT         #【Meta专属】可指定端口范围
  
  #来源端口规则
  - SRC-PORT,123/136/137-139,DIRECT,udp     #【Meta专属】可指定端口范围
  
  #【Meta专属】入站规则
  #支持HTTP/HTTPS/SOCKS5/SOCKS4/SOCKS/TUN/TPROXY/REDIR/INNER
  - IN-TYPE,SOCKS5/HTTP,auto
  
  #【Meta专属】逻辑判断规则
  - AND,((DOMAIN,baidu.com),(NETWORK,UDP)),DIRECT #AND(和):域名为baidu.com的UDP协议
  - OR,((NETWORK,UDP),(DOMAIN,baidu.com)),REJECT  #OR(或):UDP的协议，或者域名为baidu.com
  - NOT,((DOMAIN,baidu.com)),PROXY                #NOT(否)：域名不为baidu.com访问
  #域名关键词为bilibili或者douyu的UDP协议
  - AND,((OR,((DOMAIN-KEYWORD,bilibili),(DOMAIN-KEYWORD,douyu))),(NETWORK,UDP)),REJECT 
  
  #【Meta专属】子规则集规则
  - SUB-RULE,(OR,((NETWORK,TCP),(NETWORK,UDP))),sub-rule-name1 # 当满足条件是 TCP 或 UDP 流量时，使用名为 sub-rule-name1 当规则集
  - SUB-RULE,(AND,((NETWORK,UDP))),sub-rule-name2 # 定义多个子规则集，规则将以分叉匹配
  
  #【Meta专属】GEOSITE规则
  - GEOSITE,category-ads-all,REJECT
  - GEOSITE,apple-cn,DIRECT
  - GEOSITE,microsoft@cn,DIRECT
  - GEOSITE,facebook,PROXY
  - GEOSITE,youtube,PROXY
  - GEOSITE,cn,DIRECT
  - GEOSITE,geolocation-!cn,PROXY
  
  # Rule Provider规则
  - RULE-SET,google,PROXY                   # Meta支持RULE-SET规则
  
  # GEOIP规则  
  - GEOIP,telegram,PROXY,no-resolve
  - GEOIP,private,DIRECT,no-resolve
  - GEOIP,cn,DIRECT
  
  # 兜底规则
  - MATCH,auto
```
