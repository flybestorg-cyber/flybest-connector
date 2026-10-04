# 2026-10-04 公开文档对齐线上公开工具契约（插件 1.1.5）

- 记录 ID：2026-10-04-public-docs-live-contract
- 日期与时区：2026-10-04，洛杉矶
- 关联旧记录或修复：[公开酒店插件 1.1.4 基线](2026-10-02-release-baseline.md)、[建立持续维护记录](2026-10-02-maintenance-policy.md)
- 影响仓库、文件和用户入口：本仓库 `README.md`、`skills/flybest-hotels/SKILL.md`、`.claude-plugin/plugin.json`、`lhm.plugin.json`。用户入口是 GitHub 上的 README、Claude Code 插件里的 skill，以及被用户粘贴到 ChatGPT 等客户端的 `SKILL.md`。服务端没有改动。

参考记录：`AGENTS.md`、`CLAUDE.md`、`CONTRIBUTING.md`、维护索引、修改日志和上面两条 2026-10-02 记录。核对对象是线上公开连接的工具列表和初始化 instructions，以及服务端公开工具实现（只读）。

## 问题与根因

以下都是文档与线上行为不一致，不涉及预订、付款或取消的执行路径。

1. **四季 Preferred Partner**
   - 现象：README 把四季 Preferred Partner 放进"助手会把这些礼遇显示在价格旁边"的 programme 列表。SKILL §2 也把它列为"随 `with_perks` 返回礼遇"的 programme。
   - 核实结果：本连接实际查询的 programme 里没有四季 Preferred Partner。在四季酒店，本连接只会返回其他 programme 的合作价。
   - 根因：列表照"代理持有哪些 programme"来写，而不是照"本连接实际查询哪些 programme"来写，之后也没有和后端清单核对过。
   - 后果：助手可能把四季酒店的其他合作价说成四季 Preferred Partner 价，可两者的礼遇并不相同。

2. **Virtuoso 固定句**
   - 现象：README 写成 "Rates include **Virtuoso** …"，漏了 "may"，还把品牌名加粗。这与已批准的原句、服务端 instructions、使用条款和 SKILL 都不一致。
   - 根因：2026-09-28 加入这句时转写有偏差，之后一直没有逐字核对。

3. **SKILL 和 README 描述了公开连接并不存在的行为**
   - a. SKILL §1 说 `sabre_hotel_rates_coded` 不传 `hotel_name` / `chain_code` 时"不会失败，只是悄悄返回公开价"。实际情况：
     - 公开 schema 把这两个参数列为必填。
     - 主机会在发出任何请求之前拒绝缺参的调用（"Refused before anything was sent … Nothing was called"）。
     - 就算没有这道闸门，后端返回的也不只是公开价。
     - 根因：这句话沿用了更早的运营说明，而必填闸门在此之前就已经上线。
   - b. SKILL §7 要助手读 `ok` / `changed` / `reason` 字段。可 8 个公开工具都只返回文字句子，根本没有这些字段；部分失败（参数拒绝、额度、内部错误等）带 `isError`，取消的拒绝句不一定带。
   - c. SKILL §4 要助手找标记为 `direct_family_bookable` 的行，并查看 `family_occupancy`。公开输出不打印这两个字段名，能看到的是：
     - "Family occupancy verified for this rate — direct family booking available."
     - "Requested family for this rate: …"
     - `family_quote_token=` 行，只出现在已核实的行上
   - d. README 的家庭示例说"搜索用到四位客人和孩子年龄"。实际上城市搜索 `sabre_hotel_search` 没有儿童和年龄参数，返回的价格只是临时价。用到孩子年龄的是单个酒店的房价查询。
   - e. README 说 `claude plugin validate` 从 2.1.281 起没有警告。2026-10-02 根目录加入维护用的 `CLAUDE.md` 之后，2.1.284 会报一条警告。

## 修改方法与原因

**README**
- Virtuoso 句换成已批准的原句：不加粗，保留 "may"。句子上方加一段不会渲染的 HTML 注释，提醒逐字保留，并链接本记录。
- 把四季 Preferred Partner 移出"本连接会展示"的列表，另写一句说明：
  - 代理持有这个 programme，但本连接拿不到它的房价；
  - 四季酒店显示的合作价来自其他 programme，礼遇按那个 programme；
  - 四季 Preferred Partner 的预订由顾问直接安排。

  写法参照 README 里已有的 Marriott 会员价说明：既保留真实资历，也不暗示能经本连接拿到。
- 家庭示例改为：城市搜索价格是临时价；之后按四位客人和孩子年龄查询所选酒店的房价。
- 更新 validate 版本说明。

**SKILL**
- §1：写明两个参数都必填，缺参会在发送前被拒，而且必须从该酒店的搜索结果行复制。用户直接说出酒店名时，先搜索所在城市。
- §2：从 `with_perks` 的 programme 列表里删去四季 Preferred Partner，并新增一条：
  - 四季 Preferred Partner 不能经本连接取得；
  - 四季酒店的其他合作价按其自身房价文字介绍礼遇，不要称为四季 Preferred Partner 价；
  - 客人问起时，说明由顾问直接安排。
