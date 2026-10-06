# 2026-10-05 MCP Registry：补充公开 repository 与可维护的发布清单

- 记录 ID：2026-10-05-mcp-registry-repository
- 日期与时区：2026-10-05，America/Los_Angeles
- 关联记录：已查阅 [维护规范](2026-10-02-maintenance-policy.md)、[公开插件基线](2026-10-02-release-baseline.md)、[公开文档与工具契约](2026-10-04-public-docs-live-contract.md)。
- 影响：本公开仓库的 README、根目录 server.json 和官方 MCP Registry 的 `org.flybest/travel-hotels` 元数据。

## 问题与根因

GitHub MCP Registry 审核要求官方 MCP Registry 条目包含公开 repository URL，其自动化从 server.json 读取仓库并使用 README 展示功能、配置和使用方式。

核对官方 API：当前 1.0.1 条目 active，但没有 repository 字段。公开仓库 flybestorg-cyber/flybest-connector 已存在并可匿名读取，其 README 已说明酒店功能、OAuth 连接方式和预订/取消流程；此前根目录没有纳入版本管理的 Registry server.json。

## 修改方法与原因

- 将正式发布清单保存到本仓库根目录 server.json，补充 `repository.url=https://github.com/flybestorg-cyber/flybest-connector`、`repository.source=github`。
- 发布清单版本提升为 1.0.2，保留原服务器名称、描述、标题、网站和 Streamable HTTP 地址；以新的登记版本更新元数据。
- README 新增 Registry 入口，明确本仓库承载托管服务的文档、登记清单和客户端插件，并集中说明 Streamable HTTP、OAuth、邮箱验证码及使用示例入口。
- Registry 的 1.0.2 与 Claude 插件的 1.1.5 是各自的版本；本次没有改动插件运行配置或 skill，因此不改插件版本。

## 用户体验与兼容性

现有连接地址、OAuth 登录、8 个公开酒店工具及预订/取消的确认要求保持原有行为。本次让 Registry 审核与发现能够正确关联公开文档，不涉及后端代码、权限、付款流程或服务重启。

## 验证

- 已通过匿名 GitHub API 核对目标仓库 `private=false`、默认分支 main。
- 已对照官方 Registry 1.0.1 内容，新增清单只修改版本和 repository。
- README 中的功能、配置和使用示例均有明确章节；新增相对链接指向仓库文件或既有章节。
- 发布前执行 schema/Registry 校验，发布后回读官方 latest 条目与匿名 GitHub 文件；实际结果在下方追加。不为纯文档和元数据修改执行真实订房、付款或取消。

## 版本与发布状态

- Git 基线：5cfa5e6ab9213c75f9e7f911efff31d7e3cf0321；本次提交见本记录所属 Git 提交。
- 本记录初次写入时为待提交、待推送、待发布的 1.0.2 清单，官方 latest 仍为 1.0.1；完成后追加证据。
- 服务端运行版本不适用，本仓库为公开连接文档和配置；本次无服务部署或重启。

## 剩余边界与后续事项

官方 Registry 发布成功不代表 GitHub 目录已重新审核或收录。完成后可把公开仓库、清单和官方条目链接回复审核团队，由其重新运行审核。回信是独立动作，本次修改不自动发送邮件。
