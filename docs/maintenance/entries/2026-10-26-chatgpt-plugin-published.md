# 2026-10-26 README：ChatGPT 插件已上架，改为直接指向插件页

- 记录 ID：2026-10-26-chatgpt-plugin-published
- 日期与时区：2026-10-26 美西（PDT）
- 关联旧记录或修复：[2026-10-14 README 更新说明](2026-10-14-readme-updating.md)；[2026-10-14 先搜再问草稿](2026-10-14-search-first-draft.md)（当时 ChatGPT 插件在审核中）。
- 影响仓库、文件和用户入口：`README.md`（开头安装段、Connect → ChatGPT、Updating）。不改插件包、Skill 或版本号（仍为 1.1.11）。

## 问题与根因
FlyBest 的 ChatGPT 插件于 2026-10-26 通过 OpenAI 审核并发布。README 仍把 ChatGPT 写成「开发者模式自建连接器、实验性、未做端到端测试」，读者找不到已上架的插件。

## 修改方法与原因
- 开头在「Install in Claude」后加「Use in ChatGPT」，链接 ChatGPT 插件页。
- Connect 一节的 ChatGPT 改为：先用已发布的插件，同一个邮箱验证码登录；说明 ChatGPT 插件带同一套实时酒店工具和服务器说明，本仓库的 Skills 是给 Claude 的；手机 App 未经 FlyBest 核实；开发者模式自建连接器作为工作区的备选，保留 OpenAI 说明链接。
- Updating 一节把 ChatGPT 插件归入「工具和说明来自服务器、无需安装」那一类。

## 用户体验与兼容性
只改说明文字。已用开发者模式连上的用户不受影响。

## 验证
渲染前人工通读三处改动；链接为插件所有者提供的 ChatGPT 插件页地址，其中的 ID 与 OpenAI 后台插件 ID 一致（服务器抓取该页面会被人机验证挡住，内容由所有者在浏览器确认）。

## 版本与发布状态
- 相关代码提交或 PR：见本条记录的 Git 提交。
- GitHub 推送状态：`ebee226` 已于 2026-10-26 推送到 GitHub main，ls-remote 一致。
- 网站同步：flybest.org 同日加上同一链接（服务端仓库记录 2026-10-26-chatgpt-plugin-link）。

## 剩余边界与后续事项
没有运行时变更。ChatGPT 插件在 ChatGPT 目录里能否被搜到、未登录能否打开，待所有者确认。
