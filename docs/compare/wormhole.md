# Coordigent vs Wormhole

*Last checked 7 September 2026 against [github.com/fatmali/wormhole](https://github.com/fatmali/wormhole).*

## What Wormhole is

Wormhole is an open MCP server — "Collaborative AI Workflow Manager" — that gives Claude
Code, GitHub Copilot and Cursor a shared memory layer so context survives switching tools
mid-task. Its README lists universal logging, event tagging, session management, token-
optimised delta queries, **conflict detection** ("Know when agents touch the same files"),
stale-event rejection, a local web UI via `npx wormhole ui`, and knowledge capture and
search. Its documented workflow calls `check_conflicts` before edits and `log` during work.

Its README states plainly that it is an early-stage project whose APIs and behaviour may
change. At the time of checking the repository had 11 stars and no licence set. It runs
locally with `npx wormhole-mcp`.

## The honest overlap

This is the closest comparison of the four. Wormhole and Coordigent both ship an MCP server, both
track what agents are doing at file level, and both warn about agents touching the same
files. If you want that shape of tool, free and inspectable, Wormhole does it today.

## Where they differ

Wormhole is a local tool keyed on `project_path`, and its stated purpose is continuity for
*you* across your own tools and subagents — "when you switch tools mid-task, nothing gets
lost." Coordigent is built for a team of people on one GitHub repository, with per-user tokens
and state held by a service so agents on different machines share one view. Wormhole's
conflict check is a tool an agent calls; Coordigent also pushes warnings back as banners on
whatever tool result comes next.

Wormhole is open and unlicensed-as-yet; Coordigent is a hosted service with a free solo tier and
$20 per seat per month team pricing in preview.

## Which to pick

- Solo developer keeping one project coherent across Claude Code, Copilot and Cursor, who
  wants something free and local: Wormhole is a good fit and honest about its maturity.
- A team of people whose agents share one repository across several machines: that is the
  case Coordigent is built for.

## Sources

- [github.com/fatmali/wormhole](https://github.com/fatmali/wormhole) — README, feature list, tool names and project-stage disclaimer, fetched 7 September 2026.
- [Wormhole listing on mcpservers.org](https://mcpservers.org/servers/fatmali/wormhole)
