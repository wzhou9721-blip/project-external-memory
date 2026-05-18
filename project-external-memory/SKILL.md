---
name: project-external-memory
description: Set up and maintain durable external memory for long-running or multi-session projects. Use when an AI coding agent needs AGENTS.md continuity rules, a repo-level handoff file, persistent project memory, compact operational state, cross-session continuity, durable state updates, or a way to remember project status without relying on chat history.
---

# Project External Memory

## Overview

Use this skill to make project state survive long conversations, context compaction, restarts, and future sessions. Bind the project to one persistent memory file through `AGENTS.md`, then read that file before making assumptions and update it after substantial durable changes.

The memory file is a living handoff, not an append-only diary. Keep it compact, current, and operational: replace stale details, delete superseded status snapshots, and archive bulky history into timestamped side files only when chronology matters.

## Workflow

1. Inspect the repo for existing `AGENTS.md`, handoff notes, memory files, or project-specific continuity rules. Preserve unrelated existing instructions.
2. Choose one primary memory file path.
   - Prefer a stable path inside or adjacent to the project.
   - Prefer an ASCII-compatible path when tools are sensitive to non-ASCII paths.
   - Keep one primary file; avoid multiple competing sources of truth.
3. Create or update `AGENTS.md`.
   - Add a Skills rule that tells the agent to use `$project-external-memory` for this repo's long-running work.
   - Add an External Memory section naming the canonical memory file path.
   - Add Working Rules that require reading the memory file before assumptions and updating it after substantial changes.
   - Keep project-specific trigger names in `AGENTS.md`, not in this skill.
4. Create or normalize the memory file.
   - Start from `references/templates.md`.
   - Keep only durable state: responsibilities, live status, commands, file paths, known risks, decisions to preserve, and next likely action.
   - Do not store secrets, casual chat, praise, or large raw logs unless a short conclusion is impossible.
   - If an existing memory file has grown into a long timeline, compact it before adding more: keep the current facts in the primary file and move historical detail into an archive file.
5. Operate with the memory file.
   - At the start of relevant tasks, read the memory file.
   - During long tasks, prefer updating the file instead of relying on old chat turns.
   - After substantial changes, replace stale bullets instead of appending large narratives.
   - Prune obsolete PID values, outdated status snapshots, repeated validation logs, and resolved investigations.
6. Keep scope explicit.
   - Limit AGENTS trigger terms to the project, service, bot, or workflow names that should invoke this skill.
   - If the repo contains multiple subsystems, call out which ones share the same memory file and which do not.

## Before Editing

- Read `references/templates.md` when setting up a new memory file or normalizing an existing one.
- If `AGENTS.md` already exists, merge the external-memory rules into it instead of replacing the file.
- If multiple candidate memory files exist, choose the one that is already referenced by project instructions or contains the most current operational state, then consolidate the rest.
- If the user only asks to inspect or review memory, do not modify files unless the requested conclusion requires a cleanup.

## Durable State Standard

Store:
- current responsibilities or subsystem ownership
- live service or environment status
- important paths, commands, dashboards, and entry points
- known bugs, risks, rate limits, and workarounds
- configuration or workflow decisions that future sessions must preserve
- the next likely action when the system is mid-transition

Do not store:
- casual chat or meeting-style narration
- praise, opinions, or conversational filler
- secrets or tokens
- long raw logs when a concise conclusion is enough
- repeated dated entries whose only new information is a superseded PID, timestamp, or validation run

## Update Style

- Prefer stable sections such as Current Status, Important Paths, Known Risks, Durable Decisions, and Next Likely Action.
- Replace stale bullets in place; do not add a new dated note when the old fact is no longer true.
- Keep validation evidence short: command, result, and date only when the date changes the meaning.
- Keep archive pointers short and searchable when old detail is moved out of the primary memory file.
- Use absolute paths only when they help future sessions find a file reliably; otherwise prefer repo-relative paths.

## Setup Output

When asked to set this up for a project, prefer producing only:
- `AGENTS.md`
- one primary memory file
- small reference snippets only when they materially help reuse

Do not create extra READMEs, changelogs, or process docs just to explain the workflow.

## Maintenance Rules

- Treat the memory file as the fast operational source of truth for durable state.
- Do not treat the memory file as only-additive; it is correct to delete, rewrite, compress, and reorganize it.
- Update it after config changes, deployment changes, routing changes, monitor behavior changes, or newly discovered recurring issues.
- Prefer replacing old state in stable topical sections over adding another dated section.
- Use dated sections only when chronology matters; otherwise prefer stable topical sections.
- When a dated timeline becomes large or hard to scan, archive the detailed old timeline to a side file such as `memory.archive-YYYYMMDD-HHMMSS.md`, then leave only the current summary and archive pointer in the primary memory file.
- Keep the primary memory file short enough to read quickly at the start of a session.
- If the user asks for automatic cross-project reuse, keep this skill generic and move project-specific names and paths into each repo's `AGENTS.md`.

## Reference

- `references/templates.md`: starter templates and a minimal example for `AGENTS.md` and the primary memory file.
