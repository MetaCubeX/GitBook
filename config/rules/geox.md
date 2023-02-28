# GEO规则

## GEOSITE

域名集合,匹配集合内的域名,具体参考 [https://github.com/v2fly/domain-list-community/tree/master/data](https://github.com/v2fly/domain-list-community/tree/master/data)

```
  GEOSITE,google,proxy
  GEOSITE,cn,DIRECT
```

## GEOIP

国家IP代码规则,匹配集合内相应的IP范围

```
GEOIP,CN,DIRECT
GEOIP,LAN,DIRECT
```

### no-resolve

当请求为域名匹配到GEOIP或IP-CIDR规则时,clash将请求DNS查询来检查域名的IP是否匹配此条规则,可以选择“`no-resolve`”选项以跳过域名去进行dns解析

如在更早的匹配中触发了解析,则依旧会匹配到添加了“`no-resolve`”选项的IP规则

如`enhanced-mode`为`redir-host`,则此选项无效

```
GEOIP,lan,DIRECT,no-resolve
```

