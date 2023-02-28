# 一般的 clash 语法

## 注释

在 yaml 格式的文件中,以"＃"作为注释开头,行尾为结尾,"#"必须在行头或者必须在前方有空格,否则不视为注释

```yaml
port: 7890 # http代理端口
socks-port: 7891
＃ socks代理端口
```

## IPV6地址

在clash内，应当使用 \[] 来框选一个IPV6地址

```yaml
[aaaa::a8aa:ff:fe09:57d8] 
[aaaa::a8aa:ff:fe09:57d9]:853 # 带端口的IPV6地址
```

## 域名通配符

### 通配符 ＊

clash的通配符 \* 一次只能匹配一级域名

\*.baudu.com 只匹配 tieba.baidu.com 而不匹配 123.tieba.baidu.com 或者 baidu.com

### 通配符 +

通配符 ＋ 类似DOMAIN-SUFFIX,可以一次性匹配多个级别

＋.baudu.com 匹配 tieba.baidu.com 和 123.tieba.baidu.com 或者 baidu.com

通配符 ＋ 只能用于域名前缀匹配

### 通配符 .

通配符 . 可以一次性匹配多个级别

.baudu.com 匹配 tieba.baidu.com 和 123.tieba.baidu.com, 但不能匹配 baidu.com

通配符 . 只能用于域名前缀匹配

### 使用示例

使用通配符时,应当使用引号 ‘ ’ 将内容包裹起来，以免过度匹配

```yaml
fake-ip-filter:
  - '.lan'
  - 'xbox.*.microsoft.com'
  - '+.xboxlive.com'
  - localhost.ptlogin2.qq.com
```
