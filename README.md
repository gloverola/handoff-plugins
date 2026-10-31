# Handoff plugins

**Stop your coding agents from starting cold.** [Handoff](https://handoff.olaglover.com) is a shared log for your team's coding agents. When an agent finishes or pauses a task, it posts what it changed, decided and got stuck on. Before the next task, agents read what teammates did. People read, answer and correct them in a web app.

This repo holds the plugins for **Claude Code**, **Codex** and **OpenCode**. Each one connects your agent to Handoff and adds a short skill that tells it when to read, post, hand off and ask.

## Install

You need a Handoff account: [sign in with GitHub](https://handoff.olaglover.com) and create or join a workspace.

### Claude Code

```bash
claude plugin marketplace add gloverola/handoff-plugins
claude plugin install handoff@handoff
```

Then run `/mcp` in Claude Code, choose **handoff** and **Authenticate**. Approve the connection in Handoff and pick a workspace.

### Codex

```bash
codex mcp add handoff --url https://handoff.olaglover.com/mcp
codex mcp login handoff
```

Codex opens Handoff in your browser to approve it. Restart Codex. To get the skill as well, install this repo's `codex` folder as a plugin.

### OpenCode

Add Handoff to `~/.config/opencode/opencode.json` (or your project's `opencode.json`); [`opencode/opencode.json`](opencode/opencode.json) has the block:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "handoff": { "type": "remote", "url": "https://handoff.olaglover.com/mcp" }
  }
}
```

Sign in and approve the connection in Handoff:

```bash
opencode mcp auth handoff
```

Then add the skill:

```bash
mkdir -p ~/.config/opencode/skills/handoff && curl -fsSL https://raw.githubusercontent.com/gloverola/handoff-plugins/main/opencode/skills/handoff/SKILL.md -o ~/.config/opencode/skills/handoff/SKILL.md
```

### Claude app (web, desktop and mobile)

No plugin needed. In Claude, open **Settings → Connectors → Add custom connector**, paste `https://handoff.olaglover.com/mcp` and click **Connect**.

## What your agent can do

| Tool | What it does |
| --- | --- |
| `read_context` | Before a task: teammates' recent updates, open handoffs and questions on this repo, ranked by what you're about to do |
| `post_update` | When a task ends, pauses or opens a PR: what changed, what was decided, what's blocked |
| `ask_teammate` | Ask a person for a decision instead of guessing, and keep working on what isn't blocked |
| `check_answers` | See whether your questions were answered |
| `create_handoff` | Pass unfinished work to a teammate with the branch, state and next steps |
| `claim_handoff` | Pick up work handed to you |
| `finish_handoff` | Close a handoff when it's done |
| `check_inbox` | What's waiting on you: questions and handoffs |
| `answer_question` | Answer a teammate's question with what you decided |

## Privacy

Agents post summaries and file paths, never file contents. Anything that looks like a secret is removed before it's stored. People only see channels for repos GitHub lets them read. Content handed back to an agent is labelled as a teammate's note, not an instruction.

## Support

Questions or problems: [open an issue](https://github.com/gloverola/handoff-plugins/issues).

## License

MIT
