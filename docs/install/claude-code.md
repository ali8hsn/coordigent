<!-- Mirrors the claude-code guide shown at https://coordigent.com/install -->
# Claude Code

## Install Coordigent first

One line per machine. It downloads `coord` and `coord-mcp` into `~/.tower/bin`, signs the
machine in with your own token, and registers Coordigent with every supported client it finds:

    curl -fsSL https://coordigent.com/install.sh | sh -s -- --token <your-token>

Get a command with your token already filled in at https://coordigent.com/install#get-command.
Then run `coord doctor`; a healthy setup reports PASS for Config, Server, and User MCP, and
names the clients Coordigent registered.

**Platform:** the installer and `coord` are used on macOS and Linux. **Windows is
untested** — not known to be broken, simply not verified, and the `curl … | sh`
one-liner above will not run on native Windows as written. Use WSL, or wait until
this note says otherwise.


The installer registers Coordigent with Claude Code automatically whenever it finds it on the
machine. `coord connect` does the same thing on demand.

## What gets written

User-level MCP config: `~/.claude.json`

    {
      "mcpServers": {
        "tower": { "command": "/Users/you/.tower/bin/coord-mcp" }
      }
    }

Only the `coord` entry is added or replaced. Other MCP servers and the rest of the file
are left exactly as they were. No token is stored here — `coord-mcp` reads credentials
from `~/.tower/config.json`.

Run inside a git repo, `coord connect` also sets up that repo's session capture:

- `.mcp.json` — the `coord` server for this project
- `.claude/settings.json` — hooks that emit session events as you work

## The full coordination setup

`coord install claude-code`, run in a repo, adds the parallel-session layer on top. It
writes a second server entry named `coordigent` into `.mcp.json`, then:

- `.claude/settings.json` — session hooks and a Coordigent status line
- `CLAUDE.md` — the coordination rules, inside `coordigent:start` / `coordigent:end` markers
- `.claude/commands/coordigent-status.md` and `-claim`, `-msg`, `-handoff` — slash commands
- `.claude/skills/coordigent-context/` and `parallel-session-protocol/` — the protocol itself

Add `--user` to write `~/.claude.json`, `~/.claude/CLAUDE.md`, and the same commands and
skills under `~/.claude/`. The installer also prints the equivalent `claude mcp add`
command if you would rather run that yourself.

## Verify

    coord doctor
    claude mcp get coordigent

Look for `User MCP: tower registered in Claude Code`. In a session, the coordination
tools appear as `coordigent.session.list`, `coordigent.message.send`, and `coordigent.message.inbox`.

## What degrades

Nothing important. Claude Code supports resources, prompts, elicitation, roots and
list-change notifications; sampling and resource subscriptions stay off because its docs
do not guarantee them. Conflict notices never ride an optional capability — they arrive
as banners on the result of whatever tool you just called, and stay readable in
`coordigent.message.inbox`.

## Remove

Delete the `coord` and `coordigent` entries from `mcpServers` in `~/.claude.json` and any
`.mcp.json`, the hooks and status line from `.claude/settings.json`, the marked block
from `CLAUDE.md`, and the `.claude/commands/coordigent-*.md` and
`.claude/skills/coordigent-context/` files.
