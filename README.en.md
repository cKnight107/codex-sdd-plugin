# Spec Skills

[中文 README](./README.md)

Spec Skills is a Spec-Driven Development plugin for Codex. It is not just a bundle of isolated skills. It turns proposal, spec creation, implementation, review, fixing, and archiving into one executable workflow, so the agent can keep moving around `spec.md`, `tasks.md`, and `log.md`.

More precisely, `Spec Skills` is not only a plugin collection. It is a project execution framework. It uses the repository's `/docs` directory as the collaboration center, so AI coding is driven by documents, task breakdowns, execution logs, and archive evidence instead of short-lived chat context.

## Why Open Source This Plugin

This repository is not meant to be a prompt demo. It is meant to be a reusable Codex plugin directory that others can directly adopt:

- Ready to load into Codex
- Includes stage-oriented `spec-*` skills
- Includes foundational engineering skills for implementation, testing, review, and delivery
- Organizes requirements, proposals, tasks, logs, and archives around `/docs`
- Connects requirements, implementation, verification, and archiving through one document flow

If you want an agent to clarify requirements before coding, implement work task by task, and leave traceable evidence at the end, this plugin is designed for that workflow.

## What It Really Is

The core of `Spec Skills` is not "a few good prompts." It is "a stable project execution framework for AI coding."

The key constraints of this framework are:

- Use `/docs` as the execution backbone instead of scattering critical context across chat history
- Use `docs/changes/` to hold change proposals, specs, task breakdowns, and execution logs
- Use `docs/knowledge/` and archive content to preserve long-term knowledge, decisions, and constraints
- Keep the agent grounded in project documentation rather than generating code in isolation

So the focus of this plugin is not a one-off coding action. The focus is helping AI work continuously inside a real project with a document-driven process.

## Relationship to `agent-skills`

This project evolved from [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills), and continues to build on its approach of turning engineering practices into executable skills.

`agent-skills` provides a general-purpose engineering skill system across development phases and agent types. `Spec Skills` goes further by orchestrating those lower-level capabilities into a Spec-Driven Development lifecycle plugin tailored for Codex.

## Key Differences from `agent-skills`

| Dimension | `agent-skills` | `Spec Skills` |
| --- | --- | --- |
| Core positioning | General engineering skill collection | SDD lifecycle plugin for Codex |
| Center of gravity | Engineering method inside each skill | Stage collaboration driven by `/docs`, `spec.md`, `tasks.md`, and `log.md` |
| Working style | Trigger the right skill per task | Explicit lifecycle stages such as `spec-init`, `spec-propose`, `spec-apply`, `spec-review`, `spec-fix`, and `spec-archive` |
| Deliverables | Skill methodology | Spec documents, execution records, verification evidence, and archive actions |
| Process control | Emphasis on engineering practice | Emphasis on stage gates: propose first, implement second, review next, archive last |
| Plugin goal | Broadly applicable to many agents and tools | Focused on a document-driven Codex workflow |

In short, `agent-skills` is closer to a foundational capability layer, while `Spec Skills` is a production workflow built on top of that layer.

## What the Plugin Includes

This repository currently contains:

- `7` lifecycle-stage skills: `spec-init`, `spec-propose`, `spec-create`, `spec-apply`, `spec-review`, `spec-fix`, `spec-archive`
- `21` foundational engineering skills for design, implementation, verification, review, and delivery
- `references/full-sdd-lifecycle.md`, which defines how stage skills collaborate with foundational skills

## Repository Structure

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

## Using It in Codex

Load this repository as a local plugin directory.

### Option 1: Clone Locally

```bash
git clone https://github.com/cKnight107/codex-sdd-plugin.git
codex --plugin-dir /path/to/codex-sdd-plugin
```

### Option 2: Point Codex to This Directory

The plugin manifest is located at [`./.codex-plugin/plugin.json`](./.codex-plugin/plugin.json).

If your Codex setup supports directory-based plugins, pointing it to the repository root is enough.

## Suggested Starting Prompts

- `Use $spec-init to initialize the spec directory and document skeleton for this repository`
- `Use $spec-propose to produce spec/tasks/log for this request, and do not code before confirmation`
- `Use $spec-apply to implement confirmed tasks one by one and sync verification evidence`
- `Use $spec-review to first check spec alignment, then run a quality review`
- `Use $spec-fix to apply incremental fixes based on review findings`
- `Use $spec-archive to archive the completed change and preserve long-term knowledge`

## Lifecycle Mapping

| Stage skill | User-facing action | Foundational skills used with it |
| --- | --- | --- |
| `spec-init` | Initialize the spec/document workspace | `documentation-and-adrs`, `context-engineering` |
| `spec-propose` | Clarify the request, analyze facts, and write the proposal | `idea-refine`, `spec-driven-development`, `planning-and-task-breakdown` |
| `spec-create` | Generate the structured spec template | `spec-driven-development` |
| `spec-apply` | Implement work from tasks | `incremental-implementation`, `test-driven-development`, `git-workflow-and-versioning` |
| `spec-review` | Run a two-phase review | `code-review-and-quality`, `security-and-hardening`, `performance-optimization` |
| `spec-fix` | Fix gaps found in review or validation | `debugging-and-error-recovery`, `test-driven-development`, `documentation-and-adrs` |
| `spec-archive` | Archive the change and preserve knowledge | `documentation-and-adrs`, `shipping-and-launch` |

See [references/full-sdd-lifecycle.md](./references/full-sdd-lifecycle.md) for the full collaboration rules.

## Design Principles

- Orchestration first: stage skills handle gates and state transitions, foundational skills handle engineering methods
- Document driven: `spec.md`, `tasks.md`, and `log.md` are the execution backbone, not side artifacts
- Minimal duplication: shared lifecycle logic lives in references instead of being repeated in every skill
- Evidence loop: implementation, testing, review, fixing, and archiving all require verifiable evidence

## Acknowledgements

Thanks to [Addy Osmani](https://github.com/addyosmani) and the contributors of [agent-skills](https://github.com/addyosmani/agent-skills). This repository inherits the core idea of turning senior engineering workflows into executable skills, and then narrows that idea into a Codex-oriented Spec-Driven Development workflow.

This project is not a simple mirror of `agent-skills`, and it is not trying to replace it. It is better understood as a derivative implementation built on top of its methodology, with a stronger focus on document-driven project execution.

## License

This repository is released under the MIT License. Because parts of it evolved from `agent-skills`, this repository keeps attribution and license continuity for the upstream work.
