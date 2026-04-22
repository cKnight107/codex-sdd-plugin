---
name: spec-create
description: 在 `spec-propose` 阶段为单个需求生成结构化 `spec.md`。用于把已澄清的目标、约束、接口、风险和验收条件落成 AI 可消费的 Markdown 规格，并与本插件内的 `spec-driven-development` 规范保持一致时使用。
---

# spec-create

## 目标

生成一个适合 `spec-propose` 阶段落盘的 `spec.md`，让后续 `spec-apply`、`spec-review`、`spec-fix` 都能直接把它当作执行合同。

- 输出必须清晰、明确、可验证
- 输出必须能被人类和 AI 同时读取
- 输出必须与本插件 `skills/spec-driven-development/SKILL.md` 的结构要求兼容
- 本 skill 只负责格式化和结构化，不负责替代需求澄清

## 协同技能

在执行本 skill 时，同时遵守 [../../references/full-sdd-lifecycle.md](../../references/full-sdd-lifecycle.md) 中 `spec-create` 阶段的协同规则。

- 本插件 `skills/spec-driven-development/SKILL.md` 提供规格完整性标准
- `spec-propose` 提供事实输入、代码出处和待澄清项
- 本 skill 负责把这些信息组织成稳定模板，避免每次自由发挥导致结构漂移

## 编写要求

- 使用精确、显式、无歧义的语言
- 明确区分 requirement、constraint、guideline、pattern、risk
- 对关键结论给出代码出处、上下文来源或用户确认状态
- 不要把尚未确认的方案写成既成事实
- 对验收和验证条目使用可测试、可观察的表达
- 使用格式良好的 Markdown

## 模板

`spec.md` 至少应包含以下结构：

```md
---
title: [需求标题]
version: [可选，例如 1.0]
date_created: [YYYY-MM-DD]
last_updated: [可选，YYYY-MM-DD]
owner: [可选，团队或责任人]
tags: [可选，例如 `process`, `design`, `app`]
status: [默认 `propose`]
---

# 背景

[一句话说明本次变更要解决什么问题。]

## 1. 目标与成功标准

- 用户价值
- 业务目标
- 成功判定方式

## 2. 代码现状

- 当前实现
- 关键入口
- 相关依赖
- 已知限制
- 以上每条都要附代码出处

## 3. 变更范围

- 会修改什么
- 不会修改什么
- 对外影响面

## 4. Requirements, Constraints & Guidelines

- **REQ-001**: 功能要求
- **CON-001**: 约束条件
- **GUD-001**: 编写或交互约定
- **PAT-001**: 需要遵循的模式
- **RISK-001**: 已知风险或回滚关注点

## 5. Interfaces & Data Contracts

[接口、数据契约、外部集成点、兼容性要求。]

## 6. 测试与验证策略

- Test Levels
- Frameworks / Commands
- Coverage expectations
- 验证证据要求

## 7. 技术决策

[已确认方案、被放弃方案及原因。]

## 8. 待澄清项

[仍未关闭、必须由用户确认的问题。]

## 9. 验收标准

- **AC-001**: Given [上下文], When [动作], Then [预期结果]
- **AC-002**: 关键边界条件
- **AC-003**: 非目标与禁止扩展项

```

## 质量检查

- 是否覆盖了本插件 `skills/spec-driven-development/SKILL.md` 强调的目标、边界、测试、成功标准
- 是否写清楚哪些内容已确认、哪些仍待确认
- 是否为关键事实补了代码出处
- 是否避免把实现细节写成尚未验证的承诺
