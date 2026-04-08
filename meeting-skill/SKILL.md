---
name: meeting-skill
description: |
  多Agent协作会议组织与管理框架。用于组织结构化的多agent会议流程，包括议程管理、角色分配、环节推进、纪要输出。

  触发场景：
  (1) 用户请求组织多agent讨论/会议/协作
  (2) 需要结构化的群体决策过程
  (3) 复杂问题需要多视角分析
  (4) 项目复盘、方案评审、问题分析等场景

  支持会议类型：问题分析会、方案评审会、决策会、创意脑暴会、共识对齐会、复盘会、日常站会、战略讨论会。

  支持八大类会议方法：
  - 程序治理型：罗伯特议事规则、议程驱动、时间盒
  - 问题分析型：ORID、5Why、鱼骨图、A3
  - 决策型：决策矩阵、点投票、决策树
  - 创意发散型：头脑风暴、脑写法、SCAMPER、六顶思考帽、设计冲刺
  - 共识协同型：世界咖啡、开放空间、共识决策
  - 执行推进型：站会、W3、PDCA
  - 复盘学习型：AAR、敏捷回顾、无责复盘
  - 写作驱动型：六页纸、一页纸提案、PRFAQ
---

# Meeting Skill - 多Agent协作会议框架

## 核心概念

将人类会议方法论适配为Agent协作模式，核心改造：
- 口头沟通 → 结构化文本输出
- 主持人控场 → TeamLead协调（通过SendMessage/TaskUpdate）
- 会议纪要 → 自动生成的结构化记录文件

## 会议角色

使用DACI模型定义权责：

| 角色 | 职责 | Agent对应 |
|------|------|-----------|
| Driver | 推进流程、组织协调 | TeamLead（会议发起者） |
| Approver | 最终决策权 | DecisionMaker（需明确指定） |
| Contributor | 提供专业意见 | Participant（参会agents） |
| Informed | 接收结果同步 | 相关方（会后通知） |

## 会议流程

### 会前准备

```
1. 明确会议目标 → 定义预期产出
2. 选择会议类型 → 匹配方法组合
3. 创建议程 → 写入 agenda.md
4. 分配角色 → 写入 roles.md
5. 准备输入材料 → 提供必要背景
```

**议程格式**：
```markdown
# 会议议程
## 会议目标
[明确的目标描述]

## 议题列表
| 序号 | 议题 | 时间盒 | 预期产出 | 方法 |
|------|------|--------|----------|------|
| 1 | ... | 10min | 结论 | ORID |
| 2 | ... | 15min | 方案 | 决策矩阵 |
```

### 会中推进

使用SendMessage广播议程，按环节推进：

```
TeamLead → "*": 广播议程和角色
TeamLead → Participant: 分配环节任务
Participant → TeamLead: 提交环节输出
TeamLead → "*": 环节结论同步
... 重复直至议程完成
```

**环节推进模板**（使用SendMessage）：
```
【环节X】{环节名称}
时间盒：{分钟}
任务：{具体任务描述}
输出格式：{要求的输出结构}
请各Participant在{时间}内完成输出。
```

### 会后输出

必须产出三类文档：
1. **会议纪要** (minutes.md) - 核心结论、决议、分歧处理
2. **行动项清单** (action-items.md) - W3格式（Who/What/When）
3. **流程记录** (process-log.md) - 各环节推进日志

## 会议类型与方法组合

| 会议类型 | 推荐方法组合 | 适用场景 |
|----------|--------------|----------|
| 问题分析会 | ORID + 5Why + 鱼骨图 + A3 | 故障分析、异常调查、质量问题 |
| 方案评审会 | 六页纸 + 决策矩阵 + DACI | 技术方案、项目立项、预算分配 |
| 决策会 | 决策树 + 点投票 + DACI + 时间盒 | 资源分配、路线选择、优先级 |
| 创意脑暴会 | 脑写法 + SCAMPER + 六顶思考帽 + 点投票 | 产品构思、创新方案、命名营销 |
| 共识对齐会 | 世界咖啡 + ORID + 共识决策 | 跨部门协作、认知对齐、利益协调 |
| 复盘会 | AAR + 敏捷回顾 + 无责复盘 | 项目结束、迭代复盘、事故处理 |
| 日常站会 | 三问题站会 + W3 + 时间盒 | 进度同步、阻塞暴露、高频协调 |
| 战略讨论会 | 六页纸 + PRFAQ + 决策树 | 战略方向、产品规划、重大决策 |

