<!-- Mirrors the windsurf guide shown at https://coordigent.com/install -->
# Windsurf / Cascade

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


`coord connect` does not register Windsurf — it only wires up Claude Code, Cursor, Codex
and Claude Desktop. Install Coordigent first, which also puts `coordigent` on your PATH, then
point Windsurf at it explicitly. Windsurf reads one global MCP config, so this has to be
user-scoped:

    coord install windsurf --user

Run without `--user` and nothing global is written: the installer prints the config it
would have added and tells you to re-run with `--user`.

## What gets written

Global MCP config: `~/.codeium/windsurf/mcp_config.json`

    {
      "mcpServers": {
        "coordigent": {
          "command": "/Users/you/.tower/bin/coord-mcp",
          "args": [],
          "env": {}
        }
      }
    }

Only the `coordigent` entry is added or replaced; anything else in the file stays. The
absolute path matters because GUI apps start MCP servers with a minimal PATH. No token
is stored here — `coord-mcp` reads credentials from `~/.tower/config.json`.

## Rules file

User scope appends the coordination rules to
`~/.codeium/windsurf/memories/global_rules.md`, inside `coordigent:start` / `coordigent:end` HTML
comment markers. Project scope writes `.windsurf/rules/coordigent.md` in the repo instead,
with `trigger: always_on` front matter — useful on its own if you want the rules in one
repo without touching the global config.

## Verify

    Cascade: MCPs > coordigent > refresh

Then ask Cascade to call `coordigent.status`. Windsurf is not installed on the machine these
files were checked on: the generated config passes a scripted stdio conformance run
against the real server, but the Windsurf application itself has not been exercised
here.

## What degrades

The Windsurf adapter claims stdio and HTTP transport and nothing optional — no
resources, prompts, sampling, elicitation, roots or server notifications. Coordination
does not depend on any of them: conflict notices always arrive as banners on the result
of whatever tool you just called, and stay readable in `coordigent.message.inbox`.

## Remove

Delete the `coordigent` entry from `mcpServers` in `~/.codeium/windsurf/mcp_config.json`, the
block between the `coordigent:start` and `coordigent:end` markers in
`~/.codeium/windsurf/memories/global_rules.md`, and `.windsurf/rules/coordigent.md` in any
repo where you installed at project scope.
