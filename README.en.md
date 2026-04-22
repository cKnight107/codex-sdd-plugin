# Spec Skills

[中文 README](./README.md)

![Spec Skills cover](./assets/spec-skills-cover-1024.png)

Spec Skills is a Spec-Driven Development plugin for Codex. The goal is not to ship a loose collection of prompts, but to provide a reusable execution workflow across proposal, spec creation, implementation, review, fixing, and archiving.

This repository is now a single Codex plugin:

- the repository root is the plugin root
- the manifest lives at `.codex-plugin/plugin.json`
- skills live under `skills/`
- references live under `references/`

The repository no longer uses marketplace packaging and no longer depends on any marketplace index file.

## Repository Structure

```txt
codex-sdd-plugin/
├── .codex-plugin/plugin.json
├── assets/
├── references/
├── skills/
├── README.md
└── README.en.md
```

Important files:

- plugin manifest: [.codex-plugin/plugin.json](./.codex-plugin/plugin.json)
- lifecycle reference: [references/full-sdd-lifecycle.md](./references/full-sdd-lifecycle.md)

## Using It in Codex

Point Codex directly at the repository root as the plugin directory:

```bash
git clone https://github.com/cKnight107/codex-sdd-plugin.git
codex --plugin-dir /path/to/codex-sdd-plugin
```

If Codex is already open, restart the app or start a fresh session so the new plugin layout is reloaded.

## Updating and Upgrading

This repository now supports only the single-plugin flow, so updating is straightforward:

```bash
git -C /path/to/codex-sdd-plugin pull
codex --plugin-dir /path/to/codex-sdd-plugin
```

Or update inside the repository and then restart Codex:

```bash
git pull
```

There is no marketplace cache to refresh and no separate plugin install step in `/plugins`.

## Release Workflow

Use this minimum release process for reliable upgrades:

1. update files under `skills/`, `references/`, `assets/`, or [.codex-plugin/plugin.json](./.codex-plugin/plugin.json)
2. bump the `version` in [.codex-plugin/plugin.json](./.codex-plugin/plugin.json) for every release
3. commit and push the repository
4. note in the release or README whether consumers need to restart Codex or reload the plugin directory

The plugin version has been bumped to `0.2.0` to mark the breaking packaging change from marketplace layout to a single-plugin layout.

## What the Plugin Includes

The plugin currently includes:

- `7` lifecycle-stage skills: `spec-init`, `spec-propose`, `spec-create`, `spec-apply`, `spec-review`, `spec-fix`, `spec-archive`
- `21` foundational engineering skills for design, implementation, verification, review, and delivery
- one full lifecycle reference document for stage coordination

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

## Acknowledgements

Thanks to [Addy Osmani](https://github.com/addyosmani) and the contributors of [agent-skills](https://github.com/addyosmani/agent-skills). This repository builds on the idea of turning engineering practices into executable skills, then narrows that idea into a Codex-oriented, document-driven workflow.

## License

This repository is released under the MIT License. Because parts of it evolved from `agent-skills`, this repository keeps attribution and license continuity for the upstream work.
