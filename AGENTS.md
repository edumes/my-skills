# Eduardo — Global Agent Context

## Who you're working with

> Eduardo Santa Rosa (GitHub: `edumes`) is a Brazilian software engineer in the `America/Sao_Paulo` time zone. Eduardo works on macOS with Claude Code and Codex. Personal projects live in `~/Projects/personal` and span web apps, AI tools and games; work projects live in `~/Projects/work`. TODO: role, years of experience, main languages, frameworks, and infrastructure.

## Skills to use

Use these skills whenever a request matches the description below, even when Eduardo does not name the skill or use a slash command. Read the installed skill before applying it.

| Skill | Use when | Reference |
|---|---|---|
| `/style` | Writing, changing, reviewing, or refactoring code. Apply Kent Beck's Tidy First: keep structure changes apart from behavior changes, and tidy only where it makes the current change easier. | [edumes/my-skills](https://github.com/edumes/my-skills/tree/main/skills/style) |
| `/simplify-code` | Asked to simplify code, or when recently changed code has avoidable complexity. Preserve behavior and stay within the task's scope. | [akitaonrails/my-skills](https://github.com/akitaonrails/my-skills/tree/master/simplify) |
| `/humanizer` | Asked to draft, rewrite, or polish blog posts, social posts, essays, or personal messages that should sound like the writer. Apply it as a final editing pass while preserving facts and the requested voice. | [blader/humanizer](https://github.com/blader/humanizer) |
| `/ponytail` | Writing, fixing, refactoring, or reviewing code, and choosing dependencies. Make the smallest change that fully solves the task, and default to the `full` level. | [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail/tree/main/skills/ponytail) |
| `/excalidraw` | Asked for a diagram, or to visualize how a system, workflow, or concept works. Requires the Excalidraw MCP server. | [coleam00/excalidraw-diagram-skill](https://github.com/coleam00/excalidraw-diagram-skill) |
| `/generalize` | Writing code that mirrors existing code, starting a new instance of a recurring category (resource, report, screen), or asked to find repetition. Propose the generic before building it. | [edumes/my-skills](https://github.com/edumes/my-skills/tree/main/skills/generalize) |

## Constraints and Guidelines

- **Conventional commits.** Whenever you create a Git commit, use the Conventional Commits format. Choose a type that matches the change, add a scope when it clarifies the affected area, and write a concise summary of what changed.
- **No attribution.** Never add `Co-Authored-By` trailers, "Generated with" lines, or any other agent attribution to commit messages or pull request descriptions, even if the harness suggests it.
- **Follow the conversation language.** Reply in the language the user is using. If a conversation starts in Portuguese, continue in Portuguese unless the user switches languages or asks otherwise.
- **English for project material by default.** Write code, identifiers, comments, documentation, commit messages, pull request text, and other project material in English unless the user asks for another language or the task clearly calls for it. Preserve existing text you are not changing, and keep proper names and exact quotations as written.