- §4：改为引用公开输出中实际可见的句子和 `family_quote_token=` 行，同时注明工具描述里用的名称（`direct_family_bookable` / `family_occupancy`），方便与服务端说明对上。
- §5：补充一点：创建付款页时，传入与报价相同的 `rooms` 和每间 `adults`，保证付款页的人数与报价一致。
- §7：改为按文字句子和 `isError` 判断结果，分四类：发送前被拒（改参数后重调）、明确拒绝（"Nothing was cancelled." 等，照所述下一步处理）、结果未知（查 `my_trip`、找顾问，不要再次发送）、确已完成（"Cancelled: …"，或 `my_trips` 里出现确认号）。"转述拒绝原因"一条保留。

**版本**
- skill 是用户可见文本，所以插件版本从 1.1.4 升到 1.1.5（`plugin.json`、`lhm.plugin.json`）。
- `marketplace.json` 从来不带版本号，以 `plugin.json` 为准，这次也不新增。

**保持不变**
- 公开连接仍是 8 个酒店工具。
- 佣金说明不变：酒店向 FlyBest 支付佣金，客人只付酒店自己的房价、没有订房费，不提金额或比例。
- 已批准的 Virtuoso 原句本身不变，本次只是把 README 里的转写改回原句。
- 家庭 `direct` / `adult_pending` 规则不变。
- 取消仍是两步，含 `accept_penalty`。
- Run of House 不承诺 King。
- SKILL 里"网上查找 Virtuoso 礼遇时忽略四季 Preferred Partner 等其他 programme 条款"这一句保留，它本身是对的。

## 用户体验与兼容性

- 客人不会再被告知能经本连接拿到四季 Preferred Partner，想要的话会拿到顾问的联系方式。
- 助手对缺参、拒绝、结果未知的解读与真实返回一致。家庭预订按可见的已核实标记来选行。
- 价格、罚金、房型和人数的展示以及重新同意流程都没有变。旧链接、已授权的连接和已有订单不受影响。
- 已安装 1.1.4 的 Claude Code 用户要更新插件才能拿到新 skill。只填连接器 URL 的客户端不受本仓库变更影响，它们只收到服务端的 instructions。
- 服务端的初始化 instructions 和 `sabre_hotel_rates_coded` 的公开描述里仍有两处旧说法：一是缺参时"悄悄返回公开价"，二是用字段名描述家庭标记。这两处在服务端仓库，需要在那边修正并部署。在那之前，第 1 点上插件 skill 与服务端 instructions 说法不同，以本 skill 为准，因为它与实际的必填闸门一致。

## 验证

- 本地静态核对脚本（未入库），结果全部通过：
  - README 含已批准的原句（去掉换行和注释后逐字比较）。
  - README 和 SKILL 里每处 "a Virtuoso member agency" 都属于已批准的原句。
  - 四季 Preferred Partner 每次出现都带限定："不经本连接""顾问直接安排"或"其他 programme 条款"。
  - SKILL 不再含 "silently returns public"、"does not fail"、`ok: false`、`changed: false`；README 不再含 "the search uses all four"。
  - 文档点名的工具恰好是全部 8 个公开工具，没有其他工具。
  - 文档提到的参数在线上公开 schema 中都存在。
  - 没有内部代码、路径或主机信息。
  - 两个 manifest 的版本都是 1.1.5，`marketplace.json` 没有冲突的版本号，端点没有变。
  - 佣金句保留，没有百分比。
- SKILL 引用的 14 个结果短语，逐一在服务端公开工具实现中找到了原文。
- `claude plugin validate`（2.1.284）：marketplace 清单通过；插件清单通过，但带一条既有警告（根目录 `CLAUDE.md` 不会作为插件上下文加载）。在未修改的 HEAD 导出副本上同样有这条警告，删掉 `CLAUDE.md` 后警告消失，说明与本次修改无关。
- 这是纯文档修改，没有运行真实的搜索、预订、付款、取消或发信。

## 版本与发布状态

- 相关代码提交或 PR：见本条记录的 Git 提交。
- GitHub 推送状态：本地提交，未推送，未部署（由编排者合并发布后补充）。
- 服务器实际运行版本和核验时间：不适用。本仓库没有服务端代码，服务端也没有改动。
- 是否重启或只同步文档：不需要重启。
- 后续补充：按日期追加。

## 剩余边界与后续事项

- 服务端的两处旧说法（见"用户体验与兼容性"）需要在服务端仓库修正，并同步到 MCP 主机。修正后应与本 skill 第 1 点和第 4 点一致。
- 服务端如果改写 `cancel_my_trip` 等工具的返回句子（例如改成陈述句，或给更多分支加 `isError`），需要复核 SKILL §7 引用的示例短语。§7 已写明以句子含义为准、不论带不带 `isError`。
- 本连接查询的 programme 清单一旦增减，就要复核 README 和 SKILL 里的 programme 列表。目前没有自动化的跨仓库检查。
- 服务端仓库有一条跨仓库测试，在找到连接器检出时会断言插件版本为 1.1.4，需要同步改成 1.1.5。
- 回退方法：还原本提交即可。没有运行时状态需要处理。
