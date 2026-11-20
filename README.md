# egern-muse-proxy · Muse / Meta AI 走代理规则集

让 `muse.ai` 和 Meta AI 相关流量走代理（境内直连打不开）。

## 文件

- `muse.list` — Surge 兼容格式，无策略列，引用处指定代理策略
- `muse.yaml` — Egern 原生格式（`domain_suffix_set` / `domain_set`）

## Egern 用法

规则集 → 新建远程 → 策略选你的代理组：

```
https://cdn.jsdelivr.net/gh/wukris1106/egern-muse-proxy@main/muse.yaml
```

或 Surge 格式：

```
https://cdn.jsdelivr.net/gh/wukris1106/egern-muse-proxy@main/muse.list
```

## 域名来源

直接读 `https://muse.ai/` 的 `Content-Security-Policy` 响应头，按段取：

- `connect-src` → `gateway.meta.ai`、`edge-chat.meta.ai`、`edge-chat-latest.meta.ai`、`shortwave.meta.ai`（**WebSocket 也在这里，漏了聊天一直转圈**）
- `img-src` / `media-src` → `*.metaaiusercontent.com`、`*.fbcdn.net`、`*.cdninstagram.com`、`*.fbsbx.com`
- `frame-src` → `auth.meta.com`、`agent.meta.ai`、Stripe（登录与订阅）

## 校验

- 每个域名经 AliDNS DoH 实测可解析
- 刻意不收 `meta.com` / `whatsapp.com` 整个消费者域族 —— 那会把别的 App 一起送进代理
- 重建于 2026-11-21（原 `bluee1111/egern-muse-proxy` tag v1.0.0）
