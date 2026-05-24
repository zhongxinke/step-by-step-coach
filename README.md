# step-by-step-coach

`step-by-step-coach` is a Codex skill for teaching users how to achieve a goal from zero to one through guided, incremental steps instead of immediately doing the work for them.

It is designed for coaching-style interactions such as:

- building a project from scratch
- learning a new tool or workflow
- fixing a bug with guidance instead of direct patching
- setting up an environment step by step
- understanding how to implement a feature before asking Codex to take over

## What This Skill Does

When triggered, the skill makes Codex:

- clarify the target outcome and current starting point
- break the work into small milestones
- teach one step at a time
- pause at natural checkpoints
- provide partial examples, hints, snippets, or pseudocode when useful
- avoid handing over a complete implementation by default
- preserve continuation state so the work can resume later

## Default Behavior

This skill defaults to coaching mode.

That means Codex should:

- guide the user instead of silently taking over
- keep explanations short and action-oriented
- recommend one next step at a time
- adapt based on what the user tried and observed

By default, Codex should not:

- produce a full finished implementation
- rewrite an entire file end to end
- complete the whole task without the user's explicit permission

## Mode Switch

If the user explicitly asks for direct execution, full implementation, or a "do it for me" mode, Codex may switch out of coaching mode and perform the work directly.

The switch should be explicit so the user knows the interaction style has changed.

## Continuation Across Threads

This skill is designed to survive pauses and thread switches without relying on implicit thread memory.

It uses three continuation layers:

- thread summaries at natural checkpoints
- a copyable `Resume` block for moving to another thread
- optional project-local state files such as `./.codex/coach-state.yaml` or `./progress.md`

Project-specific progress should live in the project or workspace, not inside the skill installation directory.

## Example Prompts

- `Use $step-by-step-coach to teach me how to build this feature from scratch.`
- `Use $step-by-step-coach and guide me through fixing this bug without patching it directly.`
- `Use $step-by-step-coach to walk me through setting up this project step by step.`
- `Use $step-by-step-coach to coach me through this task first. If I get stuck, we can switch to direct implementation later.`

## Files

- `SKILL.md`: trigger description and operating instructions
- `agents/openai.yaml`: UI metadata for the skill
- `references/continuation.md`: resume templates and project state file patterns

## Install

Place the skill folder under:

```bash
~/.codex/skills/step-by-step-coach
```

Then invoke it explicitly with `$step-by-step-coach`, or rely on matching requests such as:

- "teach me step by step"
- "guide me instead of doing it for me"
- "walk me through it"
- "一步一步教我"
- "先不要直接改代码，带我做"

## Repository Purpose

This repository exists to version and share the `step-by-step-coach` Codex skill as a reusable teaching-first workflow.
