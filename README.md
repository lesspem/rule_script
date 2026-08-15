# rule_script

代理分流规则集合。

## 123av.com

覆盖 `123av.com` 主域名, 以及含 `123av` 关键词的镜像站与子域名。

### Surge

在配置 `[Rule]` 段添加:

```
RULE-SET,https://raw.githubusercontent.com/lesspem/rule_script/main/Surge/123av.list,PROXY
```

把末尾 `PROXY` 换成你自己的策略组名。

### Quantumult X

在配置 `[filter_remote]` 段添加:

```
https://raw.githubusercontent.com/lesspem/rule_script/main/QuantumultX/123av.list, tag=123av, force-policy=proxy, enabled=true
```

把 `force-policy=proxy` 里的 `proxy` 换成你自己的策略组名。

### 说明

`DOMAIN-KEYWORD` / `host-keyword` 用于覆盖该站频繁更换的镜像域名,
代价是会匹配任何含 `123av` 字样的域名。只要精确匹配可删掉该行。
