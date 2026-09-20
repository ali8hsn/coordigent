<!-- Mirrors the kiro guide shown at https://coordigent.com/install -->
# Kiro

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


`coord connect` does not register Kiro — it only wires up Claude Code, Cursor, Codex and
Claude Desktop. Install Coordigent first, then point Kiro at it explicitly:

    coord install kiro

## What gets written

Workspace MCP config: `.kiro/settings/mcp.json` in the repo you ran it in.

    {
      "mcpServers": {
        "coordigent": {
          "command": "/Users/you/.tower/bin/coord-mcp",
          "args": [],
          "env": {},
          "disabled": false,
          "autoApprove": [
            "coordigent.session.list",
            "coordigent.claim.check",
            "coordigent.directory.search",
            "coordigent.directory.get",
            "coordigent.status"
          ]
        }
      }
    }

Only the `coordigent` entry is added or replaced; other MCP servers in the file stay. The
`autoApprove` list is deliberately short — it holds read-only tools only, so Kiro never
silently claims a path or acknowledges a message on your behalf. `coordigent.message.inbox`
consumes events, so it is not on the list. `disabled: false` is written explicitly, so
reinstalling re-enables an entry you had switched off in Kiro's MCP panel. No token is stored here — `coord-mcp` reads
credentials from `~/.tower/config.json`.

`coord install kiro --user` writes `~/.kiro/settings/mcp.json` instead, with the same
shape.

## Steering file

The coordination rules land in `.kiro/steering/coordigent.md` with `inclusion: always`
front matter, so Kiro loads them in every session in that workspace. User scope writes
`~/.kiro/steering/coordigent.md`.

## Verify

    Kiro: MCP Servers > coordigent > reconnect

Then ask Kiro to call `coordigent.status`. Kiro is not installed on the machine these files
were checked on: the generated config passes a scripted stdio conformance run against
the real server, but the Kiro application itself has not been exercised here.

## What degrades

Kiro's adapter claims stdio and HTTP transport and nothing optional — no resources,
prompts, sampling, elicitation, roots or server notifications. Nothing is lost that
matters for coordination: conflict notices always arrive as banners on the result of
whatever tool you just called, and stay readable in `coordigent.message.inbox`.

## Remove

Delete the `coordigent` entry from `mcpServers` in `.kiro/settings/mcp.json`, and delete
`.kiro/steering/coordigent.md`.
