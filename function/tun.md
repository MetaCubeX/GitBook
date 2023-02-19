---
cover: ../.gitbook/assets/bannerf.jpg
coverY: 0
---

# TUN模式

```yaml
tun:
  enable: true
  stack: system             # system / gvisor / lwip liwp 仅为 1.13.2 以上的功能
  dns-hijack:               # 需要劫持的 DNS，‘any:53’ 表示劫持所有 53 流量
    - 'any:53'
  auto-route: false
  auto-detect-interface: false
  # mtu: 9000               # 最大传输单元
  # strict_route: true      # 将所有连接路由到 tun 来防止泄漏，但你的设备将无法其他设备被访问
  inet4_route_address:      # 启用 auto_route 时使用自定义路由而不是默认路由
    - 0.0.0.0/1
    - 128.0.0.0/1
  inet6_route_address:      # 启用 auto_route 时使用自定义路由而不是默认路由
    - '::/1'
    - '8000::/1'
  # device: meta            # 默认无需设置，MacOS 务必不配置此项
  # endpoint_independent_nat: false         # 启用独立于端点的 NAT
  # include_uid: # UID 规则仅在 Linux 下被支持，并且需要 auto_route
    # - 0
  # include_uid_range: # 限制被路由的的用户范围
    # - 1000-99999
  # exclude_uid: # 排除路由的的用户
    #- 1000
  # exclude_uid_range: # 排除路由的的用户范围
    # - 1000-99999

  # Android 用户和应用规则仅在 Android 下被支持
  # 并且需要 auto_route

  # include_android_user: # 限制被路由的 Android 用户
    # - 0
    # - 10
  # include_package: # 限制被路由的 Android 应用包名
    # - com.android.chrome
  # exclude_package: # 排除被路由的 Android 应用包名
    # - com.android.captiveportallogin

```
