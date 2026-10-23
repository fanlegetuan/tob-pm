---
name: tob-pm
description: >-
  Use when doing B2B/toB software product management: PRD, requirements,
  prioritization, stakeholder maps, discovery, roadmap, eng handoff for
  enterprise SaaS. Triggers: tob-pm, toB产品经理, B2B PM, PRD, 需求评审, 产品路线图, 企业软件产品,
  验收标准.
---
# tob-pm

企业 SaaS / 定制软件的 toB 产品工作流：需求→PRD→范围裁剪→优先级→交接。输出必须可执行、可验收；禁止软化空话。

## Inputs

| Input | Required | If missing |
| --- | --- | --- |
| 问题/目标（业务结果 + 谁痛） | Yes | 🔴 STOP — 先问清「谁、什么场景、要什么可度量结果」；不编造 |
| 干系人线索（买方/Champion/终端用户/IT安全/采购） | Preferred | 跑步骤2补全；缺买方或安全 → Warning 标在 PRD 顶栏 |
| 约束（合规/SSO/权限/审计/集成/SLA/合同期限） | Preferred | 步骤3强制填「未知」行；未知 ≠ 不做 |
| 竞品/现有方案 | Optional | 步骤5写「未调研」+ 列须补的3个问题 |
| 工程容量（人周/窗口） | Preferred | RICE 的 Effort 用相对档（S/M/L/XL）并写假设 |

## Workflow

### 1 需求入口 → 结构化问题
- **In:** 原始诉求（邮件/工单/销售口述）
- **Out:** 一页问题卡（见模板 A）；每条诉求映射到「用户/场景/结果/证据」
- 规则：同一诉求出现 ≥2 个冲突目标 → 拆成独立条目，禁止合并成模糊一句

🔴 **CHECKPOINT:** 问题卡缺「可度量结果」或「证据来源」→ 停；回问后再写 PRD。

### 2 干系人地图
- **In:** 问题卡 + 组织线索
- **Out:** 表：角色 | 姓名/岗位 | 决策权(决定/否决/影响/使用) | 成功标准 | 风险
- 必覆盖五类：Buyer、Champion、End-user、IT/Security、Procurement（缺一类写「待确认」+ 联系动作）
- 冲突：Buyer 要速度、Security 要管控 → 记入决策日志，不静默偏向任一方

### 3 范围与 MVP（toB 硬约束）
- **In:** 问题卡 + 干系人表 + 约束清单
- **Out:** Must / Should / Could / Won't + 合规清单勾选
- 合规清单（每项：In-MVP / Post-MVP / N/A + 理由一句）：SSO/SAML、RBAC、审计日志、数据驻留、加密传输与静态、第三方集成、SLA/可用性、导出/删除（GDPR类）
- MVP 裁剪规则：砍掉不影响「首单可签/可上线验收」的项；合规 Must 不可因「以后再做」进 Won't

🛑 **STOP before 锁定 MVP：** 任一合规 Must 未裁决，或 Buyer 与 Security 对同一 Must 仍冲突 → 不输出最终范围。

### 4 优先级（RICE，强制打分步骤）
- **In:** 候选需求列表（每条一句话 + 受益角色）
- **Out:** 排序表：ID | Reach | Impact | Confidence | Effort | RICE | 结论(做/缓/砍)
- 打分（整数，禁止「大概」）：
  - Reach：90天内触及的账号数或席位（写假设来源）
  - Impact：0.25 / 0.5 / 1 / 2 / 3（对应微小/低/中/高/巨大，相对同一基线）
  - Confidence：50% / 80% / 100%（有访谈/数据=100；仅销售口述=50）
  - Effort：人周（工程+设计；未知用档位中值 S=1 M=3 L=6 XL=12）
  - RICE = Reach × Impact × Confidence / Effort
- 同分：优先解锁收入/续约/合规阻塞项

🔴 **CHECKPOINT:** 输出路线图前必须展示 RICE 表并获确认（或任务已授权跳过确认）。

### 5 竞品 / 市场简报（企业成交向）
- **In:** 目标功能 + 已知对手
- **Out:** 半页简报：对手能力对比（有/无/部分）| 我方差异 | 采购异议与反驳一句 | 需补证据
- 最少对比 2 个具名对手；不知名则列「替代方案：手工/Excel/现有模块」

### 6 交接 eng/design（DoD）
- **In:** 锁定的 MVP + 用户故事
- **Out:** 交接包：故事列表 + AC + 非功能 + 开放问题 + DoD 勾选
- DoD（全部勾上才算可排期）：AC 可测、权限矩阵有表、错误态列出、审计事件名列出、集成契约（API/事件）有草案、验收负责人写名

🛑 **STOP before 「可开发」声明：** DoD 任一项未勾 → 状态保持「草稿」，禁止写「已就绪」。

### 7 发现访谈脚本与综合
- **In:** 待验证假设（最多5条）
- **Out:** 脚本（开场60s + 5个主问 + 2个追问）+ 综合：洞察 | 证据原话 | 对范围的影响(保/改/砍)
- 主问必须问行为与最近一次实例，禁止只问「你觉得要不要」

