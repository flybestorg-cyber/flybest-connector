# 2026-11-18 README：写明经营者、所属旅行社和「关于」页

- 记录 ID：2026-11-18-readme-who-runs-it
- 日期与时区：2026-11-17 傍晚，America/Los_Angeles（UTC 已是 11-18）
- 关联旧记录或修复：`2026-10-04-public-docs-live-contract.md`（固定措辞那一句没有动）、`2026-11-11-directory-hold-wording-1-1-21.md`（合并前先跑门户的 Validate）
- 影响仓库、文件和用户入口：只有 `README.md`。不改技能、不改清单、不改版本号（仍是 1.1.21）。

## 问题与根因
用同样 8 个问题分别问了三家 AI 助手（联网、不装本插件）。问「有没有能查价订房的插件」时，Claude 找到了 FlyBest，但出处是第三方的 MCP 目录站，并注明「没有独立来源证实它和 Virtuoso 的关系」；问「FlyBest 是谁、可靠吗」时找不到答案。这些目录站的介绍取自本仓库的 README 和仓库简介。README 原来只在最后一节写「一位加州的独立顾问」，没有姓名、没有注册号，也没有可以核对的链接。

## 修改方法与原因
- 开头「Overview」一行后面加一行「Who runs it」：Jay Yan，Virtuoso 旅行顾问，Garden Grove，英语和普通话；预订经 Coastline Travel Advisors（Virtuoso 成员旅行社，CST 2040360-40，ARC 05582905）；链接到网站的「关于」页和 Virtuoso 顾问资料页。目录站通常只取开头几段，所以放在前面。
- 最后一节「Who runs this」第一段补上同样的事实和 Coastline 的地址，其余句子（谁负责数据、免费、佣金由酒店支付）原样保留。
- 这些事实都已在 flybest.org 的首页、条款页和「关于」页公开。
- 没有动「Rates may include Virtuoso hotel programme benefits…」那句固定措辞。

## 用户体验与兼容性
插件的行为、工具和登录方式都不变。只是读 README 或目录站介绍的人（和 AI）能看到经营者是谁、去哪里核对。

## 验证
- 全文检查没有出现规矩第 6 条禁用的那个动词。
- 合并前在分支 `docs/who-runs-this` 上跑开发者门户的 Validate，结果见下面「版本与发布状态」。

## 版本与发布状态
- 相关代码提交或 PR：见本条记录的 Git 提交。
- GitHub 推送状态：见后续补充。
- 服务器实际运行版本和核验时间：不适用，纯文档。
- 是否重启或只同步文档：只同步文档。
- 后续补充：

## 剩余边界与后续事项
`server.json` 里给 MCP 注册表的一句话简介没有改（改它要重新发布到注册表）。各目录站什么时候重新抓取不由我们控制。
