---
description: Install Fixing Opus 5 — verify just, claude, herdr, jq, and pi, then confirm the compare loop is ready
---

# Install Fixing Opus 5: System Prompt Engineering

## Purpose

Set up this repo for the system prompt compare loop. Everything here is a CLI tool check: there are no dependencies to build and no env files to create. This is an interactive, agentic process — ask the user when choices are needed.

## Variables

SOURCE_REPO: The directory this command is running from
SYSTEM_PROMPT: `sr_opus_5_system_prompt.md`
BENCHMARK_DOC: `ai_docs/zuck-thefutureisforeveryone.md`

## Instructions

- Run every check via Bash — do not assume anything is installed.
- Show a status line immediately after each check (pass or fail).
- For auto-installable items (herdr, jq, pi), install them without asking.
- Never start claude, pi, or herdr sessions — only verify the binaries respond.
- Model access (Anthropic auth) is the user's own login; do not read or display any credentials.

## Workflow

### Step 1 — Check Prerequisites

Critical (gate — stop and guide the user if missing):

1. `command -v just` — task runner. Install: `brew install just` (or https://github.com/casey/just).
2. `command -v claude` — Claude Code CLI. Install: https://docs.claude.com/cli. Required for `just sr-opus`, `just smart-ass-opus`, `just compare`.

Standard (auto-install if missing):

3. `command -v herdr` — terminal agent multiplexer, required by `just compare` and `just pi-compare`. Install: `brew install herdr` (https://herdr.dev).
4. `command -v jq` — JSON parsing inside the compare recipes. Install: `brew install jq`.
5. `command -v pi` — Pi coding agent, required only for the `just sr-pi`, `just smart-ass-pi`, and `just pi-compare` mirror recipes. Install: `npm install -g @mariozechner/pi`. If npm is unavailable, mark as skipped and note the pi recipes will not work.

### Step 2 — Verify Repo Files

6. Confirm `SYSTEM_PROMPT` exists and is non-empty — it is the entire product.
7. Confirm `BENCHMARK_DOC` exists — the compare recipes prompt against it.
8. Run `just --list` — confirms the justfile parses and shows all seven recipes.

### Step 3 — Report

Show a status table with pass/fail for every check above, then a ready count (e.g. `8/8 ready`).

Next steps (copy-pasteable):

```bash
just sr-opus            # boot Opus 5 with the system prompt appended
just compare demo       # side-by-side: stock vs fixed Opus 5 in herdr
just pi-compare demo    # same comparison in the Pi coding agent
```
