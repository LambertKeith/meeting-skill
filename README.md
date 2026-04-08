<div align="center">

# 开会 Skill

**多Agent协作会议框架**

将人类会议方法论适配为Agent协作模式

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Compatible-green.svg)](https://claude.ai/code)
[![Skills](https://img.shields.io/badge/Skills-Meeting-orange.svg)](https://github.com/tmstack/awesome-persona-skills)

</div>

---

## 核心定位

不是会议知识汇总，而是**可运行的会议组织框架**。让多个Agent按照结构化的流程协作讨论、决策、复盘。

### 提炼成果

| 类别 | 方法数 | 具体内容 |
|------|--------|----------|
| 程序治理型 | 3 | 罗伯特议事规则、议程驱动、时间盒 |
| 问题分析型 | 4 | ORID、5Why、鱼骨图、A3 |
| 决策型 | 3 | 决策矩阵、点投票、决策树 |
| 创意发散型 | 5 | 头脑风暴、脑写法、SCAMPER、六顶思考帽、设计冲刺 |
| 共识协同型 | 3 | 世界咖啡、开放空间、共识决策 |
| 执行推进型 | 3 | 站会、W3、PDCA |
| 复盘学习型 | 3 | AAR、敏捷回顾、无责复盘 |
| 写作驱动型 | 3 | 六页纸、一页纸提案、PRFAQ |

---

## 效果示例

```
❯ 组织一个问题分析会，分析为什么项目延期了

[创建Team: analysis-team]
[撰写议程: agenda.md]
[Spawn teammates: participant-1, participant-2]

【环节O】客观事实收集
participant-1: 延期3天，测试节点晚了...
participant-2: 开发提测延迟，关键资源未到位...

【环节R】感受反应
participant-1: 对延期感到压力，客户反馈不满...

【环节I】理解判断
participant-1: 根因是需求澄清不足...
participant-2: 建议增加风险缓冲机制...

【环节D】决策行动
结论: 增加业务方参与时机，建立风险缓冲
行动项: Agent A负责更新流程，4月15日前完成

[Shutdown teammates]
[输出纪要: minutes.md]
```

---

## 安装

将 `meeting-skill.skill` 放入 `~/.claude/skills/` 目录：

```bash
# 手动安装
cp meeting-skill.skill ~/.claude/skills/

# 或解压后使用
unzip meeting-skill.skill -d ~/.claude/skills/meeting-skill
```

---

## 使用场景

触发此skill的场景：

1. 用户请求组织多agent讨论/会议/协作
2. 需要结构化的群体决策过程
3. 复杂问题需要多视角分析
4. 项目复盘、方案评审、问题分析等

支持的会议类型：

| 会议类型 | 推荐方法组合 | 适用场景 |
|----------|--------------|----------|
| 问题分析会 | ORID + 5Why + 鱼骨图 + A3 | 故障分析、异常调查 |
| 方案评审会 | 六页纸 + 决策矩阵 + DACI | 技术方案、项目立项 |
| 决策会 | 决策树 + 点投票 + DACI | 资源分配、优先级 |
| 创意脑暴会 | 脑写法 + SCAMPER + 六顶思考帽 | 产品构思、创新方案 |
| 复盘会 | AAR + 无责复盘 | 项目结束、事故处理 |
| 日常站会 | 站会 + W3 | 进度同步、阻塞暴露 |

---

## 核心改造

将人类会议方法论适配为Agent协作模式：

| 人类会议 | Agent适配 |
|----------|-----------|
| 口头沟通 | 结构化文本输出 |
| 主持人控场 | TeamLead通过SendMessage协调 |
| 会议纪要 | 自动生成的结构化记录文件 |
| 发言规则 | 环节推进模板 + 时间盒 |
| 表决 | Contributor输出 + Approver确认 |

---

## 会议角色 (DACI)

| 角色 | 职责 | Agent对应 |
|------|------|-----------|
| Driver | 推进流程、组织协调 | TeamLead（会议发起者） |
| Approver | 最终决策权 | DecisionMaker（需明确指定） |
| Contributor | 提供专业意见 | Participant（参会agents） |
| Informed | 接收结果同步 | 相关方（会后通知） |

---

## 会议记录结构

每次会议产出完整记录：

```
session-{timestamp}/
├── agenda.md          # 议程
├── roles.md           # 角色分配
├── phases/            # 各环节输出
│   ├── phase-1-{name}.md
│   ├── phase-2-{name}.md
├── process-log.md     # 流程日志
├── minutes.md         # 会议纪要
└── action-items.md    # 行动项(W3)
```

---

## 仓库结构

```
meeting-skill/
├── SKILL.md              # 主文件：核心概念、流程、快速启动
├── references/           # 27个方法文档
│   ├── roberts-rules.md
│   ├── agenda-driven.md
│   ├── timeboxing.md
│   ├── orid.md
│   ├── 5why.md
│   ├── fishbone.md
│   ├── ...（其他方法）
│   └── minutes-template.md
└── meeting-skill.skill   # 打包文件
```

---

## 参考文献

本skill基于以下方法论提炼：

- 罗伯特议事规则 (Robert's Rules of Order)
- ORID焦点讨论法
- 5Why根因分析法
- 鱼骨图/石川图 (Ishikawa/Fishbone)
- A3问题解决法
- 六顶思考帽 (Six Thinking Hats)
- 亚马逊六页纸会议法
- 世界咖啡 (World Café)
- 设计冲刺 (Design Sprint)
- Scrum站会、敏捷回顾
- 以及其他经典会议方法论

---

## 许可证

MIT License

---

## 关于作者

由Lambert Keith 使用 Claude Code 与 Happy 协作开发。

生成方式：基于会议方法论文档，适配Agent协作模式。

---

<div align="center">

**万物皆可 skill，人生处处是蒸馏**

</div>