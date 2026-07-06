# po0fw — po0 防火墙自动加白 Surge 模块

自动把设备当前出口 IP 加入 po0 防火墙白名单，加白后才能连上开启了防火墙的 po0 机器。

📖 **图文教程 / 一键安装：<https://po0fw.rlyio.com/>**

## 特性

- **多机器**：`tokens` 参数英文逗号分割多个 `pgnfw_` token，一台机器一个。
- **省坑位**：GET 先查，当前出口已在白名单则不 POST（白名单上限 5 个，API 无删除能力）。
- **蜂窝优化**：蜂窝（CGNAT）下自动加白 24h 内最多消耗 2 个坑位，超限只通知；面板手动刷新不受限。
- **即时响应**：network-changed 事件即时触发 + 每 2 分钟 cron 兜底。
- **面板**：显示白名单 IP 与坑位占用（不显示 token），蜂窝加白的 IP 标 📶，当前出口标 ←。
- **安静**：KV 记录状态，仅在失败、限频或消耗新坑位时通知。

## 安装

```
surge:///install-module?url=https%3A%2F%2Fraw.githubusercontent.com%2Freallinzc%2Fpo0fw%2Fmain%2Fpo0-firewall-whitelist.sgmodule
```

安装后在模块参数 `tokens` 填入 `pgnfw_xxx`（多个用 `,` 分割）。token 只保存在你自己的 Surge 配置里，模块与本仓库不包含、不上传任何 token。

## 文件

- `po0-firewall-whitelist.sgmodule` — Surge 模块（规则 + cron/事件/面板脚本挂载）
- `scripts/po0-firewall-whitelist.js` — 加白脚本
- `web/index.html` — 教程页源码（部署于 po0fw.rlyio.com）
