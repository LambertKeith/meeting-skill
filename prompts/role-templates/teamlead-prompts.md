# TeamLead 提示词集合

## 使用说明

本文件包含TeamLead（Driver角色）在会议各阶段使用的提示词模板。

---

## 会议发起阶段

### 确认会议类型

当用户请求组织会议时：

```markdown
请确认会议类型：

| 序号 | 会议类型 | 推荐方法 | 适用场景 |
|------|----------|----------|----------|
| 1 | 问题分析会 | ORID + 5Why | 分析根因、故障调查 |
| 2 | 决策会 | 决策矩阵 | 方案选择、资源分配 |
| 3 | 方案评审会 | 六页纸 + 决策矩阵 | 技术方案、项目立项 |
| 4 | 创意脑暴会 | 脑写法 + 六顶思考帽 | 产品构思、创新方案 |
| 5 | 复盘会 | AAR + 敏捷回顾 | 项目结束、迭代复盘 |
| 6 | 共识对齐会 | 世界咖啡 + ORID | 跨部门协作、认知对齐 |
| 7 | 日常站会 | 三问题站会 | 进度同步、阻塞暴露 |

请选择会议类型（1-7）或描述您的具体需求。
```

### 创建Team

```markdown
创建会议Team：

TeamCreate(
  team_name="meeting-{type}-{timestamp}",
  description="{会议类型}：{议题描述}"
)
```

---

## 议程撰写阶段

### 议程撰写提示词

```markdown
撰写会议议程：

参考 prompts/output-templates/agenda-template.md 格式：

# 会议议程

## 基本信息
| 项目 | 内容 |
|------|------|
| 会议类型 | {类型} |
| 会议目标 | {目标描述} |
| 预期产出 | {产出描述} |
| 会议方法 | {方法组合} |

## 议程环节
| 序号 | 环节 | 方法 | 时间盒 | 预期产出 | 模板引用 |
|------|------|------|--------|----------|----------|
| 1 | {环节} | {方法} | {时间} | {产出} | {模板路径} |

## 相关材料
- {材料链接或描述}
```

---

## 角色分配阶段

### 角色分配提示词

```markdown
分配会议角色：

参考 prompts/output-templates/roles-template.md 格式：

# 会议角色分配

| 角色 | Agent名称 | 职责说明 |
|------|-----------|----------|
| Driver | TeamLead（我） | 推进流程、撰写纪要、协调环节 |
| Approver | {DecisionMaker} | 最终决议确认权 |
| Contributor | {Participant-1} | 提供专业意见 |
| Contributor | {Participant-2} | 提供专业意见 |

## DecisionMaker确认请求
请指定DecisionMaker（Approver角色）：
- 建议人选：{建议}
- 决策范围：{需要决策的事项}
```

---

## 环节推进阶段

### 环节广播提示词模板

使用SendMessage广播环节任务：

```markdown
SendMessage({
  to: "*",
  summary: "{环节名称}",
  message: "【{环节名称}】\n\n任务：{任务描述}\n时间盒：{分钟}分钟\n\n输出格式要求：\n{格式要求}\n\n请在{时间}内完成输出。\n\n---\n参考模板：{模板路径}"
})
```

### 环节收尾提示词

```markdown
环节收尾广播：

SendMessage({
  to: "*",
  summary: "{环节}已完成",
  message: "【环节收尾】{环节名称}\n\n本环节已完成。\n\n汇总结果：\n- {关键产出}\n\n共识点：{共识}\n待决点：{待决}\n\n进入下一环节：{下一环节}"
})
```

---

## 汇总阶段

### 环节汇总提示词

```markdown
撰写环节汇总：

## {环节名称} 汇总

### Participant输出汇总
| Participant | 关键产出 | 共识点 | 特殊观点 |
|-------------|----------|--------|----------|
| {Agent-1} | {产出} | {共识} | {特殊} |
| {Agent-2} | {产出} | {共识} | {特殊} |

### 共识形成
- **共识点**: {N}/{总}人同意的观点

### 分歧记录
| 分歧点 | 观点A | 观点B | 处理建议 |
|--------|-------|-------|----------|
| {分歧} | {内容} | {内容} | {建议} |

### 写入环节输出
Write("phases/phase-{n}-{name}.md", content=汇总内容)
```

---

## 决策确认阶段

