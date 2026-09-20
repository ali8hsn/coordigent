# Command line reference

Two binaries are installed into `~/.tower/bin`, and both end up on your `PATH`.

- **`coord`** — the machine-level agent: signs in, registers Coordigent with the clients on this
  machine, and captures sessions.
- **`coordigent`** — the repository-level coordination layer: installs the per-client protocol
  files, and gives you the same claim, message and status surface the agents use.

Neither stores a token in any client config. Credentials live in one place,
`~/.tower/config.json`.

## `coord`

| Command | What it does |
| --- | --- |
| `coord login` | Signs this machine in with your token. |
| `coord connect` | Registers `coord-mcp` with every supported client found on the machine. Run inside a git repo, it also sets up that repo's session capture. |
| `coord doctor` | Health check. A healthy setup reports PASS for Config, Server and User MCP, and names the clients Coordigent registered. |
| `coord status` | Current session and crew state for this machine. |
| `coord chat` | Interactive session against the crew. |
| `tower summarize` | Summarises a captured session. |
| `coord takeover` | Takes over a session that another client started. |
| `coord init` | Initialises capture in the current repository. |
| `tower --version` | Prints the installed version. |

`tower emit`, `tower codex-watch` and `tower daemon` are internal plumbing invoked by hooks
and watchers. You should not need to run them by hand.

## `coordigent`

    coordigent <init|install <client>|doctor [client]|status [--oneline]|watch|claim <paths...>|msg <to> "text"> [--user] [--source] [--config-path path]

| Command | What it does |
| --- | --- |
| `coord install <client>` | Writes the full coordination setup for one client: its MCP entry, session hooks, protocol instructions and any slash commands or rules files it supports. |
| `coord init` | Prepares the current repository for coordination. |
| `coord doctor [client]` | Verifies the install, optionally for one client only. |
| `coord status [--oneline]` | Who is in the crew and what they have claimed. `--oneline` is the form used by status lines. |
| `coord watch` | Follows crew activity as it happens. |
| `coord claim <paths...>` | Claims repository-relative paths before editing them. |
| `coord msg <session-id\|crew> "text"` | Sends a message to one session, or to the whole crew. |

Supported `<client>` values: `claude-code`, `cursor`, `codex`, `vscode`, `kiro`,
`perplexity`, `windsurf`, `generic`. Use `generic` for any MCP client not listed; it writes a
plain `mcp.json` you can point the client at.

### Flags

| Flag | Effect |
| --- | --- |
| `--user` | Writes user- or profile-level config instead of repository-level. |
| `--config-path <path>` | Writes to an explicit config file, for non-default profiles. |
| `--source` | Prints what would be written rather than writing it. |

## The MCP tool surface

These are the tools an agent sees once Coordigent is connected. Every name is prefixed `coordigent.`.

| Tool | When an agent calls it |
| --- | --- |
| `coordigent.session.register` | At session start. Returns the `session_id` used for heartbeats and claims. |
| `coordigent.session.heartbeat` | Between tasks, and at least every 15 seconds while working. Carries pending conflicts and messages back. |
| `coordigent.session.list` | To see live sessions in the crew and pick a peer to coordinate with. |
| `coordigent.claim.check` | Before planning edits. Reads who claims a set of repository-relative paths. No side effects. |
| `coordigent.claim.add` | Before editing. Overlaps are returned as conflicts; a hard conflict denies the claim. |
| `coordigent.claim.release` | When finished editing or handing off. An agent releases only its own claim ids. |
| `coordigent.message.send` | Sends a note to a session or the crew. Messages are team-visible. |
| `coordigent.message.inbox` | Reads unread messages and conflicts. Reading consumes the inbox. |
| `coordigent.directory.search` | Searches the team's tool directory for a capability. |
| `coordigent.directory.get` | Fetches one directory entry and its installation instructions. |
| `coordigent.status` | A concise crew summary. |

`coordigent.claim.check`, `coordigent.session.list`, `coordigent.directory.search`, `coordigent.directory.get` and
`coordigent.status` are read-only, which is why they are the only ones auto-approved in the Kiro
install. `coordigent.message.inbox` consumes events, so it is never auto-approved.

Conflict notices never depend on an optional MCP capability. They arrive as banners on the
result of whatever tool the agent just called, so they reach every client, and they remain
readable in `coordigent.message.inbox`.
