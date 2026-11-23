# 2026-11-23 目录不再接受 CLAUDE.md / AGENTS.md：维护规则改名为 MAINTAINING.md

- 记录 ID：2026-11-23-directory-allowed-files
- 日期与时区：2026-11-23，America/Los_Angeles
- 关联旧记录或修复：`2026-11-06-skill-essentials-1-1-18.md`（当时把维护用的 `CLAUDE.md` 从根目录挪到 `.claude/`）、`2026-11-11-directory-hold-wording-1-1-21.md`（合并前先跑门户的 Validate）、`2026-11-18-readme-who-runs-it.md`（被扣的那次提交）、`2026-10-02-maintenance-policy.md`（新增根目录 `AGENTS.md`）
- 影响仓库、文件和用户入口：`AGENTS.md` → `MAINTAINING.md`（多一条规矩第 7 条），删除 `.claude/CLAUDE.md`，`README.md`、`CONTRIBUTING.md`、`docs/maintenance/README.md` 里的链接跟着改。不改技能、不改清单、不改版本号（仍是 1.1.21）。

## 问题与根因
`8a824a7`（只改 README 的那次提交）被 Claude 目录定时检查拾取后，显示「Held by directory policy」，理由是两条：「Files the policy review couldn't cover」和「Policy review didn't complete」，页面不点名文件。

2026-11-23 在开发者门户对 `main @ 8a824a7` 跑 Validate，结果变成 1 条阻断：「Files outside the allowed list accepted only from Verified organizations」，点名 `.claude/CLAUDE.md`。说明文字写明：未认证（Community）组织的插件里，任何文件夹、任何大小写的 `CLAUDE.md`、`CLAUDE.local.md`、`AGENTS.md` 都要改名或移除。

同一个文件在 2026-11-17 的 Validate 里没有被报（7 项全过）。所以是目录的规则在这几天里收紧了，不是那次 README 改动引入的问题。已证实的是今天的阻断和它点名的文件；「五天前那两条理由就是因为这个文件」是推测，页面没有给出文件名。

## 修改方法与原因
- `AGENTS.md` 改名为 `MAINTAINING.md`，内容不变，只加第 7 条：目录对未认证组织接受哪些文件、哪些文件名不能出现、合并前清掉 Validate 的阻断项。
- 删除 `.claude/CLAUDE.md`。它只有两行引用，指向维护规则和维护索引，对安装插件的客人没有作用。
- 维护者自己的工作副本可以保留同名的指向文件给代码助手读，写进 `.git/info/exclude`，不提交。
- 没有采用「把插件挪进子目录、只提交子目录」：已上架的提交记录绑定的是仓库根目录，换路径要新建提交记录，已安装用户的市场地址也会变。

## 用户体验与兼容性
插件的技能、工具、清单都不变，已安装的用户不受影响。

## 验证
- 全文检查没有出现规矩第 6 条禁用的那个动词。
- 仓库里不再有名为 `CLAUDE.md`、`AGENTS.md` 的文件；剩下的文件只有 Markdown、JSON、LICENSE 和 `icon.png`。
- 合并前在分支 `fix/directory-allowed-files` 上跑开发者门户的 Validate，结果见下面「版本与发布状态」。

## 版本与发布状态
- 相关代码提交或 PR：见本条记录的 Git 提交。
- GitHub 推送状态：见后续补充。
- 服务器实际运行版本和核验时间：不适用，纯文档。
- 是否重启或只同步文档：只同步文档。
- 后续补充：

## 剩余边界与后续事项
- 插件整体仍是「held for review」：任何版本都要 Anthropic 的审核员放行才会上线，这次改动只是让最新一版不再带阻断项。
- 目录的定时检查约每 6 小时一次（页面显示 Claude GitHub App 未连接）。
