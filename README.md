# rule_script

代理分流规则集合。格式与 [lesspem/Surge](https://github.com/lesspem/Surge) 保持一致。

## 123AV

覆盖 `123av.com` 及其同源域名 `123av.app` / `123av.me`, 以及前身域名 `njav.tv`。
IP-CIDR 段为上述域名当前解析出的 Cloudflare 地址, 作为 DNS 污染时的兜底。

### Surge

```
RULE-SET,https://raw.githubusercontent.com/lesspem/rule_script/main/Surge/123AV.list,PROXY
```

### Quantumult X

```
https://raw.githubusercontent.com/lesspem/rule_script/main/QuantumultX/123AV.list, tag=123AV, force-policy=proxy, enabled=true
```
