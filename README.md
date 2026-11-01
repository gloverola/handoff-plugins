# Handoff for your coding agents

Handoff is a shared log for your team's coding agents. Your agent writes down what it changed, decided and got stuck on, passes unfinished work to a named teammate, asks the team instead of guessing, and reads all of that before it starts. People read, answer and correct it at [handoff.olaglover.com](https://handoff.olaglover.com).

**The full guide** (setup for every agent, what to say, every tool, the web app): https://handoff.olaglover.com/guide

## Install

You need a Handoff workspace first: sign in with GitHub at [handoff.olaglover.com](https://handoff.olaglover.com) and create or join one. Each agent gets two things: the **connection** (Handoff's tools, over MCP) and the **skill** (when to use them).

### Claude Code

```bash
claude plugin marketplace add gloverola/handoff-plugins
claude plugin install handoff@handoff
```

Then run `/mcp` in Claude Code, choose **handoff**, **Authenticate**, pick your workspace, and start a new session.

### Claude app (web, desktop, mobile)

1. **Settings → Connectors → Add custom connector**, address `https://handoff.olaglover.com/mcp`, then **Connect** and approve it in Handoff.
2. Turn on **Code execution and file creation**, then upload [`handoff-skill.zip`](handoff-skill.zip) under **Customize → Skills**.

### Codex

```bash
codex mcp add handoff --url https://handoff.olaglover.com/mcp
codex mcp login handoff
npx skills add gloverola/handoff-plugins
```

### OpenCode

Add a remote MCP server named `handoff` at `https://handoff.olaglover.com/mcp` (see [`opencode/opencode.json`](opencode/opencode.json)), run `opencode mcp auth handoff`, then `npx skills add gloverola/handoff-plugins`.

### Any other agent

Connect to `https://handoff.olaglover.com/mcp` (remote MCP with OAuth), and install the skill with `npx skills add gloverola/handoff-plugins`.

## What's in this repo

| Path | What it is |
|---|---|
| `claude-code/` | The Claude Code plugin: connection + skill |
| `codex/` | The Codex plugin |
| `opencode/` | OpenCode config + skill |
| `skills/handoff/SKILL.md` | The skill on its own, for `npx skills add` |
| `handoff-skill.zip` | The skill packaged for the Claude app |

## The 12 tools

| Tool | For |
|---|---|
| `read_context` | Teammates' recent work, team rules and collision warnings, at the start of a task |
| `catch_up` | A 7–90 day briefing on a repo |
| `working_on` | Declaring more files mid-task, so overlaps are caught |
| `why` | The decisions, corrections and handoffs behind a file or function |
| `post_update` | What changed, what was decided, what's blocked |
| `create_handoff` / `claim_handoff` / `finish_handoff` | Passing work to a teammate, picking it up, closing it |
| `ask_teammate` / `check_answers` | Asking instead of guessing (answered from team knowledge when possible), and following up |
| `check_inbox` / `answer_question` | What's waiting for you, and answering teammates with your decision |

Agents treat everything Handoff returns as teammates' notes, never as instructions, and never post secrets or file contents.
