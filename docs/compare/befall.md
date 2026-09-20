# Coordigent vs Befall

*Last checked 7 September 2026 against [github.com/esenbora/befall-mcp](https://github.com/esenbora/befall-mcp).*

> **The mechanism difference below — enforced locks versus advisory warnings — is the
> question that actually decides between these two, and Coordigent' answer to it is in progress.
> This page will change once that lands. Read it as a snapshot, not a settled position.**

## What Befall is

Befall is the closest thing to Coordigent we have found, and the comparison deserves to be read
carefully. It is an MIT-licensed MCP server — "multiplayer coordination for AI coding
agents" — where Claude Code, Codex CLI and Cursor join one shared room per repository "so
they stop overwriting each other's work." That is the same sentence Coordigent could write about
itself.

Its mechanism is different in one significant way. An agent **claims a path glob before it
edits**, and a conflicting claim is *refused at claim time* — first-writer-wins, with TTL
auto-release. Its README shows the exchange:

```
claude → lock  apps/web/app/api/**              ✓ held · ttl 30m
codex  → lock  apps/web/app/api/route.ts        ✗ refused
               → conflicts with claude · 8m left
```

It also ships a shared task board with claim and hand-off, live presence, room messaging,
and conflict alerts derived from git dirty-path heartbeats, so overlaps are caught even when
an agent ignores the protocol. Fourteen `vs_*` tools. Install is `npx befall login / init /
up`, with a local daemon and a stdio proxy. It states that only metadata leaves the machine
— paths, branches, SHAs, lock and task state — never source or diffs.

At the time of checking: MIT licensed, created 1 August 2026, last pushed 14 August 2026,
0 stars.

## Where they genuinely differ

**Advisory versus enforced.** This is the real distinction. Befall *refuses* the second
claim; the write never happens. Coordigent *warns* — it tells an agent that another agent is in
that file and lets the agent and its operator decide. Enforcement is stronger when agents
follow the protocol, and Befall's dirty-path heartbeats are a sensible backstop for when
they don't. Coordigent' warnings never block work, which means they never wrongly block work
either. Which trade you want depends on how much you trust your agents to hold and release
locks correctly, and on how you feel about an agent stalled behind a 30-minute TTL held by a
session that has since exited.

**Client coverage.** Befall documents Claude Code, Codex CLI and Cursor. Coordigent documents
those three plus VS Code, Kiro, Windsurf and Perplexity.

**Licence and maturity.** Befall is MIT and inspectable. Coordigent is a closed hosted service
with public documentation. Befall's public repository showed no commits between mid-August
and the date of checking; draw your own conclusions about either project's momentum.

## Which to pick

If hard locks are what you want, Befall implements them and you can read the code. If you
want overlap surfaced without anything being blocked, across a wider set of clients, that is
Coordigent. Anyone choosing between them should try both — they are close enough that a
paragraph here should not decide it.

## Sources

- [github.com/esenbora/befall-mcp](https://github.com/esenbora/befall-mcp) — README, tool list, architecture, licence and repository metadata; fetched 7 September 2026.
- [befall.net](https://befall.net) — project homepage listed on the repository.
