# ASCA 节点订阅

ASCS Cloud（加拿大 Onoway, Alberta）上的自建节点，订阅文件供 Clash / mihomo / FlClash / Karing / Shadowrocket 等客户端导入。

## 文件

| 文件 | 用途 |
|---|---|
| `sub/clash.yaml` | Clash Meta / mihomo / FlClash / Karing 整份配置 |
| `sub/vless.txt` | 明文节点链接（纯文本订阅） |
| `sub/vless-base64.txt` | 同上的 base64 版本（部分客户端只认 base64） |

## 订阅链接

```
https://raw.githubusercontent.com/JLuo327/asca-nodes/main/sub/clash.yaml
https://raw.githubusercontent.com/JLuo327/asca-nodes/main/sub/vless.txt
https://raw.githubusercontent.com/JLuo327/asca-nodes/main/sub/vless-base64.txt
```

## 节点

| 名称 | 协议 | 入口 | 实测 |
|---|---|---|---|
| ASCA-vless | VLESS Reality（`xtls-rprx-vision`） | `2600:70ff:b8c1:1::504:443` | 2026-11-05 23:00 起 9/9 通过，成功率 100% |
| ASCA-hy2 | Hysteria2 | `2600:70ff:b8c1:1::504:8443` | 家宽 QUIC 被拦，未验证；需蜂窝网络复测 |

## 已知限制

- **纯 IPv6 出口**：节点没有 IPv4 出网，所以 `github.com` 这类只有 A 记录的站点走它必然失败。能用的前提是目标有 AAAA（或本机走 NAT64）。
- **hy2 在国内家宽大概率连不上**：实测该宽带上所有境外 QUIC（Cloudflare / Quad9 / Google，v4 与 v6 都试过）全部握手超时，而国内 QUIC 22 ms 正常 —— 属于线路拦截，不是节点故障。
- 延迟中位 250 ms，吞吐 0.1–2.6 MB/s 随时段波动（同机房 speedtest 对比显示瓶颈在中国↔加拿大国际段，节点上行 1 Gbps 不是瓶颈）。

## 安全

- 公开仓库里的 UUID / hysteria2 密码就是凭据，任何人拿到都能白用你的 VPS 流量。发现异常就把服务端的 UUID、密码换掉，再 `git push` 新链接。
- **要立刻让所有旧链接失效**：把这仓库改回 private（Settings → General → Danger Zone → Change visibility）。raw 链接对未登录用户立即 403。
- 18080（HTTP 代理）和 11080（SOCKS5 代理）是**无认证**的，故意没有进入本仓库。需要时单独手动加，不要公开。
