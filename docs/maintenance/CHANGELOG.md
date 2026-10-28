# flybest-connector 修改与修复日志

本日志按日期追加。先参考相关历史，再补充新记录；不要删除或改写历史修复理由。

## 2026-10-02 洛杉矶

- [今日行为基线与已发布版本](entries/2026-10-02-release-baseline.md)
- [建立维护记录要求并保存日报](entries/2026-10-02-maintenance-policy.md)

## 2026-10-04 洛杉矶

- [公开文档对齐线上公开工具契约（插件 1.1.5）](entries/2026-10-04-public-docs-live-contract.md)

## 2026-10-05 洛杉矶

- [MCP Registry 补充公开仓库地址，登记版本 1.0.2，README 增加配置和使用入口](entries/2026-10-05-mcp-registry-repository.md)
- [发布补记：公开清单已推送，官方 Registry 1.0.2 已发布并回读 active/latest](entries/2026-10-05-mcp-registry-repository.md#发布结果补记2026-10-05-1831-pdt)

## 2026-10-07 洛杉矶

- [Priced recommendations and booking conversion (1.1.6)](entries/2026-10-07-hotel-skills-conversion.md)
- [Publication receipt: PR merged, version 1.1.6 published, related MCP guidance deployed and health verified](entries/2026-10-07-hotel-skills-conversion.md#publication-and-live-verification--2026-10-07-pdt)

## 2026-10-08 洛杉矶

- [Customer-facing hotel Skill refresh: targeted benefits, booking verification and plugin installation guidance (1.1.7)](entries/2026-10-08-public-hotel-skill-refresh.md)
- [Publication receipt: source 1.1.7 pushed and GitHub main verified; no backend restart](entries/2026-10-08-public-hotel-skill-refresh.md#publication-receipt--2026-10-08-1608-pdt)
- [Claude directory verification: 1.1.7 passed scanning and is Serving after automatic publication](entries/2026-10-08-public-hotel-skill-refresh.md#claude-directory-live-verification--2026-10-08-1614-pdt)

## 2026-10-11 洛杉矶

- [Loyalty wording restored (points and elite nights credited as usual; status benefits on top), per-row benefit-lookup status lines, install link wording (1.1.8)](entries/2026-10-11-loyalty-wording.md)
- Template: added a length target (body about 12 KB; full test inventories and raw logs stay out of records), matching the other two repositories.

## 2026-10-13 洛杉矶

- [README 安装链接从发布者管理页改为公开安装页（三处）](entries/2026-10-13-plugin-install-link.md)
- 推送回执：`e68006f` 已于 2026-10-13 推送到 GitHub main，ls-remote 一致。

## 2026-10-14 洛杉矶

- [README 增加 “Updating”：目录安装自动更新；GitHub marketplace 安装在 Claude Code 里打开自动更新或手动 update 后 `/reload-plugins`。Skill 复查无需改动，版本仍为 1.1.8](entries/2026-10-14-readme-updating.md)
- 推送回执：`9525aa2` 已于 2026-10-14 推送到 GitHub main，ls-remote 一致。
- [Skill/README 1.1.9：付款链接邮箱可选（不给就用注册邮箱，付款人在页面确认或修改）；“价格变了”分已有页面重新同意与铸链被拒没有页面两种情况；付款页约 10 分钟、结果给关闭时间、关了没订没扣马上重开](entries/2026-10-14-booking-wording-1-1-9.md)
- [Skill 1.1.10 “先搜再问”（draft, not published; held with sabre-booking draft/public-search-first-2026-10-14）：任何问酒店/住哪/房价/有没有房当轮就搜，没日期用服务端样例日期并在首行说明；样例结果只用一行问日期和人数，床型/行程/会员等真实日期的第一批报价；样例日期不取 rates、不报总价、不开付款页；description 加“什么时候用”和中文触发词。只能和服务端草稿一起上线](entries/2026-10-14-search-first-draft.md)
- [Review round 1 fixes for the 1.1.10 draft (still draft, not published): sample-answer order with one dates-and-party question and a closing statement, rate lookups only on the traveller's own dates, children/month/priority wording, search-first scope; correction of the earlier 12/12 second-turn claim](entries/2026-10-14-search-first-draft.md#review-round-1-and-fixes--2026-10-15-still-a-draft-not-pushed-not-published)
- [Review round 2 for the 1.1.10 draft (still draft, not published): correction of the round-1 hand-check claim; sample sentence before any itinerary, ask only what is missing, no destination question, no-prices case; stricter re-test 23/24 sample-first, 0/24 booking questions, 0/24 sample-date rate lookups](entries/2026-10-14-search-first-draft.md#review-round-2-and-fixes--2026-10-15-still-a-draft-not-pushed-not-published)
- [Review round 3 for the 1.1.10 draft (record only): round-2 scores restated as automated-check passes (10/12 with the skill, 10/12 server only) with the known ordering deviations listed; no further wording change](entries/2026-10-14-search-first-draft.md#review-round-3--2026-10-15-still-a-draft-not-pushed-not-published)
- [1.1.10 publication receipt: merged as e625609 and pushed to GitHub main; matching service release live 2026-10-15 03:10 UTC; shipped before the ChatGPT app review finished (held update there); Claude directory publication to be confirmed by the owner](entries/2026-10-14-search-first-draft.md#publication-receipt--2026-10-15-032x-utc-2026-10-14-pdt)

## 2026-10-16 洛杉矶

- [Skill/README 1.1.11: Marriott Bonvoy member rates now come back at some Marriott hotels (about 2% under the public rate where measured), marked members-only; the assistant searches again with the traveller's number like at Hilton/Hyatt/IHG/I Prefer; "not available through this connection" removed. Local commit, not pushed, not published; ships with booking-service record 2026-10-16-marriott-y47](entries/2026-10-16-marriott-member-rates.md)
- 推送回执：`540b9ca` 已于 2026-10-16 推送到 GitHub main（1.1.11），ls-remote 一致；对应服务 8f0f717 已于 04:16Z 上线。
- [README：ChatGPT 插件 2026-10-26 已上架，开头与 Connect 一节直接指向插件页；说明 ChatGPT 带同一套实时酒店工具、Skills 只给 Claude；开发者模式自建连接器改为备选；插件包与版本不变](entries/2026-10-26-chatgpt-plugin-published.md)
- [ChatGPT plugin package 1.1.11 draft built from the published 1.1.8 ZIP: skill = repo 1.1.11 with the one client-neutral line, version and release notes; uploaded as draft, not yet submitted](entries/2026-10-26-chatgpt-package-1-1-11.md)
- [ChatGPT package 1.1.11: submitted for review on the owner's go-ahead and approved the same day; Ready to publish, publication left to the owner](entries/2026-10-26-chatgpt-package-1-1-11.md)

## 2026-10-27 (Los Angeles)

- [Skill/README 1.1.12: the "may charge the card at booking" line comes from the rate's live terms and is passed on before sharing a link (deposit/non-refundable flags not needed); after booking, `my_trips`/`my_trip` are checked only for what they return and the total and cancellation terms are the ones accepted on the payment page; README says the ChatGPT plugin bundles the same Skill; next ChatGPT package prepared, not built or uploaded. Local commit, not pushed; ships with booking-service record 2026-10-27-review-fix-g6-tool-text](entries/2026-10-27-live-terms-wording-1-1-12.md)
- 2026-10-27 release receipt: `881f5e9` pushed to main (1.1.12); see [2026-10-27-live-terms-wording-1-1-12](entries/2026-10-27-live-terms-wording-1-1-12.md).
