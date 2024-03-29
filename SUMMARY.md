# Table of contents

* [简介](README.md)
* [使用Meta的客户端](used/README.md)
  * [在线面板](used/zai-xian-mian-ban.md)
* [完整配置示例](example.md)
  * [懒人配置](example/lan-ren-pei-zhi.md)

## Meta特性 <a href="#function" id="function"></a>

* [基础配置](function/general.md)
* [DNS配置](function/dns/README.md)
  * [Sniffer域名嗅探器](function/dns/sniffer.md)
  * [Reidr Host恢复域名传递](function/dns/redirhost.md)
  * [DNS 按策略解析](function/dns/nameserver-policy.md)
  * [代理服务器解析DNS](function/dns/dnsproxy.md)
  * [Fallback功能扩展](function/dns/fallback.md)
* [代理配置](function/proxy/README.md)
  * [VLESS 节点支持](function/proxy/vless.md)
  * [Hysteria节点支持](function/proxy/hysteria.md)
  * [Tuic 节点支持](function/proxy/tuic-jie-dian-zhi-chi.md)
  * [Wireguard节点支持](function/proxy/wireguard.md)
  * [Http Headers支持](function/proxy/http.md)
  * [Provider功能扩展](function/proxy/provider.md)
* [代理组配置](function/proxygroups/README.md)
  * [PASS跳过策略](function/proxygroups/pass.md)
  * [Relay代理链支持UDP](function/proxygroups/relay.md)
  * [代理组筛选](function/proxygroups/filter.md)
  * [主动健康检测](function/proxygroups/health.md)
* [规则配置](function/rule/README.md)
  * [域名规则](function/rule/domain.md)
  * [IP规则](function/rule/ip.md)
  * [端口规则](function/rule/port.md)
  * [入站类型规则](function/rule/intype.md)
  * [逻辑判断规则](function/rule/logic.md)
  * [GEO规则](function/rule/geo.md)
  * [子规则集](function/rule/other.md)
  * [其他](function/rule/other-1.md)

## 配置文件 WIP <a href="#config" id="config"></a>

* [一般的 clash 语法](config/yaml.md)
* [全局配置](config/general.md)
* [Tun 模式](config/tun.md)
* [DNS](config/dns.md)
  * [域名嗅探](config/dns/sniffer.md)
  * [hosts](config/dns/hosts.md)
* [代理](config/proxies.md)
  * [socks](config/proxies/socks.md)
  * [http](config/proxies/http.md)
  * [ss](config/proxies/ss.md)
  * [ssr](config/proxies/ssr.md)
  * [trojan](config/proxies/trojan.md)
  * [vmess](config/proxies/vmess.md)
  * [vless](config/proxies/vless.md)
  * [tuic](config/proxies/tuic.md)
  * [hysteria](config/proxies/hysteria.md)
  * [wg](config/proxies/wg.md)
* [代理策略](config/proxy-groups.md)
  * [内置策略](config/proxy-groups/built-in.md)
  * [手动选择](config/proxy-groups/select.md)
  * [自动选择](config/proxy-groups/url-test.md)
  * [自动回退](config/proxy-groups/fallback.md)
  * [负载均衡](config/proxy-groups/load-balance.md)
  * [链式代理](config/proxy-groups/relay.md)
  * [指定接口以及路由标记](config/proxy-groups/interface-name-and-routing-mark.md)
* [代理集合](config/proxy-providers.md)
  * [代理集合内容](config/proxy-providers/content.md)
  * [引用代理集](config/proxy-providers/use.md)
  * [筛选代理集](config/proxy-providers/filter.md)
  * [健康检查](config/proxy-providers/health-check.md)
* [规则](config/rules.md)
  * [域名规则](config/rules/domain.md)
  * [IP规则](config/rules/ipcidr.md)
  * [端口规则](config/rules/port.md)
  * [入站类型规则](config/rules/intype.md)
  * [逻辑规则](config/rules/logic.md)
  * [进程规则](config/rules/process.md)
  * [GEO规则](config/rules/geox.md)
  * [规则集](config/rules/rule-provider.md)
  * [子规则](config/rules/sub-rule.md)
  * [最终匹配](config/rules/match.md)
* [规则集合](config/rule-providers.md)
* [子规则](config/sub-rules.md)
* [流量入站](config/liu-liang-ru-zhan.md)
* [隧道](config/tunnels.md)
* [实验性配置](config/test.md)

## 关于

* [项目地址](https://github.com/MetaCubeX/Clash.Meta/tree/Meta)
