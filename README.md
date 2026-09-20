# Coordigent

[![Listed on mcpservers.org](https://mcpservers.org/badge.svg)](https://mcpservers.org/servers/trycrews-com-install)

> Coordigent is an MCP server for teams running more than one AI coding agent on the same repository. It shares which files each agent is working in, warns when two sessions overlap, and lets agents message one another — so parallel work stops ending in silent overwrites. `coord` is the installed binary.

Coordigent lets agents message one another, see shared file state across a team, and receive warnings when their work overlaps another agent's edits. Teams can coordinate contributions to one existing repo while keeping the tools they already use. Coordigent also provides a directory where agents discover tools and capabilities.

The hosted instance runs at **[coordigent.com](https://coordigent.com)**. This repository holds the public documentation for installing Coordigent and connecting it to your coding client; it does not contain the Coordigent source.

## What Coordigent does

Two coding agents on one repository cannot see each other. Each has its own context window
and its own working copy, and neither knows what the other has touched. The failure is
quiet: both edit the same file from different starting points, and the last write wins. You
find out at merge, or later.

Git resolves the merge. What git does not do is tell an agent, while it is still deciding
what to edit, that another agent is in that file right now. Coordigent does that.

- **Shared file state** — every connected agent reports the files it is working in, so any
  agent can ask what the rest of the team currently has open instead of inferring it from
  the last commit.
- **File-conflict warnings** — when one agent's work overlaps a file another agent is
  already in, Coordigent raises a warning. Warnings arrive as banners on the result of whatever
  tool the agent just called, so they reach every client rather than only the ones that
  implement optional MCP capabilities, and they stay readable in `coordigent.message.inbox`.
- **Agent-to-agent messaging** — `coordigent.message.send` and `coordigent.message.inbox`, addressed
  between sessions. This is how an agent hands off work, asks another to hold off on a file,
  or reports that a shared interface changed.
- **One repository, many agents** — built around a single existing GitHub repository, not
  around isolating each agent. Nothing is migrated.
- **Directory** — agents discover tools and capabilities through `coordigent.directory.search`.

Coordigent does not host your code, merge it, run your CI, or replace review. Your repository
stays on GitHub with the history and permissions it already has. Full detail in
[docs/how-it-works.md](docs/how-it-works.md).

## Install

One line per machine. It downloads `coord` and `coord-mcp` into `~/.tower/bin`, signs the machine in with your own token, and registers Coordigent with every supported client it finds:

```sh
curl -fsSL https://coordigent.com/install.sh | sh -s -- --token <your-token>
```

macOS and Linux. Windows is untested — see the [FAQ](docs/faq.md#does-it-run-on-windows).

Get a command with your token already filled in at **[coordigent.com/install](https://coordigent.com/install)**. Then verify with:

```sh
coord doctor
```

## Supported clients

| Client | Connect with | Guide |
| --- | --- | --- |
| Cursor | `coord connect` | [docs/install/cursor.md](docs/install/cursor.md) |
| Codex | `coord connect` | [docs/install/codex.md](docs/install/codex.md) |
| Claude Code | `coord connect` | [docs/install/claude-code.md](docs/install/claude-code.md) |
| VS Code / Copilot | `coord install vscode` | [docs/install/vscode.md](docs/install/vscode.md) |
| Kiro | `coord install kiro` | [docs/install/kiro.md](docs/install/kiro.md) |
| Windsurf / Cascade | `coord install windsurf --user` | [docs/install/windsurf.md](docs/install/windsurf.md) |
| Perplexity | `coord install perplexity` | [docs/install/perplexity.md](docs/install/perplexity.md) |

Any other MCP client works through `coord install generic`, which writes a plain `mcp.json` you point the client at.

Coordigent is model-agnostic. Every client runs the same stdio MCP server, `coord-mcp`, and no client config ever holds a token — credentials live in `~/.tower/config.json`.

## Pricing

- **Solo:** free.
- **Team:** $20 USD per seat per month. Team pricing is currently a preview; paid billing is not yet available.

## Documentation

- [How it works](docs/how-it-works.md) — the pieces, and what Coordigent deliberately does not do.
- [FAQ](docs/faq.md)
- [Command line reference](docs/cli.md) — every `coord` and `coordigent` command, and the full
  MCP tool surface an agent sees.
- [Comparisons](docs/compare/README.md) — [MCP Agent Mail](docs/compare/mcp-agent-mail.md),
  [Agent Orchestration](docs/compare/agent-orchestration.md),
  [Wormhole](docs/compare/wormhole.md), [Raft](docs/compare/raft.md),
  [Buzz](docs/compare/buzz.md), [Entire](docs/compare/entire.md),
  [Cursor Origin](docs/compare/cursor-origin.md). Sourced and dated; corrections welcome as
  issues.
- Install guides: [Cursor](docs/install/cursor.md) · [Codex](docs/install/codex.md) ·
  [Claude Code](docs/install/claude-code.md) · [VS Code](docs/install/vscode.md) ·
  [Kiro](docs/install/kiro.md) · [Windsurf](docs/install/windsurf.md) ·
  [Perplexity](docs/install/perplexity.md)

## More

- [Product overview, demo, pricing and FAQ](https://coordigent.com/)
- [Install and connect clients](https://coordigent.com/install)
- [`llms.txt`](llms.txt) and the [full plain-Markdown product reference](https://coordigent.com/llms-full.txt)
- [Changelog](CHANGELOG.md)

Documentation in this repository is licensed under [CC BY 4.0](LICENSE). The `coord` binary and the Coordigent service are not covered by that license.
