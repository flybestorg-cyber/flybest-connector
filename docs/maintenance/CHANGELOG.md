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