## 会议记录结构

创建目录：`meeting-records/session-{timestamp}/`

```
session-{timestamp}/
├── agenda.md          # 议程
├── roles.md           # 角色分配
├── phases/            # 各环节输出
│   ├── phase-1-{name}.md
│   ├── phase-2-{name}.md
│   └── ...
├── process-log.md     # 流程日志
├── minutes.md         # 会议纪要
└── action-items.md    # 行动项
```

## 快速启动

当用户请求组织会议时：

```
1. 确认会议类型 → AskUserQuestion
2. 创建Team → TeamCreate
3. 撰写议程 → Write agenda.md
4. 分配角色 → Write roles.md
5. Spawn teammates → Agent (指定team_name)
6. 广播启动 → SendMessage to "*"
7. 按议程推进环节
8. 产出纪要和行动项
9. Shutdown teammates → SendMessage shutdown_request
10. 清理Team → TeamDelete
```

## 详细方法指南

按八大类别组织，详见各方法的references文档：

### 一、程序治理型

- **罗伯特议事规则**: 见 [references/roberts-rules.md](references/roberts-rules.md)
- **议程驱动会议法**: 见 [references/agenda-driven.md](references/agenda-driven.md)
- **时间盒管理**: 见 [references/timeboxing.md](references/timeboxing.md)

### 二、问题分析型

- **ORID焦点讨论法**: 见 [references/orid.md](references/orid.md)
- **5Why分析法**: 见 [references/5why.md](references/5why.md)
- **鱼骨图**: 见 [references/fishbone.md](references/fishbone.md)
- **A3问题解决法**: 见 [references/a3-problem-solving.md](references/a3-problem-solving.md)

### 三、决策型

- **决策矩阵**: 见 [references/decision-matrix.md](references/decision-matrix.md)
- **点投票法**: 见 [references/dot-voting.md](references/dot-voting.md)
- **决策树讨论法**: 见 [references/decision-tree.md](references/decision-tree.md)

### 四、创意发散型

- **头脑风暴**: 见 [references/brainstorming.md](references/brainstorming.md)
- **脑写法**: 见 [references/brainwriting.md](references/brainwriting.md)
- **SCAMPER法**: 见 [references/scamper.md](references/scamper.md)
- **六顶思考帽**: 见 [references/six-hats.md](references/six-hats.md)
- **设计冲刺**: 见 [references/design-sprint.md](references/design-sprint.md)

### 五、共识协同型

- **世界咖啡**: 见 [references/world-cafe.md](references/world-cafe.md)
- **开放空间会议**: 见 [references/open-space.md](references/open-space.md)
- **共识决策法**: 见 [references/consensus-decision.md](references/consensus-decision.md)

### 六、执行推进型

- **站会(Daily Stand-up)**: 见 [references/standup.md](references/standup.md)
- **W3方法**: 见 [references/w3-method.md](references/w3-method.md)
- **PDCA循环**: 见 [references/pdca.md](references/pdca.md)

### 七、复盘学习型

- **AAR复盘法**: 见 [references/aar.md](references/aar.md)
- **敏捷回顾会**: 见 [references/retrospective.md](references/retrospective.md)
- **无责复盘**: 见 [references/blameless-retro.md](references/blameless-retro.md)

### 八、写作驱动型

- **六页纸会议法**: 见 [references/six-page.md](references/six-page.md)
- **一页纸提案法**: 见 [references/one-page-proposal.md](references/one-page-proposal.md)
- **PRFAQ逆向写作法**: 见 [references/prfaq.md](references/prfaq.md)

### 记录模板

- **会议纪要模板**: 见 [references/minutes-template.md](references/minutes-template.md)