# portage
> Carry only what the step needs; when recall fails, write it down and start clean.

`portage` keeps an agent's working context lean across long tasks. It loads only
the tools and files the current step requires, watches for the point where recall
of earlier decisions degrades, and at that point writes a handoff document and
restarts in a clean agent. The rule above all: **carry only what the current step
needs, and when you can no longer recall without rereading, put it in writing and
start clean.**

## Install

| Environment | Path |
|---|---|
| Claude Code, project | `.claude/skills/portage/` |
| Claude Code, personal | `~/.claude/skills/portage/` |
| Antigravity, workspace | `.agents/skills/portage/` (legacy: `.agent/skills/`) |
| Antigravity IDE, global | `~/.gemini/antigravity/skills/portage/` |
| Antigravity CLI, global | `~/.gemini/antigravity-cli/skills/portage/` |

```bash
unzip portage.zip -d .claude/skills/
```

Antigravity global paths shift between releases. If the skill does not load, run
`/skills` in the CLI and use the path it prints.

## Usage

Fires on its own during long multi-step work. To invoke it directly:

- "check which tools you actually need before starting"
- "context is too heavy, hand off"
- "continue this in a new session"

The handoff document is written from `assets/handoff-template.md` and saved into
the project, so it survives the context that produced it.

## License

MIT — see [LICENSE](LICENSE).
