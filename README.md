# Spec Skills

[English README](./README.en.md)

面向 Codex 的 Spec-Driven Development 插件，核心目标不是堆一组 prompt，而是把“提案、规约、实施、审查、修正、归档”串成一条可复用、可验证、可持续推进的执行链路。

## 仓库结构

```txt
codex-sdd-plugin/
├── .codex-plugin/plugin.json
├── assets/
├── references/
├── skills/
├── README.md
└── README.en.md
```

关键文件：

- 插件 manifest：[.codex-plugin/plugin.json](./.codex-plugin/plugin.json)
- 生命周期参考：[references/full-sdd-lifecycle.md](./references/full-sdd-lifecycle.md)

## 在 Codex 中使用

直接把仓库根目录作为插件目录传给 Codex：

```bash
git clone https://github.com/cKnight107/codex-sdd-plugin.git
codex --plugin-dir /path/to/codex-sdd-plugin
```

如果 Codex 已经打开，建议重启应用或重新开始一个新会话，让新的插件结构被重新加载。

## 更新与升级

当前项目只有单插件模式，更新流程也更直接：

```bash
git -C /path/to/codex-sdd-plugin pull
codex --plugin-dir /path/to/codex-sdd-plugin
```

或者先在仓库目录里更新，再重新启动 Codex：

```bash
git pull
```

## 发布约定

为了让别人稳定拿到更新，建议按下面的最小发布流程执行：

1. 修改仓库根下的 `skills/`、`references/`、`assets/` 或 [.codex-plugin/plugin.json](./.codex-plugin/plugin.json)。
2. 每次发布都递增 [.codex-plugin/plugin.json](./.codex-plugin/plugin.json) 里的 `version`。
3. 提交并 push 到远端仓库。
4. 在 README 或 release note 里说明本次更新是否需要重启 Codex 或重新加载插件目录。

当前版本已提升到 `0.2.0`，用于标记这次从 marketplace 结构切换到单插件结构的兼容性变化。

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

完整协同规则见 [references/full-sdd-lifecycle.md](./references/full-sdd-lifecycle.md)。

## 致谢

感谢 [Addy Osmani](https://github.com/addyosmani) 及 [agent-skills](https://github.com/addyosmani/agent-skills) 项目贡献者。这个仓库继承了其“把资深工程师流程沉淀为可执行 skill”的核心思想，并在此基础上把能力进一步收敛到 Codex 中的 Spec-Driven Development 场景。

## 许可证

本仓库采用 MIT License 发布。由于其中包含基于 `agent-skills` 演变而来的内容，仓库同时保留对上游项目的署名与许可声明。
