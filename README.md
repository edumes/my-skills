# my-skills

The context and skills I carry between coding agents. One source of truth, symlinked into each agent.

Third-party skills from [`npx skills`](https://github.com/vercel-labs/skills) stay managed there (`~/.agents/skills`). This repository holds only the skills I own or have adapted, plus my global `AGENTS.md`.

## Setup

Run `make link` once per machine, and again after adding a skill. It symlinks this repository's files into each agent's directories and refuses to overwrite anything that already exists:

| Agent | Instructions | Skills |
|---|---|---|
| Claude Code | `~/.claude/CLAUDE.md` | `~/.claude/skills/` |
| Codex | `~/.codex/AGENTS.md` | `~/.codex/skills/` |

Edits to existing files reach the agents through the links; restart a running agent to pick up a new skill.

## Skills

Each directory under `skills/` has a `SKILL.md` entry point ([Agent Skills specification](https://agentskills.io/specification)) and any files that skill needs.

| Skill | What it does |
|---|---|
| [style](skills/style/SKILL.md) | Applies Kent Beck's simple design principles while writing, reviewing, or refactoring code. |
| [simplify-code](skills/simplify-code/SKILL.md) | Makes working code easier to read without changing its behavior. Renamed to avoid clashing with Claude Code's built-in `/simplify`. |
| [humanizer](skills/humanizer/SKILL.md) | Revises prose that sounds generated while preserving its facts and intended voice. |
| [excalidraw](skills/excalidraw/SKILL.md) | Guides diagram design and uses the local Excalidraw MCP server to create and render diagrams. |
| [ask-first](skills/ask-first/SKILL.md) | Asks every question needed to understand the task, in rounds through the harness's question tool, before starting. A lighter take on `grill-me`. |
| [reflect](skills/reflect/SKILL.md) | Reviews recent sessions for repeated workflows and proposes the smallest reusable asset worth adding, or none. |
| [ponytail](skills/ponytail/SKILL.md) | Pushes coding work toward the smallest complete change: YAGNI, reuse, and stdlib or platform features before new code. Levels: lite, full, ultra. |
| [generalize](skills/generalize/SKILL.md) | Turns code that keeps being rewritten into one generic implementation that each case declares, and audits a codebase for that repetition. Proposes before building. |

### Excalidraw MCP server

The `excalidraw` skill drives the canvas through the [Excalidraw MCP server](https://github.com/yctimlin/mcp_excalidraw) (Node ≥ 20, no account needed). Register it once per machine:

```sh
claude mcp add excalidraw --scope user -- npx -y mcp-excalidraw-server
codex mcp add excalidraw -- npx -y mcp-excalidraw-server
```

The server auto-starts the canvas at <http://127.0.0.1:3000>; open it to watch the agent draw.

### Codex question tool

The `ask-first` skill asks through Codex's `request_user_input` tool, which Codex only offers outside Plan mode behind an under-development feature flag. Enable it once per machine:

```sh
codex features enable default_mode_request_user_input
```

## Upstream sources

Third-party skills are local copies. Upstream changes come in only after I review them.

| Skill | Source | Synced at | Local changes |
|---|---|---|---|
| style | [nathankim0/clean-architecture-skills](https://github.com/nathankim0/clean-architecture-skills/tree/main/plugins/kent-beck-style/skills/kent-beck-style) | `7359eb1` | Renamed from `kent-beck-style`; scope widened to writing code. |
| simplify-code | [akitaonrails/my-skills](https://github.com/akitaonrails/my-skills/tree/master/simplify), adapted from [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills/tree/main/skills/code-simplification) | `7b8a5e5` | Renamed from `simplify`; dropped `README.md` and `codemap.md`; added Addy's MIT license; removed the repo-specific "Guidance for This Repository" section. |
| humanizer | [blader/humanizer](https://github.com/blader/humanizer) | `8c307f3` | None (kept `SKILL.md`, `LICENSE`, `agents/openai.yaml`). |
| excalidraw | [coleam00/excalidraw-diagram-skill](https://github.com/coleam00/excalidraw-diagram-skill), adapted for the [yctimlin/mcp_excalidraw](https://github.com/yctimlin/mcp_excalidraw) tools | n/a | Rewritten around the MCP tools. |
| reflect | [akitaonrails/my-skills](https://github.com/akitaonrails/my-skills/tree/master/reflect) | `7b8a5e5` | Replaced OpenCode and oh-my-opencode-slim references with Claude Code and Codex equivalents (instruction files, transcripts, hooks, restart note). |
| ponytail | [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail/tree/main/skills/ponytail) | `09c434a` | Only the main skill (kept `SKILL.md`, added the repo's MIT `LICENSE`); left out the companion skills and the plugin's activation hooks. |

To update a skill: clone its source, diff it against `skills/<name>`, apply what I want to keep, and update the commit in this table.

`coleam00/excalidraw-diagram-skill` and `akitaonrails/my-skills` have no license file. Check that before publishing this repository.

## References

- [Fábio Akita's my-skills](https://github.com/akitaonrails/my-skills)
- [Agent Skills specification](https://agentskills.io/specification)
