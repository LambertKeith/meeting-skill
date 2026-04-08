# 问题分析会验证用例

## 验证场景

**用户请求**: "分析为什么项目延期了"

**预期触发**: 问题分析会，推荐方法 ORID + 5Why + 鱼骨图

---

## 验证步骤

### Step 1: 触发识别验证

| 检查项 | 预期结果 | 验证方式 |
|--------|----------|----------|
| 会议类型识别 | 问题分析会 | 检查TeamCreate参数 |
| 方法推荐 | ORID + 5Why | 检查agenda.md方法列 |

### Step 2: 初始化验证

| 检查项 | 预期结果 | 验证方式 |
|--------|----------|----------|
| Team创建成功 | meeting-analysis-{timestamp} | 检查TeamCreate结果 |
| agenda.md存在 | ✅ | 检查文件存在 |
| roles.md存在 | ✅ | 检查文件存在 |
| DecisionMaker已指定 | ✅ | 检查roles.md |

### Step 3: 环节推进验证

| 检查项 | 预期结果 | 验证方式 |
|--------|----------|----------|
| Phase O广播 | SendMessage to "*" | 检查process-log |
| Phase O输出 | 所有Participant有输出 | 检查phase-1-orid-o.md |
| Phase R广播 | SendMessage to "*" | 检查process-log |
| Phase R输出 | 所有Participant有输出 | 检查phase-2-orid-r.md |
| Phase I广播 | SendMessage to "*" | 检查process-log |
| Phase I输出 | 包含根因分析 | 检查phase-3-orid-i.md |
| Phase D广播 | SendMessage to "*" | 检查process-log |
| Phase D输出 | 包含行动项 | 检查phase-4-orid-d.md |

### Step 4: 输出验证

| 检查项 | 预期结果 | 验证方式 |
|--------|----------|----------|
| minutes.md存在 | ✅ | 检查文件存在 |
| 纪要包含决议 | ✅ | 检查minutes.md |
| 决议有DecisionMaker确认 | ✅ | 检查minutes.md |
| action-items.md存在 | ✅ | 检查文件存在 |
| 行动项W3格式 | Who/What/When | 检查action-items.md |
| process-log.md存在 | ✅ | 检查文件存在 |

---

## 检查清单

### 流程检查

| 检查项 | 预期结果 | 通过标准 |
|--------|----------|----------|
| 议程包含ORID四环节 | ✅ | O/R/I/D四个环节 |
| Phase O输出格式 | 事实列表 | >=3条事实 |
| Phase R输出格式 | 感受表达 | 有感受描述 |
| Phase I输出格式 | 原因分析 | 包含根因分析 |
| Phase D输出格式 | 行动项 | 有Who/What/When |

### 输出检查

| 检查项 | 预期结果 | 通过标准 |
|--------|----------|----------|
| 根因识别 | ✅ | 纪要中有根因结论 |
| 行动项明确 | ✅ | 行动项有负责人和截止时间 |
| 待决问题记录 | ✅ | 有待决问题清单 |

### 角色检查

| 角色 | 检查项 | 通过标准 |
|------|--------|----------|
| TeamLead | 环节广播 | 每环节有广播记录 |
| TeamLead | 汇总输出 | 每环节有汇总 |
| Participant | 环节输出 | 每环节有输出 |
| DecisionMaker | 决议确认 | 决议有确认记录 |

---

## 验证评分

| 维度 | 权重 | 检查项数 | 通过项数 | 得分 |
|------|------|----------|----------|------|
| 流程正确性 | 30% | 5 | {N} | {分数} |
| 角色履行度 | 20% | 4 | {N} | {分数} |
| 输出完整性 | 25% | 6 | {N} | {分数} |
| 输出质量 | 15% | 3 | {N} | {分数} |
| 方法一致性 | 10% | 5 | {N} | {分数} |
| **总分** | **100%** | **23** | **{N}** | **{分数}** |

---

## 常见问题

### 问题1: Phase O出现观点而非事实

**表现**: Phase O输出中包含"我认为"、"应该"等主观表述

**判定**: 不通过

**改进**: 提醒Participant Phase O只能陈述客观事实

### 问题2: 行动项缺乏负责人

**表现**: action-items.md中有行动项未指定Who

**判定**: 不通过

**改进**: 确保每个行动项有明确负责人

### 问题3: 决议无DecisionMaker确认

**表现**: minutes.md中决议无DecisionMaker确认记录

**判定**: 不通过

**改进**: 在Shutdown前必须获得DecisionMaker确认