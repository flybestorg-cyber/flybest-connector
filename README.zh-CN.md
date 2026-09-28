# 我把旅行社的订房系统接进了 Claude

[English](README.md) · 中文

**FlyBest** 是一个 AI 订酒店连接器（MCP）。装进 Claude 或 ChatGPT 之后，你正常聊天：去哪、几号、几个人，它去旅行社的预订系统里读实时房价，把礼遇、取消条款讲清楚，选好了直接帮你订，订完的单在对话里就能查、能取消。免费使用，不用注册账号。

- Claude 目录：https://claude.ai/directory/connectors/flybest （Claude → Customize → Connectors 里搜 **FlyBest**）
- 连接地址：`https://ai.flybest.org/mcp`
- 作者：奢游公子 Jay（FlyBest），持牌旅行社 Coastline Travel Advisors 旗下的独立旅行顾问，自己动手做的

## 为什么做它

做顾问这些年，最花时间的一件事是替客人一家家酒店去问：这个房价含不含早、有没有额度、能升房吗、几号前能退。客人问一句「帮我看看」，我这边要翻半天。所以我把这些活交给了 AI：它去查，它来讲，选好了它来订。

## 和其它 AI 旅行工具有什么不同

| | 一般 AI 助手 / 旅行类 AI 工具 | FlyBest |
|---|---|---|
| 价格从哪来 | 网上搜来的、可能是缓存的价格 | 旅行社预订系统里的实时库存和房价 |
| 能不能订 | 给你一个订房网站的链接 | 直接把单订出来，订单在你名下 |
| 礼遇 | 看不到旅行社渠道的礼遇 | 礼遇写在每一行房价旁边，和公开价并排比 |
| 取消条款 | 要自己去啃 | 用人话写出来：几号前免费取消、押金多少、不可退会标出 |
| 订完以后 | 各找各的 | 对话里查订单、取消订单，只看得到自己的 |

## 礼遇：同一间房，同一个价，差在这几行

通过合作项目订的房价，通常和公开价**同价**，但会多出：

- 每天两人早餐
- 酒店消费额度（有的酒店给，有的不给，以酒店确认为准）
- 到店看房态升房
- 早到晚退（看房态）
- 欢迎礼

项目包括 **Virtuoso**、Four Seasons Preferred Partner、Rosewood Elite、Mandarin Oriental Fan Club、Peninsula PenClub、Belmond Bellini Club、Dorchester Collection Diamond Club、Maybourne Exclusive、Hyatt Privé、Hilton for Luxury、IHG Destined、Accor Preferred、Shangri-La Luxury Circle、SLH Within、Preferred Platinum Partner、Kempinski Club 1897、Langham Couture、Rocco Forte Knights、Jumeirah。

实测（2026-09-27）：京都三井酒店，两人三晚，实时查到 29 个房价。Virtuoso 礼遇价含早餐、100 美元酒店额度、看房态升房；旁边的公开价同价，没有礼遇。

```
京都三井，11 月 12 到 15 日，两个人

[Virtuoso 礼遇价]  豪华房 · 大床 · 三晚 · 11 月 5 日前免费取消
                   含：每天两人早餐 · USD 100 酒店额度 · 到店看房态升房 · 早到晚退 · 欢迎礼
[公开价]           豪华房 · 大床 · 三晚 · 同价 · 11 月 5 日前免费取消
                   含：—
```

## 怎么用（两分钟）

**Claude（网页 / 桌面 / 手机）**
1. Customize → Connectors，搜 **FlyBest**，点 Connect。
2. 在弹出的页面里留邮箱，收一个 6 位验证码。没有密码，不用注册。
3. 回到对话，直接说：「京都 11 月 12 到 15 号，两个人，看看有什么酒店。」

**ChatGPT（网页版开发者模式）**
1. Settings → Security and login → 打开 Developer mode。
2. 添加自定义 MCP 服务器：`https://ai.flybest.org/mcp`，认证选 OAuth。
3. 同样的邮箱验证码页面。手机 App 目前可能看不到自定义连接器。

**装成 Claude 插件（推荐）**：本仓库同时是一个 Claude 插件包，带 `flybest-hotels` skill，装上以后 Claude 自动知道订房的规矩（订前确认什么、押金怎么读、什么绝不能做）。上架后在 Claude 的 Customize → Plugins 里搜；Claude Code 里：

```bash
claude plugin add flybestorg-cyber/flybest-connector
```

## 你可以这样问

- 「找一下京都 11 月 12 到 15 号的酒店，两个人，靠近祇园。」
- 「三井这家含早餐的房价和取消条款给我看看。」
- 「按 Jane Doe 的名字订那个可退的房价，邮箱和电话是……」→ 它给你一个一次性确认页面，你在页面上看清条款再确认。
- 「我的订单」「把京都那单取消」

## 先说清楚

- 只做酒店，不做机票。
- 每个账号每天有查询上限，正常使用足够。
- 礼遇以酒店确认为准，升房看当天房态；价格以确认页和酒店确认为准。
- 需要能打开 Claude / ChatGPT 的网络环境。

## 条款、隐私、安全

- [使用条款](https://ai.flybest.org/terms) · [隐私说明](https://ai.flybest.org/privacy)
- 发现安全问题请看 [SECURITY.md](SECURITY.md)

本仓库只放公开文档和 skill，服务端代码不公开。
