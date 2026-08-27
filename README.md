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

## GitHub

覆盖网页与 API (`github.com`, 含 `api` / `gist` / `codeload` / `npm.pkg` 等子域),
静态与用户内容 (`githubusercontent.com` 覆盖 `raw` / `avatars` / `objects` /
`camo` / `user-images`; `githubassets.com`), Pages (`github.io`),
Codespaces (`github.dev`), Copilot (`githubcopilot.com`), 容器镜像 (`ghcr.io`),
GitHub App 回调 (`githubapp.com`), 以及 `githubstatus.com` / `github.blog` /
`github.community` / `githubnext.com` / `git.io`。

Release 附件、上传的图片附件和仓库归档实际由 S3 分发, 域名形如
`github-production-release-asset-2e65be.s3.amazonaws.com`,
中间的 hash 段会变, 因此用 `DOMAIN-KEYWORD,github-production` 一条兜住三类
(`release-asset` / `user-asset` / `repository-file`)。LFS 与部分 artifact
走 `github-cloud.s3.amazonaws.com`, 单独按整域名收录。

同样不含 IP-CIDR。GitHub 前端在 Fastly / Azure 上, `/meta` 接口公布的网段
是共享的, 且会调整, pin IP 既误捞又易失效。

两点需要留意:

- `github.io` 是 Pages 的公共后缀, 收录它意味着所有第三方 Pages 站点一并走代理。
  只想代理 GitHub 本体的话删掉这条。
- 域名清单来自 GitHub 官方文档与常见实践, 未做逐条抓包实测 (本机 DNS 走
  fake-ip, 无法用解析结果验证), 如遇漏放行的子域名请补充。

- Surge: `RULE-SET,https://raw.githubusercontent.com/lesspem/rule_script/main/Surge/GitHub.list,PROXY`
- QX: `https://raw.githubusercontent.com/lesspem/rule_script/main/QuantumultX/GitHub.list, tag=GitHub, force-policy=proxy, enabled=true`
