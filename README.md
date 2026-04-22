# Spec Skills

面向 Codex 的 Spec-Driven Development 插件。它不是把一组零散 skill 打包在一起，而是把“提案、创建规约、实施、审查、修正、归档”这些阶段串成一条可执行工作流，让 agent 围绕 `spec.md`、`tasks.md`、`log.md` 持续推进。

更准确地说，`Spec Skills` 不只是一个插件集合，而是一套项目执行框架。它以仓库内的 `/docs` 目录为项目协作中枢，让 AI Coding 不再围绕临时对话推进，而是围绕文档、任务拆解、执行记录和归档证据持续运转。

## 为什么开源这个插件

这个仓库的目标不是演示一套 prompt，而是提供一套别人可以直接复用的 Codex 插件目录：

- 可直接加载到 Codex
- 自带阶段化 `spec-*` skill
- 内置支撑实现、测试、审查、发布的基础工程 skill
- 以 `/docs` 为中心组织需求、方案、任务、日志和归档
- 用统一文档载体把需求、实现、验证和归档串起来

如果你希望 agent 在编码前先完成需求澄清，在编码中按 task 推进，在收尾时留下可追溯证据，这个插件就是为这类流程设计的。

## 它本质上是什么

`Spec Skills` 的核心不是“多几个好用的 prompt”，而是“给 AI Coding 一套稳定的项目执行框架”。

这套框架的关键约束是：

- 以 `/docs` 作为执行主线，而不是把关键上下文散落在聊天记录里
- 用 `docs/changes/` 承载需求变更、方案设计、任务拆解和执行日志
- 用 `docs/knowledge/` 与归档内容沉淀长期有效的经验、决策和约束
- 让 agent 的编码行为始终回到文档上下文，而不是脱离项目状态单点生成代码

因此，这个插件强调的不是一次性完成某个 coding 动作，而是让 AI 在一个真实项目里按文档驱动方式持续工作。

## 它与 `agent-skills` 的关系

本项目由 [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) 演变而来，并在其工程化 skill 设计思路基础上继续发展。

`agent-skills` 提供的是一套通用、跨开发阶段、跨 agent 的工程 skill 体系；`Spec Skills` 则进一步把这些底层能力编排成一套面向 Codex 的 Spec-Driven Development 生命周期插件。

## 与 `agent-skills` 的关键区别

| 维度 | `agent-skills` | `Spec Skills` |
| --- | --- | --- |
| 核心定位 | 通用工程 skill 集合 | 面向 Codex 的 SDD 生命周期插件 |
| 关注中心 | 单个 skill 的工程方法 | `/docs` 下 `spec.md` / `tasks.md` / `log.md` 驱动的阶段协同 |
| 工作方式 | 按任务触发合适 skill | 明确区分 `spec-init`、`spec-propose`、`spec-apply`、`spec-review`、`spec-fix`、`spec-archive` |
| 交付物 | 以 skill 方法论为主 | 强制绑定规约文档、执行记录、验证证据和归档动作 |
| 流程门控 | 强调工程实践 | 强调“先提案、后实现、再审查、再归档”的阶段门控 |
| 插件目标 | 广泛适配不同 agent/工具 | 优先服务 Codex 中的规约驱动研发闭环 |

换句话说，`agent-skills` 更像基础能力层，`Spec Skills` 更像把这些能力编排成一条 SDD 生产线。

## 插件内容

当前仓库包含：

- `7` 个阶段 skill：`spec-init`、`spec-propose`、`spec-create`、`spec-apply`、`spec-review`、`spec-fix`、`spec-archive`
- `21` 个基础工程 skill，用于支撑设计、实现、验证、审查和交付
- `references/full-sdd-lifecycle.md`，用于描述阶段 skill 与基础 skill 的协同规则

## 目录结构

```txt
codex-sdd-plugin/
├── .codex-plugin/plugin.json
├── skills/
│   ├── spec-init/
│   ├── spec-propose/
│   ├── spec-create/
│   ├── spec-apply/
│   ├── spec-review/
│   ├── spec-fix/
│   ├── spec-archive/
│   └── ...
├── references/
│   └── full-sdd-lifecycle.md
└── README.md
```

## 在 Codex 中使用

把这个仓库作为本地插件目录加载即可。

### 方式一：本地目录

```bash
git clone https://github.com/cKnight107/codex-sdd-plugin.git
codex --plugin-dir /path/to/codex-sdd-plugin
```

### 方式二：直接指向当前目录

插件 manifest 位于 [`./.codex-plugin/plugin.json`](./.codex-plugin/plugin.json)。

只要 Codex 支持按目录加载插件，直接指向本仓库根目录即可。

## 推荐起手方式

- `使用 $spec-init 初始化当前仓库的规约目录和文档骨架`
- `使用 $spec-propose 为这个需求生成 spec/tasks/log，在确认前不要编码`
- `使用 $spec-apply 按已确认的 tasks 逐项实现并同步验证证据`
- `使用 $spec-review 先核对 spec 落地，再做质量审查`
- `使用 $spec-fix 根据 review findings 做增量修正`
- `使用 $spec-archive 归档已完成 change，并沉淀长期知识`

## 生命周期映射

| 阶段技能 | 面向用户的动作 | 协同的基础技能 |
| --- | --- | --- |
| `spec-init` | 初始化规约文档骨架 | `documentation-and-adrs`, `context-engineering` |
| `spec-propose` | 方案澄清、事实分析、提案落盘 | `idea-refine`, `spec-driven-development`, `planning-and-task-breakdown` |
| `spec-create` | 生成结构化 spec 模板 | `spec-driven-development` |
| `spec-apply` | 按 tasks 执行实现 | `incremental-implementation`, `test-driven-development`, `git-workflow-and-versioning` |
| `spec-review` | 两阶段审查 | `code-review-and-quality`, `security-and-hardening`, `performance-optimization` |
| `spec-fix` | 基于 findings 或失败验证修正 | `debugging-and-error-recovery`, `test-driven-development`, `documentation-and-adrs` |
| `spec-archive` | 知识沉淀与归档收尾 | `documentation-and-adrs`, `shipping-and-launch` |

完整协同规则见 [references/full-sdd-lifecycle.md](./references/full-sdd-lifecycle.md)。

## 设计原则

- 编排优先：阶段 skill 负责门控与状态推进，基础 skill 负责工程方法
- 文档驱动：`spec.md`、`tasks.md`、`log.md` 是执行主线，而不是附属产物
- 最小重复：共性流程放进共享 references，避免每个 skill 各写一套生命周期叙事
- 证据闭环：实现、测试、审查、修正、归档都要求可验证证据

## 致谢

感谢 [Addy Osmani](https://github.com/addyosmani) 及 [agent-skills](https://github.com/addyosmani/agent-skills) 项目贡献者。这个仓库继承了其“把资深工程师流程沉淀为可执行 skill”的核心思想，并在此基础上把能力进一步收敛到 Codex 中的 Spec-Driven Development 场景。

本项目不是对 `agent-skills` 的简单镜像，也不试图替代它；它更像是一个建立在其方法论之上的、面向规约驱动研发流程的派生实现。

## 许可证

本仓库采用 MIT License 发布。由于其中包含基于 `agent-skills` 演变而来的内容，仓库同时保留对上游项目的署名与许可声明。
