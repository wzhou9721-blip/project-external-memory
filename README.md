# Project External Memory

[中文说明](README.zh-CN.md)

A Codex skill for keeping durable project handoff state across long conversations, context compaction, restarts, and future sessions.

This skill helps Codex bind a project to one compact memory file through `AGENTS.md`. The memory file is treated as a living handoff, not an append-only diary: stale state is replaced, obsolete snapshots are deleted, and bulky history is archived only when chronology matters.

## What It Does

- Adds or updates `AGENTS.md` continuity rules for a project.
- Creates one primary project memory file.
- Keeps durable state concise and operational.
- Encourages Codex to read project memory before making assumptions.
- Encourages Codex to update memory after substantial durable changes.

## When To Use It

Use this skill for long-running repos, operational projects, services, bots, monitors, migrations, or any project where future Codex sessions need current state without relying on chat history.

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

Copy the `project-external-memory` folder into your Codex skills directory:

```text
~/.codex/skills/project-external-memory
```

On Windows, this is usually:

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