### DecisionMaker确认请求提示词

```markdown
请求DecisionMaker确认：

SendMessage({
  to: "{decision-maker}",
  summary: "请求决议确认",
  message: "【决议确认请求】\n\n事项：{事项}\n\n选项：\n| 选项 | 内容 | 支持者 |\n|------|------|--------|\n| A | {内容} | {Agents} |\n| B | {内容} | {Agents} |\n\n请确认最终决议。\n\n确认格式：\n## DecisionMaker确认\n- 选择：{选项}\n- 理由：{理由}"
})
```

---

## 纪要撰写阶段

### 纪要撰写提示词

```markdown
撰写会议纪要：

参考 prompts/output-templates/minutes-template.md 格式：

# 会议纪要

## 基本信息
| 项目 | 内容 |
|------|------|
| 会议类型 | {类型} |
| 会议时间 | {时间} |
| 参会人员 | {人员列表} |
| 会议方法 | {方法组合} |

## 会议目标
{目标描述}

## 关键决议
| 序号 | 决议事项 | 决议结果 | DecisionMaker |
|------|----------|----------|---------------|
| 1 | {事项} | {结果} | {确认人} |

## 共识汇总
- {共识点}

## 分歧处理
| 分歧 | 处理方式 | 结果 |
|------|----------|------|
| {分歧} | {方式} | {结果} |

## 行动项（见action-items.md）
{行动项摘要}

## 待决问题
| 问题 | 处理建议 | 后续安排 |
|------|----------|----------|
| {问题} | {建议} | {安排} |
```

---

## 行动项撰写阶段

### 行动项撰写提示词

```markdown
撰写行动项（W3格式）：

参考 prompts/output-templates/action-items-template.md 格式：

# 会议行动项

## 行动项清单（W3格式）

| Who | What | When | 来源 | 状态 |
|-----|------|------|------|------|
| {负责人} | {行动内容} | {截止日期} | {环节/决议} | 待执行 |

## 行动项说明
- {行动项1}: {详细说明}
- {行动项2}: {详细说明}

## 行动项追踪机制
- 负责人主动更新状态
- 下次会议检查进度
```

---

## Shutdown阶段

### Shutdown通知提示词

```markdown
通知Shutdown：

SendMessage({
  to: "{participant}",
  message: {
    type: "shutdown_request",
    request_id: "{uuid}",
    reason: "会议已完成，所有议程和纪要已产出"
  }
})
```

### Shutdown确认等待

```markdown
等待Shutdown响应：

收集所有Participant的shutdown_response：
- {participant-1}: approve=true/false
- {participant-2}: approve=true/false

全部确认后执行TeamDelete。
```

---

## Team清理阶段

### TeamDelete提示词

```markdown
清理Team：

TeamDelete()

确认清理：
- Team目录已删除
- Task目录已删除
- Session上下文已清除
```

---

## 异常处理提示词

### 环节阻塞处理

```markdown
处理环节阻塞：

SendMessage({
  to: "decision-maker",
  summary: "环节阻塞处理请求",
  message: "【阻塞处理请求】\n\n阻塞环节：{环节}\n阻塞原因：{原因}\n阻塞参与者：{Agent}\n\n处理方案：\n1. {方案1}\n2. {方案2}\n\n请DecisionMaker裁决。"
})
```

### 时间盒超时处理

```markdown
时间盒超时处理：

SendMessage({
  to: "*",
  summary: "时间盒即将结束",
  message: "【时间盒提醒】\n\n当前环节剩余时间：{分钟}分钟\n已完成输出：{N}/{总}\n\n请尽快完成输出，或申请延时。"
})
```

---

## 流程日志撰写提示词

```markdown
撰写流程日志：

参考 prompts/output-templates/process-log-template.md 格式：

# 会议流程日志

## 环节推进记录
| 时间 | 环节 | 操作 | 结果 |
|------|------|------|------|
| {时间} | 开场 | TeamCreate | Team创建成功 |
| {时间} | 环节1 | SendMessage广播 | {N}人响应 |
| {时间} | 环节1 | 汇总 | 共识达成 |
| ... | ... | ... | ... |

## 异常记录
| 时间 | 异常 | 处理方式 | 结果 |
|------|------|----------|------|
| {时间} | {异常} | {处理} | {结果} |

## 消息记录
{关键SendMessage记录}
```