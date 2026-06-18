---
name: investment-research
description:
  投研分析技能套件：业绩快评、可比分析、晨会纪要、深度报告、研报摘要、行业研究、年报阅读、调研纪要。
  业绩快评: 业绩快评, 业绩点评, 财报速评, 季报分析; 可比分析: 可比分析, 可比公司, PE对比, comps; 晨会纪要: 晨会纪要, 晨会, 早盘观点, morning brief; 深度报告: 深度报告, 首次覆盖, 公司深度; 研报摘要: 研报摘要, 卖方研报, 观点提炼; 行业研究: 行业研究, 产业链, 行业格局; 年报阅读: 年报阅读, 年报分析, 10-K; 调研纪要: 调研纪要, 实地调研, 专家访谈。
version: "1.0.1"
author: "智慧半岛"
---

# investment-research -- 投研分析综合技能

本技能是一个综合技能套件，包含多个子技能。接到用户请求后，按以下流程执行。

## 执行流程

### Step 1: 意图识别与路由匹配

分析用户输入，与下方路由表逐一比对。匹配规则：
- 用户输入中包含路由表中「子技能」列的关键词 → 匹配该子技能
- 用户输入中包含路由表中「功能说明」列中提到的场景 → 匹配该子技能
- 多个子技能同时匹配时，选择匹配度最高的
- 无法唯一确定时，向用户确认意图

### Step 2: 加载子技能模板

匹配到子技能后，根据子技能索引表找到对应的文件路径，**必须**使用 `read_text` 工具读取 `references/` 目录下的完整执行模板。

### Step 3: 按模板执行

严格按照加载的模板逐步执行。模板中定义了：
- 输入要求（用户需要提供什么）
- 执行步骤（每一步做什么、如何判断）
- 输出格式（最终产出的结构和规范）
- 质量标准（产出必须满足的底线）

### Step 4: 输出结果

按模板规定的格式输出结果。如果模板要求生成文件，写入后声明产出物。

## 约束规则

1. **必须先读模板再执行**：匹配到子技能后，严禁凭记忆或猜测执行，必须先读取对应的 references 文件
2. **严格遵循模板**：不得跳过步骤、不得省略检查项、不得自行简化流程
3. **输入不足时主动索取**：模板中标注「必填」的输入项缺失时，向用户索取
4. **质量底线不妥协**：模板中的质量标准必须逐条满足

## 路由表

| 子技能 | 功能说明 |
|--------|----------|
| 业绩快评 | 上传业绩公告、业绩快报或业绩预告 → 快速生成业绩点评报告... |
| 可比公司分析 | 输入标的公司 → 筛选可比公司并构建估值指标矩阵，输出估值区间和隐含股价。 |
| 晨会纪要 | 输入覆盖范围或素材 → 生成晨会汇报材料... |
| 深度报告 | 输入公司名称和材料 → 撰写券商体例的公司深度研究报告... |
| 研报摘要 | 上传1-10份券商研报PDF → 提取核心观点、盈利预测和评级... |
| 行业研究 | 输入行业名称 → 撰写行业全景研究报告，覆盖市场空间、产业链、竞争格局和投资机会... |
| 读年报 | 上传A股年报PDF → 提取核心财务数据、经营分析和风险提示... |
| 调研纪要 | 上传调研笔记或录音转写 → 整理为标准化调研纪要... |

## 子技能索引

| 子技能 | 英文标识 | 文件 |
|--------|----------|------|
| 业绩快评 | `earnings-review` | [references/earnings-review.md](./references/earnings-review.md) |
| 可比公司分析 | `comparable-analysis` | [references/comparable-analysis.md](./references/comparable-analysis.md) |
| 晨会纪要 | `morning-briefing` | [references/morning-briefing.md](./references/morning-briefing.md) |
| 深度报告 | `deep-dive-report` | [references/deep-dive-report.md](./references/deep-dive-report.md) |
| 研报摘要 | `research-digest` | [references/research-digest.md](./references/research-digest.md) |
| 行业研究 | `industry-research` | [references/industry-research.md](./references/industry-research.md) |
| 读年报 | `annual-report-reader` | [references/annual-report-reader.md](./references/annual-report-reader.md) |
| 调研纪要 | `field-research-notes` | [references/field-research-notes.md](./references/field-research-notes.md) |
## 跨技能协同指引

| 协同技能 | 典型场景 |
|---------|---------|
| 股权投资 | 深度研究报告可作为投资决策备忘录的输入 |
| 财富管理 | 行业研究数据可驱动基金分析和资产配置建议 |

> 以上为推荐协同路径。执行复合任务时，请根据实际需求灵活组合。

## 变更日志

### v1.0.1 (2026-06-19)
- 对齐 description 子技能名与路由表名称
- 压缩路由表说明列至40字以内
- 新增跨技能协同指引章节
- 删除冗余英文 description 行