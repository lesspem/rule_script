# rule_script

代理分流规则集合。格式与 [lesspem/Surge](https://github.com/lesspem/Surge) 保持一致。

## 123AV

覆盖 `123av.com` 及同源域名 `123av.app` / `123av.me`, 以及前身域名 `njav.tv`。

仅使用域名规则, 不含 IP-CIDR。这些站点均由 Cloudflare 托管, 解析出的
`104.21.x` / `172.67.x` / `104.26.x` 属共享 anycast 地址, pin 成 /32 会
误捞无关网站, 且会随时轮换, 因此不收录。

- Surge: `RULE-SET,https://raw.githubusercontent.com/lesspem/rule_script/main/Surge/123AV.list,PROXY`
- QX: `https://raw.githubusercontent.com/lesspem/rule_script/main/QuantumultX/123AV.list, tag=123AV, force-policy=proxy, enabled=true`

## DMM / FANZA

`dmm.co.jp` 一条即覆盖全站, 已实测确认以下子域名均在该后缀下:
`www` / `video` / `litevideo` / `cc3001` / `pics` / `p` / `accounts`。
`dmm.com` 与 `dmm.co.jp` 解析到同一地址, 且页面引用了 `stat.i3.dmm.com`。
`d2ezz24t9nm0vu.cloudfront.net` 为页面实测引用的 CloudFront 资源,
属自动生成的分发域名, 官方轮换分发后可能失效, 需复查。

注意: DMM / FANZA 影片播放有日本地区限制, 需使用日本节点, 且部分
机房 IP 会被拒。规则只负责把流量交给代理, 能否播放取决于节点出口。

- Surge: `RULE-SET,https://raw.githubusercontent.com/lesspem/rule_script/main/Surge/DMM.list,JAPAN`
- QX: `https://raw.githubusercontent.com/lesspem/rule_script/main/QuantumultX/DMM.list, tag=DMM, force-policy=japan, enabled=true`
