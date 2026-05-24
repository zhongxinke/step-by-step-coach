# Continuation Patterns

Use this reference when the task may continue in another thread, after a pause, or across multiple sessions.

## Principles

- Prefer explicit state over remembered context.
- Keep continuation artifacts short and reusable.
- Optimize for the next action, not for a long retrospective.
- Store project-specific state in the project or workspace, never in the skill installation directory.

## Thread Summary Template

Emit this at natural checkpoints inside the current thread:

```md
Progress Summary
- Goal: ...
- Current progress: ...
- Verified: ...
- Blocker: ... or None
- Next step: ...
- Mode: coach / do-it-for-me
```

Use the shortest wording that still lets another agent continue correctly.

## Resume Block Template

Offer this when the user may switch threads or continue later:

```md
Resume:
- Goal: ...
- Current step: ...
- Done: ...
- Verified: ...
- Blocker: ... or None
- Next action: ...
- Mode: coach / do-it-for-me
```

Guidance:

- Keep each field to one line when possible.
- Prefer concrete facts over commentary.
- Include the current mode so the next thread does not accidentally switch from coaching to direct execution.

## Project State File Locations

If the work has a project or repo directory, prefer one of these:

- `./.codex/coach-state.yaml`
- `./progress.md`

Recommendations:

- Prefer `./.codex/coach-state.yaml` for structured, machine-friendly continuation.
- Prefer `./progress.md` for human-readable notes or when the user may edit the file manually.
- If there is no project directory, place the file in the current workspace folder rather than inside the skill installation directory.

## `coach-state.yaml` Template

Use this for longer-running technical or project-based work:

```yaml
goal: "..."
mode: "coach"
current_step: "..."
next_action: "..."
blockers: []
completed_steps:
  - "..."
verified:
  - "..."
artifacts:
  - path: "..."
    note: "..."
```

Field guidance:

- `goal`: current target outcome
- `mode`: `coach` or `do-it-for-me`
- `current_step`: the step the user is on now
- `next_action`: the next concrete action to take
- `blockers`: current blockers; use an empty list when none
- `completed_steps`: concise milestones already finished
- `verified`: observed results that were confirmed
- `artifacts`: relevant files, commands, or outputs worth carrying forward

## `progress.md` Template

Use this when a readable narrative is more useful than strict structure:

```md
# Progress

## Goal
...

## Current Step
...

## Done
- ...

## Verified
- ...

## Blockers
- None

## Next Action
...

## Mode
coach
```

## Resume-Diagnosis Questions

If a new thread does not include enough state, ask the minimum needed to continue:

1. What is the goal you still want to reach?
2. What step were you on last time?
3. Do you want me to stay in coaching mode or switch to direct execution?

Ask for a Resume Block or state file path first if the user may already have one.
