# Spec Skills 与内置基础技能的协同规则

本文件定义 `spec-skills` 作为 Codex 插件时，如何与本插件 `skills/` 目录下的基础技能协同工作。

## 总原则

- `spec-skills` 负责阶段门控、文档同步和状态推进
- 本插件 `skills/` 下的基础 skill 负责每个阶段内部的工程方法
- 同一阶段内，优先先读本插件 skill，再按需补读对应基础 skill
- 如果基础 skill 的约束比阶段 skill 更严格，以更严格者为准

## 阶段映射

### 1. `spec-init`

用途：初始化 `docs/` 工作区与后续规约文档承载结构。

建议协同：

- `documentation-and-adrs`
  - 保证目录职责清晰，文档只记录长期有效信息
- `context-engineering`
  - 在初始化阶段只装载最少上下文，不提前灌入实现细节

### 2. `spec-propose`

用途：做事实分析、澄清需求、产出提案态 `spec.md`、`tasks.md`、`log.md`。

建议协同：

- `idea-refine`
  - 当用户需求仍然模糊、目标不稳定时，先做收敛
- `spec-driven-development`
  - 用它的六大核心域约束 `spec.md` 的完整性
- `planning-and-task-breakdown`
  - 用它的任务拆解规则生成提案态 `tasks.md`

### 3. `spec-create`

用途：作为 `spec-propose` 的低层模板化能力，输出结构化 spec。

建议协同：

- `spec-driven-development`
  - 继承目标、边界、测试策略、成功标准等结构化要求

### 4. `spec-apply`

用途：按确认后的 `tasks.md` 执行实现，并对每一项同步证据与日志。

建议协同：

- `incremental-implementation`
  - 一次只做一个可验证切片
- `test-driven-development`
  - 关键行为先红后绿，修 bug 先复现
- `context-engineering`
  - 只加载当前 task 的最小必要代码与规则
- `git-workflow-and-versioning`
  - 保持分支、提交粒度、回滚边界清晰

### 5. `spec-review`

用途：先做 spec 一致性审查，再做质量审查。

建议协同：

- `code-review-and-quality`
  - 提供 findings 分级和评审结构
- `security-and-hardening`
  - 处理鉴权、输入校验、敏感信息等高风险点
- `performance-optimization`
  - 对存在性能要求或潜在回归的改动补充审查

### 6. `spec-fix`

用途：根据 review findings、失败测试或验收缺口做增量修正。

建议协同：

- `debugging-and-error-recovery`
  - 先复现、再定位、再修复、最后加防回归措施
- `test-driven-development`
  - 每个 fix 都补对应证明
- `documentation-and-adrs`
  - 当修正改变边界或决策时，同步原因而不只同步结果

### 7. `spec-archive`

用途：沉淀长期知识、清理活跃 change、归档完成态目录。

建议协同：

- `documentation-and-adrs`
  - 把长期有效的决策、约束、踩坑沉淀到合适位置
- `shipping-and-launch`
  - 用它的交付收尾心智确认当前变更确实闭环，而不是中途归档

## 推荐执行路径

对于完整的 SDD 周期，推荐按下面顺序推进：

1. `spec-init`
2. `spec-propose`
3. `spec-apply`
4. `spec-review`
5. `spec-fix`
6. `spec-review`
7. `spec-archive`

如果需求只涉及局部修复，可以从 `spec-fix` 开始；如果只是审查现有实现，可以从 `spec-review` 开始。

## 不应该做的事

- 不要把 `spec-*` 当成脱离基础 skill 的独立口令；阶段 skill 仍然应调用同目录下的方法论 skill
- 不要在 `spec-propose` 阶段偷跑编码
- 不要在 `spec-apply` 完成后跳过 `spec-review`
- 不要把一次性的执行细节沉淀成长期规则
