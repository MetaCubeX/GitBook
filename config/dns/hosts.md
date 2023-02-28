# hosts

```yaml
hosts:                           #host，支持通配符（非通配符域名优先级高于通配符域名）
  '*.clash.dev': 127.0.0.1     #例如foo.example.com>*.example.com>.example.com
  '.dev': 127.0.0.1
  'alpha.clash.dev': '::1'
```
