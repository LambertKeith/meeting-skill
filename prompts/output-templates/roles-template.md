# 会议角色分配模板

## 使用说明

本模板用于会议角色分配文档的标准化输出。TeamLead在会议初始化阶段使用此模板创建roles.md。

---

## DACI角色模型

| 角色 | 英文名 | 职责 | Agent对应 |
|------|--------|------|-----------|
| Driver | 推进者 | 推进流程、组织协调、汇总输出 | TeamLead（会议发起者） |
| Approver | 决策者 | 最终决议确认权、分歧裁决 | DecisionMaker（需明确指定） |
| Contributor | 贡献者 | 提供专业意见、参与环节讨论 | Participant（参会Agents） |
| Informed | 知情者 | 接收结果同步（会后通知） | 相关方 |

---

## 模板格式

```markdown
# 会议角色分配

## 基本信息

| 项目 | 内容 |
|------|------|
| 会议类型 | {类型} |
| 会议议题 | {议题} |
| 会议时间 | {时间} |

## DACI角色分配

| 角色 | Agent名称 | 职责说明 | 权限范围 |
|------|-----------|----------|----------|
| Driver | TeamLead（我） | 推进流程、撰写纪要、协调环节 | 流程控制权 |
| Approver | {DecisionMaker} | 最终决议确认、分歧裁决 | 决策权 |
| Contributor | {Participant-1} | 提供专业意见 | 发言权 |
| Contributor | {Participant-2} | 提供专业意见 | 发言权 |
| Contributor | {Participant-N} | 提供专业意见 | 发言权 |
| Informed | {相关方列表} | 会后接收纪要 |知情权 |

## DecisionMaker确认

### 决策者信息
- Agent名称：{DecisionMaker名称}
- 决策范围：{本次会议需要决策的事项}
- 决策授权确认：{DecisionMaker确认}

### 决策权限说明
- DecisionMaker拥有最终决议权
- Contributors意见分歧时由DecisionMaker裁决
- 决议需记录理由

## Contributors职责说明

### Participant-1
- **角色定位**: {定位：如技术专家、业务专家等}
- **期望贡献**: {期望贡献什么专业意见}
- **发言环节**: {需要发言的环节}

### Participant-2
- **角色定位**: {定位}
- **期望贡献**: {期望贡献}
- **发言环节**: {需要发言的环节}

## 角色沟通机制

### TeamLead职责
1. 创建Team、撰写议程
2. 分配角色、Spawn Agents
3. 广播环节任务、汇总输出
4. 撰写纪要、Shutdown Agents

### Participant职责
1. 接收环节广播、按时输出
2. 提供专业意见、可延展他人观点
3. 提出待决问题
4. 确认Shutdown

### DecisionMaker职责
1. 确认决议、记录理由
2. 裁决分歧
3. 确认行动项
4. 确认会议纪要有效性

## 知情方（Informed）通知计划

| 相关方 | 通知内容 | 通知时间 |
|--------|----------|----------|
| {相关方1} | 会议纪要 | 会议结束后 |
| {相关方2} | 决议结果 | 会议结束后 |

---
角色分配创建时间：{时间}
角色分配创建者：TeamLead
```

---

## 角色分配示例

### 问题分析会角色分配

```markdown
# 会议角色分配 - 问题分析会

## DACI角色分配
| 角色 | Agent名称 | 职责说明 |
|------|-----------|----------|
| Driver | TeamLead | 推进流程、汇总根因分析 |
| Approver | decision-maker | 最终确认根因和解决方案 |
| Contributor | participant-1（技术专家） | 提供技术视角分析 |
| Contributor | participant-2（业务专家） | 提供业务视角分析 |
| Informed | 项目组成员 | 会后接收分析报告 |
```

### 决策会角色分配

```markdown
# 会议角色分配 - 决策会

## DACI角色分配
| 角色 | Agent名称 | 职责说明 |
|------|-----------|----------|
| Driver | TeamLead | 推进决策流程、汇总评分 |
| Approver | decision-maker | 最终决策确认 |
| Contributor | participant-1（技术负责人） | 提供技术评估意见 |
| Contributor | participant-2（产品负责人） | 提供产品评估意见 |
| Contributor | participant-3（运营负责人） | 提供运营评估意见 |
| Informed | 执行团队 | 会后接收决策结果 |
```

---

## 角色分配检查点

创建角色分配后检查：

| 检查项 | 状态 | 说明 |
|--------|------|------|
| DecisionMaker已明确指定 | ✅/❌ | Approver角色必须明确 |
| Contributors角色定位清晰 | ✅/❌ | 每个Participant有明确定位 |
| 职责说明完整 | ✅/❌ | 每个角色职责已说明 |
| 知情方已列出 | ✅/❌ | Informed已列出 |

---

## DecisionMaker确认请求

创建角色分配后，TeamLead需请求DecisionMaker确认：

```markdown
SendMessage({
  to: "{decision-maker}",
  summary: "DecisionMaker角色确认请求",
  message: "【角色确认请求】\n\n你被指定为本次会议的DecisionMaker（Approver）。\n\n决策范围：{决策事项}\n\n请确认是否接受此角色。\n\n确认格式：\n## DecisionMaker确认\n- 确认接受：是/否\n- 决策原则（可选）：{原则}"
})
```