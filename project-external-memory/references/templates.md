# Project External Memory Templates

Adapt the placeholders below to the target repo. Keep repo-specific trigger names and paths in `AGENTS.md`; keep durable state in one primary memory file.

## `AGENTS.md` Template

```md
# AGENTS.md

## Skills

- Use `$project-external-memory` for any work related to `<PROJECT_NAME>`, `<SERVICE_NAME>`, `<BOT_NAME>`, `handoff`, `ops`, `monitoring`, `durable state`, or cross-session continuity.

## External Memory

- Primary memory file: `<ABSOLUTE_PATH_TO_MEMORY_FILE>`
- Canonical workspace path: `<OPTIONAL_ASCII_WORKSPACE_PATH>`
- Compatibility workspace path: `<OPTIONAL_NON_ASCII_WORKSPACE_PATH>`
- The memory file is a living handoff, not an append-only diary.
- Keep it compact and current: replace stale state, delete obsolete snapshots, summarize resolved investigations, and archive bulky history into timestamped side files when needed.

## Working Rules

- Read the memory file before making assumptions about current state.
- After substantial changes, update the memory file with concise durable state.
- Do not treat external memory as only-additive. Prune, rewrite, and compress it whenever the current file becomes redundant or hard to scan.
- Prefer replacing stale notes over appending repeated history.
- Do not rely on chat history alone for long-running work.
- Do not store secrets in the memory file.
```

## Minimal `AGENTS.md` Example

```md
# AGENTS.md

## Skills

- Use `$project-external-memory` for Project Atlas, scheduler work, handoff, ops, monitoring, and durable state.

## External Memory

- Primary memory file: `docs/project-memory.md`
- The memory file is a living handoff, not an append-only diary.
- Keep it compact and current: replace stale state, delete obsolete snapshots, and archive bulky history when needed.

## Working Rules

- Read `docs/project-memory.md` before making assumptions about current state.
- After substantial changes, update `docs/project-memory.md` with concise durable state.
- Do not store secrets, casual chat, or raw logs in the memory file.
```

## Memory File Template

```md
# Project Memory

## Scope

- Applies to Codex sessions working on `<PROJECT_NAME>`.
- Treat this file as the short durable handoff record, not an append-only diary.
- Keep this primary file compact. Move large historical detail to `memory.archive-YYYYMMDD-HHMMSS.md` and leave a pointer here.
- Primary workspace path:
  - `<WORKSPACE_PATH>`

## Current Responsibilities

- `<SUBSYSTEM>`:
  - `<WHO_OR_WHAT_IS_OWNED>`

## Live Status

- `<SERVICE_OR_ENVIRONMENT>`:
  - `<CURRENT_STATE>`

## Important Paths And Commands

- `<PATH_OR_COMMAND>`:
  - `<WHY_IT_MATTERS>`

## Known Risks / Workarounds

- `<RISK>`:
  - `<WORKAROUND_OR_DECISION>`

## Durable Decisions

- `<DECISION>`:
  - `<WHY_IT_MUST_BE_PRESERVED>`

## Next Likely Action

- `<NEXT_STEP>`

## Memory Hygiene

- Replace stale state instead of appending another dated duplicate.
- Delete obsolete PID/status snapshots after newer state supersedes them.
- Summarize completed investigations instead of preserving raw logs.
- Preserve only durable facts, current commands, active risks, routing, and recent decisions.
```

## Minimal Memory File Example

```md
# Project Memory

## Scope

- Applies to Codex sessions working on Project Atlas.
- Primary workspace path: `C:\work\project-atlas`
- Treat this file as the short durable handoff record, not a timeline.

## Live Status

- Scheduler service:
  - Local dev server runs with `npm run dev`.
  - Production deploy is manual until CI secrets are rotated.

## Important Paths And Commands

- `src/scheduler/`:
  - Owns recurring job registration and retry behavior.
- `npm test -- scheduler`:
  - Fast validation for scheduler changes.

## Known Risks / Workarounds

- CI deploy token is being rotated:
  - Do not attempt production deploys until the owner confirms the new token is active.

## Durable Decisions

- Job state remains in Postgres, not Redis:
  - Retry history must survive worker restarts.

## Next Likely Action

- Add regression coverage for retry backoff after token rotation is complete.
```

## Minimal Setup Checklist

1. Pick one primary memory file path.
2. Add or update `AGENTS.md` so the repo invokes `$project-external-memory`.
3. Create the memory file from the template.
4. Start reading the memory file before relevant work.
5. Update the memory file after substantial durable changes.
6. Periodically compact or archive old detail so the primary file stays quick to scan.