### 8 决策日志与失败回退
- **In:** 步骤3–6 的待裁/待排决议
- **Out:** 决策日志（模板 D）≥1 行；若命中失败表则执行对应「First fix」
- 每个范围/优先级/裁剪决策写一行：日期 | 决策 | 选项 | 选择原因 | 回退条件
- 发布对外口径前对照决策日志；不一致 → 🛑 STOP

## Failure modes（trigger → first fix → still fails）

| Trigger | First fix | Still fails → |
| --- | --- | --- |
| 诉求只有功能名无结果 | 回问可度量结果 + 谁验收 | 🔴 STOP；不写 PRD |
| 五类干系人缺 ≥2 | 列待确认名单 + 负责人 | Warning 顶栏；MVP 标「未验证」 |
| Buyer↔Security 冲突 | 决策日志双选项 + 升级 Sponsor | 🛑 STOP 锁定范围 |
| 合规 Must 被塞进 Won't | 移回 Must 或改 N/A 并写法务依据 | 🛑 Block 交接 |
| RICE 缺 Effort/Confidence | 用档位中值并标注假设 | 不进路线图；只出草稿序 |
| 无竞品名 | 用替代方案对比 + 3个调研问 | 简报标「证据不足」 |
| AC 不可测（含「体验好」） | 改写成 Given/When/Then 或数值阈值 | 故事保持草稿 |
| 访谈只收集愿望清单 | 重问最近一次工作流 | 洞察标低置信；Confidence≤50% |
| 销售承诺未进范围 | 决策日志：承诺→Must/Won't + 谁签字 | 对外口径与 PRD 不一致 → 🛑 STOP 发布 |
| 工程容量未知仍承诺日期 | 只给相对序；日期改「待估」 | 禁止写死上线日 |

## Anti-patterns（do not）

- 用「建议/可以考虑/根据情况/灵活把握/视情况而定」代替裁决
- 无证据把销售口述写成 Confidence 100%
- 把 SSO/审计/权限一律丢到「二期」且无 Sponsor 签字
- PRD 只有功能列表、无 AC / 无非功能
- 干系人表只有姓名、无决策权与成功标准
- RICE 只写总分、不披露 Reach/Impact/Confidence/Effort
- 交接包缺权限矩阵或审计事件仍称「可开发」
- 访谈只问偏好、不问最近一次实例
- 静默吞掉 Buyer/Security 冲突
- 发明未确认的客户名、合同条款、合规结论

## Output templates

### A 问题卡
```
标题：
谁（角色）：
场景（触发→步骤→痛点）：
可度量结果（指标+基线+目标）：
证据（工单/访谈/数据链接）：
非目标：
```

### B 用户故事 + AC
```
作为 <角色>，我想 <能力>，以便 <结果>。
AC:
- Given … When … Then …
- 权限：角色 X 可/不可 …
- 审计：事件 <name> 记录 <字段>
非功能：可用性/延迟/保留期 =
开放问题：
```

权限矩阵示例（交接必附）：

| 动作 | 管理员 | 审批人 | 提交人 | 只读访客 |
| --- | --- | --- | --- | --- |
| 配置审批流 | ✓ | — | — | — |
| 通过/驳回 | — | ✓（队列内） | — | — |
| 提交/撤回己单 | — | — | ✓ | — |
| 查看审计 | ✓ | — | — | — |

输出句式示例（可直接贴进 PRD）：
- `Must：SSO/SAML 登录；RBAC 三角色；审计 event=approval.*`
- `RICE：Reach=120席(CRM) × Impact=2 × Conf=80% / Effort=4人周 = 48 → 缓`
- `🛑 STOP：Security 未签数据边界前不声明可开发`

### C PRD 大纲（顺序固定）
1. 背景与问题卡摘要  2. 目标/非目标  3. 干系人地图
4. 方案与 MVP（MoSCoW+合规勾选）  5. 故事与 AC  6. 非功能与集成
7. RICE/路线  8. 竞品简报  9. 开放问题  10. 决策日志  11. DoD

### D 决策日志行
`YYYY-MM-DD | <决策> | 选项A/B | 选<A>因为… | 回退若…`

## Resources

| Path | Role |
| --- | --- |
| This `SKILL.md` | Sole required recipe |
| `test-prompts.json`（同目录） | Darwin / 回归提示 |

无额外 scripts。勿发明外部路径。

## 按任务类型的最小交付物

| 用户任务 | 必须输出 |
| --- | --- |
| 写 PRD / 需求评审 | 模板 C 全节；缺节标「待补」不得删节 |
| 范围裁剪 / 冲突 | MoSCoW + 决策日志 + 对外口径；冲突未解则 🛑 |
| 排期 / 优先级 | RICE 全表 + CHECKPOINT；禁止只给名次 |
| 发现访谈 | 脚本 + 综合表（洞察/原话/对范围影响） |
| 交接 eng/design | 故事+AC+权限矩阵+DoD；DoD 未满 = 草稿 |

## Self-check before send
1. 无软化空话；每项范围有 Must/Should/Could/Won't 或明确未知
2. 合规清单每项有 In-MVP / Post-MVP / N/A
3. RICE 四因子齐全；AC 可测
4. 命中 🛑/🔴 条件则未伪称「已锁定/可开发」
5. 反模式表对照无命中
6. 上表「必须输出」齐全；缺项在文首列出
