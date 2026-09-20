<!-- Mirrors the vscode guide shown at https://coordigent.com/install -->
# VS Code / Copilot

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


`coord connect` does not register VS Code — it only wires up Claude Code, Cursor, Codex
and Claude Desktop. Install Coordigent first, then point VS Code at it explicitly:

    coord install vscode

## What gets written

Workspace MCP config: `.vscode/mcp.json` in the repo you ran it in. VS Code uses a
`servers` root rather than `mcpServers`.

    {
      "servers": {
        "coordigent": {
          "type": "stdio",
          "command": "/Users/you/.tower/bin/coord-mcp",
          "args": [],
          "env": {},
          "cwd": "${workspaceFolder}"
        }
      }
    }

The merge is JSONC-aware, so your comments and any servers already listed survive. No
token is stored here — `coord-mcp` reads credentials from `~/.tower/config.json`.

`coord install vscode --user` writes the profile-level file instead, and without the
`cwd` line: `~/Library/Application Support/Code/User/mcp.json` on macOS,
`AppData/Roaming/Code/User/mcp.json` on Windows, `~/.config/Code/User/mcp.json` on
Linux. Pass `--config-path` if you keep VS Code in a non-default profile. The installer
also prints an equivalent `code --add-mcp` one-liner, if you would rather have VS Code
write its own profile entry.

## Coordination instructions

Workspace scope appends the coordination rules to `.github/copilot-instructions.md`,
inside `<!-- coordigent:start -->` / `<!-- coordigent:end -->` markers, so the rest of the file is
untouched. User scope has no equivalent file: the installer prints the same rules for
you to paste into Chat: New Instructions File > User profile with `applyTo: '**'`.

## Verify

    VS Code: MCP: List Servers > coordigent > Start

Then ask Copilot to call `coordigent.status`. The generated config has been exercised against
the real Coordigent MCP server, but the VS Code application itself has not been driven
end to end here — expect to confirm the server starts on your own machine.

## What degrades

VS Code's MCP support covers resources and prompts. Sampling, elicitation, roots, server
notifications and resource subscriptions are left off, so Coordigent never depends on them.
Conflict notices do not travel over any of those channels anyway: they always arrive as
banners on the result of whatever tool you just called, and stay readable in
`coordigent.message.inbox`.

## Remove

Delete the `coordigent` entry from `servers` in the config file, and the block between the
`coordigent:start` and `coordigent:end` markers in `.github/copilot-instructions.md`.
