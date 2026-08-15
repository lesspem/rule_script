# rule_script

代理分流规则集合。格式与 [lesspem/Surge](https://github.com/lesspem/Surge) 保持一致。

## 123AV

覆盖 `123av.com` 及同源域名 `123av.app` / `123av.me`, 以及前身域名 `njav.tv`。

仅使用域名规则, 不含 IP-CIDR。这些站点均由 Cloudflare 托管, 解析出的
`104.21.x` / `172.67.x` / `104.26.x` 属共享 anycast 地址, pin 成 /32 会
误捞无关网站, 且会随时轮换, 因此不收录。

### Surge

```
RULE-SET,https://raw.githubusercontent.com/lesspem/rule_script/main/Surge/123AV.list,PROXY
```

### Quantumult X

```
https://raw.githubusercontent.com/lesspem/rule_script/main/QuantumultX/123AV.list, tag=123AV, force-policy=proxy, enabled=true
```
