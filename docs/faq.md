# Frequently asked questions

## What is Coordigent?

An MCP server that coordinates AI coding agents working in parallel on a shared GitHub
repository. It gives agents shared file state, warnings when their work overlaps another
agent's, and direct messaging between sessions. `coord` is the binary you install.

## What problem does it actually solve?

Agents on the same repository cannot see each other. Coordigent makes the other agents' current
file activity visible, and warns an agent when it is about to work where someone else
already is. See [how-it-works.md](how-it-works.md).

## Do I have to move my repository?

No. Coordigent works on the repository you already have on GitHub. It is not a git host and does
not import, mirror, or replace your remote.

## Which clients are supported?

Cursor, Codex, Claude Code, VS Code / Copilot, Kiro, Windsurf / Cascade, and Perplexity.
Every one of them runs the same stdio MCP server, `coord-mcp`. Setup for each is in
[docs/install/](install/). Slack and Microsoft Teams integrations are shipping.

## Is it tied to a model or vendor?

No. Coordigent is model-agnostic. Agents on different clients and different models coordinate
through the same server, which is the point — a team rarely standardises on one tool.

## Can agents on different machines coordinate?

Yes. Shared state is held by the Coordigent service, so agents sign in from their own machines
with their own tokens and see the same view of the repository.

## Does it run on Windows?

Untested. macOS and Linux are what Coordigent is used on. Windows is not known to be broken — it
simply has not been verified, and the `curl … | sh` install line will not run on native
Windows as written. WSL is the practical route today. This answer will be updated once
someone has actually checked.

## What does it cost?

Solo use is free. Team pricing is $20 USD per seat per month. Team pricing is currently a
preview and paid billing is not yet available.

## Where is my token stored?

In `~/.tower/config.json`. No client config file ever holds a token — the MCP entries in
`~/.claude.json`, `~/.cursor/mcp.json`, `~/.codex/config.toml` and the rest contain only a
command path. That is why the install command takes `--token` once per machine.

## Will it overwrite my existing MCP servers?

No. The installer adds or replaces only its own entry and leaves the rest of the file alone.
For Codex, whose config is TOML, the edit is textual so that key order and comments survive.

## How do I check it is working?

    coord doctor

A healthy setup reports PASS for Config, Server and User MCP, and names the clients Coordigent
was registered with. Per-client verification steps are in each install guide.

## What happens on a client that supports fewer MCP features?

Conflict warnings never ride on an optional MCP capability. They arrive as banners on the
result of whatever tool the agent just called, and remain in `coordigent.message.inbox`. So a
client with no support for server notifications, sampling or elicitation still gets every
warning. Each install guide has a "What degrades" section with that client's specifics.

## Does Coordigent merge code or resolve conflicts?

No. Git and your CI keep doing that. Coordigent warns earlier — while an agent is still choosing
what to edit — rather than at merge time.

## Does Coordigent replace code review?

No.

## Is the source open?

No. This repository holds the public documentation, licensed
[CC BY 4.0](../LICENSE). The `coord` binary and the Coordigent service are not covered by that
licence.

## How do I remove it?

Every install guide ends with a Remove section listing the exact entries and files to delete
for that client.

## Who builds it?

Ali Hussain (CEO) and Krish Dhanuka, both ex-Amazon and UT Austin.
