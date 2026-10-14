# 2026-10-14 README 增加“Updating”（如何收到新版本）

- 记录 ID：2026-10-14-readme-updating
- 日期与时区：2026-10-14，洛杉矶
- 关联旧记录或修复：2026-10-11-loyalty-wording（1.1.8 安装说明）、2026-10-13-plugin-install-link（安装链接）；sabre-booking 同日记录 2026-10-14-docs-air-team-owner-plugin
- 影响仓库、文件和用户入口：只有 `README.md`（新增 `## Updating` 一节，安装一节的一句加了指向它的链接）。插件包、Skill、清单版本（仍为 1.1.8）与 MCP 工具都不变。
- 篇幅：短记录。

## 问题与根因

README 只说“已安装的需要更新插件才能拿到新的 Skill 说明”，没说怎么更新。Claude 目录里装的会在新版本发布后自动更新；但从本仓库 GitHub marketplace 装进 Claude Code 的，自己添加的 marketplace 默认不自动更新，用户会一直停在旧的 Skill 文本上而不自知。

## 修改方法与原因

在 “Install in Claude Code” 之后新增 “Updating”：

- Claude 网页与桌面（目录安装）：无需操作，新版本发布到目录后自动更新。
- Claude Code（从本仓库 marketplace 安装）：一次性打开自动更新（`/plugin` → Marketplaces → `flybest` → Enable auto-update），或手动 `claude plugin marketplace update flybest` 再 `claude plugin update flybest-hotels@flybest`，然后在会话里 `/reload-plugins`（或重启 Claude Code）。
- 只连工具的客户端（`claude mcp add`、自定义连接器、ChatGPT）：工具与服务器说明来自服务器，无需安装；客户端缓存了工具定义时刷新或重连。

Skill 与参考文件逐句复查过：本轮服务器变更（机票规则查询要求 fare basis、酒店 rate key 过期时只有全部条款相同才自动重查否则拒绝、参数按 schema 在发送前校验）对公开 Skill 没有需要改的句子——公开档没有机票工具；“价格变了是新决定、按页面重新同意”和“发送前被拒就按提示改参数”两条已覆盖后两项；城市搜索的“起价仅供发现、正式报价来自 rate 查询”保持不变。所以不改 Skill、不升版本。

## 用户体验与兼容性

只是说明文字。已安装的插件、连接和订单不受影响。

## 验证

- `claude plugin --help` / `claude plugin marketplace --help` / `claude plugin update --help`（Claude Code 2.1.293）核对了命令名与参数：`marketplace update [name]`、`update <plugin>`（帮助写明更新后需重启/重载才生效）。
- `git diff` 只涉及 README 与本条记录、CHANGELOG；清单版本仍为 1.1.8。

## 版本与发布状态

- 相关提交：见本条记录的 Git 提交，分支 `docs-2026-10-14`。
- GitHub 推送状态：本地提交，未推送（由协调者合并到 main 后推送）。
- 纯文档，无服务器运行时变化；目录版本不需要重新发布。

## 剩余边界与后续事项

`/plugin` 界面里“Enable auto-update”的菜单位置按 Jay 给出的路径写，未在交互界面里逐级点过；界面改版时以 Claude 的插件文档为准。
