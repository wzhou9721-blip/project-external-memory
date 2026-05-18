# Project External Memory

[中文说明](README.zh-CN.md)

A reusable skill for keeping project memory across long conversations, context compaction, restarts, and future sessions.

It helps an AI coding agent remember not only current technical state, but also durable project goals, quality standards, collaboration preferences, and "do not repeat" lessons.

The skill binds a project to one compact memory file through `AGENTS.md`. That memory file is treated as a living handoff, not an append-only diary: stale state is replaced, obsolete snapshots are deleted, and bulky history is archived only when chronology matters.

## What It Does

- Adds or updates `AGENTS.md` continuity rules for a project.
- Creates one primary project memory file.
- Preserves project-level goals, preferences, and collaboration principles.
- Keeps durable state concise and operational.
- Encourages the agent to read project memory before making assumptions.
- Encourages the agent to update memory after substantial durable changes.

## When To Use It

Use this skill for long-running repos, operational projects, services, bots, monitors, migrations, or any project where future agent sessions need current state without relying on chat history.

Example prompts:

```text
Use project-external-memory to set up durable memory for this repo.
```

```text
Update the project memory after this deployment change.
```

```text
Review the external memory and compact stale notes.
```

## Install

Copy the `project-external-memory` folder into your agent's skills directory. For Codex, that is usually:

```text
~/.codex/skills/project-external-memory
```

On Windows with Codex, this is usually:

```text
C:\Users\<YOU>\.codex\skills\project-external-memory
```

## Repository Layout

```text
project-external-memory/
  SKILL.md
  agents/
    openai.yaml
  references/
    templates.md
```

## Notes

The skill itself stays generic. Project-specific names, paths, triggers, and operational state belong in each repo's `AGENTS.md` and primary memory file.

The memory file may include durable project preferences, such as quality standards, collaboration style, product goals, and risk tolerance. It should not capture casual chat, praise, private diary-like notes, or personal details that are not needed for future project work.
