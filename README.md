# Spec Skills

[English README](./README.en.md)

面向 Codex 的 Spec-Driven Development 插件，核心目标不是堆一组 prompt，而是把“提案、规约、实施、审查、修正、归档”串成一条可复用、可验证、可持续推进的执行链路。

这次仓库结构已经调整为标准 marketplace 源：

- 根目录是 marketplace
- 插件实体位于 `plugins/spec-skills/`
- marketplace 索引位于 `.agents/plugins/marketplace.json`

这意味着别人既可以把这个仓库当作 marketplace 源接入，也可以直接把插件目录当作单插件目录加载。

## 仓库结构

```txt
codex-sdd-plugin/
├── .agents/plugins/marketplace.json
├── plugins/spec-skills/
│   ├── .codex-plugin/plugin.json
│   ├── skills/
│   └── references/
├── README.md
└── README.en.md
```

关键文件：

- marketplace 索引：[.agents/plugins/marketplace.json](./.agents/plugins/marketplace.json)
- 插件 manifest：[plugins/spec-skills/.codex-plugin/plugin.json](./plugins/spec-skills/.codex-plugin/plugin.json)
- 生命周期参考：[plugins/spec-skills/references/full-sdd-lifecycle.md](./plugins/spec-skills/references/full-sdd-lifecycle.md)

## 在 Codex 中使用

### 方式一：作为 marketplace 源接入

本仓库现在推荐用这种方式。

本地目录：

```bash
git clone https://github.com/cKnight107/codex-sdd-plugin.git
codex marketplace add /path/to/codex-sdd-plugin
```

Git 仓库：

```bash
codex marketplace add https://github.com/cKnight107/codex-sdd-plugin.git
```

接入后，Codex 会从根目录的 `.agents/plugins/marketplace.json` 发现 `spec-skills` 插件。

### 方式二：直接作为单插件目录加载

如果你不想走 marketplace，也可以直接指向插件目录：

```bash
git clone https://github.com/cKnight107/codex-sdd-plugin.git
codex --plugin-dir /path/to/codex-sdd-plugin/plugins/spec-skills
```

注意这里不再是仓库根目录，而是 `plugins/spec-skills/`。

## 更新与升级

这里要区分两种情况：

### 1. 你是直接读取本地仓库目录

如果你是用 `--plugin-dir /path/to/.../plugins/spec-skills` 这种方式，通常流程是：

```bash
git pull
```

然后重新打开新的 Codex 会话，通常就会用到最新内容。

### 2. 你是通过 marketplace 安装/启用插件

这时不能假设 “仓库更新 = 本地已安装插件自动升级”。更稳妥的使用方式是：

1. 先拉取仓库最新内容
2. 让 Codex 重新读取 marketplace 源
3. 必要时重新安装或重新启用该插件
4. 重新开始一个新会话验证已加载新版本

原因是 Codex 可能会把插件内容放进本地缓存，并按版本目录管理；如果版本号不变，用户和工具都很难判断这次更新是否应该刷新。

## 发布约定

为了让别人稳定拿到更新，建议按下面的最小发布流程执行：

1. 修改 `plugins/spec-skills/` 下的技能、引用文档或 manifest。
2. 每次发布都递增 [plugins/spec-skills/.codex-plugin/plugin.json](./plugins/spec-skills/.codex-plugin/plugin.json) 里的 `version`。
3. 提交并 push 到远端仓库。
4. 在 README 或 release note 里说明本次更新是否需要重新安装/重新启用。

当前版本已提升到 `0.1.1`，就是为了给后续升级建立一个明确的版本边界。

## 插件内容

当前插件包含：

- `7` 个阶段 skill：`spec-init`、`spec-propose`、`spec-create`、`spec-apply`、`spec-review`、`spec-fix`、`spec-archive`
- `21` 个基础工程 skill，用于支撑设计、实现、验证、审查和交付
- 一份完整生命周期协同参考文档

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

完整协同规则见 [plugins/spec-skills/references/full-sdd-lifecycle.md](./plugins/spec-skills/references/full-sdd-lifecycle.md)。

## 致谢

感谢 [Addy Osmani](https://github.com/addyosmani) 及 [agent-skills](https://github.com/addyosmani/agent-skills) 项目贡献者。这个仓库继承了其“把资深工程师流程沉淀为可执行 skill”的核心思想，并在此基础上把能力进一步收敛到 Codex 中的 Spec-Driven Development 场景。

## 许可证

本仓库采用 MIT License 发布。由于其中包含基于 `agent-skills` 演变而来的内容，仓库同时保留对上游项目的署名与许可声明。
