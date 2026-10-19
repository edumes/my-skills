---
name: ask-first
description: Before starting a task, ask every question needed to understand exactly how the user wants it done, through the harness's question interface. Use when the user asks to be questioned before you start, e.g. "ask me first", "ask before starting", "pergunte antes de começar".
---

Before starting, ask every question you need to understand exactly how I want this done.

- Ask through the harness's built-in tool for questioning the user (`AskUserQuestion` in Claude Code, `request_user_input` in Codex). Fall back to plain chat only when there is none.
- Ask in rounds. Put every question that doesn't depend on another open answer in the same round, up to the tool's limit; the rest wait for the next round.
- Give each question concrete options and mark the one you recommend.
- Look up facts yourself (files, code, tools). Ask me only about decisions and preferences.
- Stop when nothing important is left to guess. State in a few lines what you will do, then start.
