# 2026-10-13 Claude 插件安装链接改为公开安装页

- 记录 ID：2026-10-13-plugin-install-link
- 日期与时区：2026-10-13，洛杉矶
- 关联旧记录或修复：2026-10-11-loyalty-wording（1.1.8 安装说明）；sabre-booking 2026-10-08-plugin-promotion 与 2026-10-13-plugin-install-link（官网同日修复）
- 影响仓库、文件和用户入口：`README.md` 的三处安装链接；插件包、Skill、MCP 工具不变
- 篇幅：短记录。

## 问题与根因

README 的安装链接是 `claude.ai/directory/manage/plugins/<id>`，这是插件发布者自己的目录管理页，其他用户打不开。Jay 2026-10-13 给出公开安装页 `https://claude.ai/customize/plugins/id/4c82105c-3ebc-4a9b-b2c4-9916f9566836%40anthropic-plugin-directory`。

## 修改方法与原因

三处链接（顶部安装说明、Claude 安装步骤、目录条目一句）只换 URL，文字和“需要登录”说明保留。

## 用户体验与兼容性

读者点链接直接进 Claude 的插件安装页。已安装的插件、连接和订单不受影响。

## 验证

`git diff` 只有三处 URL 替换；仓库内不再有 `directory/manage/plugins` 链接。

## 版本与发布状态

- 相关代码提交：见本条记录的 Git 提交；GitHub 推送状态见 CHANGELOG 下一行。
- 纯文档，无服务器运行时变化。

## 剩余边界与后续事项

未用一个未登录或非发布者账号实际点开验证安装页，链接以 Jay 给出的地址为准。
