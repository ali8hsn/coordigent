# Competitor watch — 7 September 2026

Sourced from Hacker News (via the Algolia API, which returns exact timestamps) and public
search, on 7 September 2026. Everything here was fetched; nothing is recalled.

## The headline: the category is filling in fast

**Two products describing themselves almost exactly as Coordigent does launched on Hacker News in
the last ten days.** Neither existed in the competitor research of 6 September.

### crew — `github.com/0xmmo/crew`

[Show HN, 7 September 2026, 07:44 UTC](https://news.ycombinator.com/item?id=49595212), by
`mmoustafa`. Two points, one comment at time of checking — it went up three hours before this
file was written.

In the author's words, crew "hooks into your favorite CLI agent and injects a brief context
of every other running agent (status, goal, recap, last few transcript entries). It also
gives agents an interface to message each other, landing messages in another agent's context
even mid-work." His listed use cases open with "shipping on a single checkout without
worktrees", then cross-agent code review and supervisor/executor pairings across models.

Two things matter here. The **name** is Coordigent minus one letter, which compounds a naming
problem that already includes CrewAI and trycrew.com — the evidence for all three is collected
in [name-collisions.md](name-collisions.md), and a fair technical comparison is in
[docs/compare/crew-0xmmo.md](../compare/crew-0xmmo.md). Note that crew is not new: its
repository dates from 29 June 2026 and today's Show HN is its launch, not its start. And the **pitch** is ours: coordination by
shared context and inter-agent messaging on one checkout, rather than isolation by worktree.

The single comment, from `apnabhidu47`, is a useful piece of market feedback and is not
flattering to either of us: "I rarely see people use all these together, if a person is on
codex it does all tasks from codex only, same with others." That is the objection to answer —
not "why your coordination and not theirs", but "why would I run more than one client at all".

### Twing — [twing.dev](https://twing.dev/), `github.com/Twing-dev/twing-cli`

[Show HN, 28 August 2026](https://news.ycombinator.com/item?id=49478737), by `imayank`. Nine
points. Described as "an open sourced coordination layer for AI agents working on the same
repository. Detects work duplication and design conflicts early."

That is the closest positional match found so far — same layer, same object, same failure
mode, and it adds *work duplication* detection, which Coordigent does not do. Note also the second
comment, from `nishant6200`: "Interested in using it within our organisation. Shot you an
email!" Someone is already trying to buy the adjacent thing.

## The wider field, grouped by approach

**MCP coordination servers** — the direct set, all open source:

| Product | Mechanism | Source |
| --- | --- | --- |
| [crew (0xmmo)](https://news.ycombinator.com/item?id=49595212) | Live context injection between sessions plus agent-to-agent mail. **No file claims, locks or conflict detection.** Machine-local, hooks not MCP. MIT, 21 stars | [compare page](../compare/crew-0xmmo.md) |
| [Twing](https://news.ycombinator.com/item?id=49478737) | Coordination layer for agents on one repository; detects work duplication and design conflicts early | not yet written |
| [Befall](https://github.com/esenbora/befall-mcp) | Path-glob locks refused at claim time, TTL auto-release | [compare page](../compare/befall.md) |
| [MCP Agent Mail](https://mcpagentmail.com/) | Reservations with TTLs, threaded inboxes, optional enforcing pre-commit hook | [compare page](../compare/mcp-agent-mail.md) |
| [Agent Orchestration](https://github.com/madebyaris/agent-orchestration) | Resource locks, shared memory, turn-based task queue | [compare page](../compare/agent-orchestration.md) |
| [Agent Claim MCP](https://glama.ai/mcp/servers/vk0dev/agent-claim-mcp) | Claims | Glama listing |
| [agnt-lock](https://lobehub.com/mcp/codewithriza-agnt-lock) | Locks | LobeHub listing |
| [multi-agent-coordination-mcp](https://glama.ai/mcp/servers/@AndrewDavidRivers/multi-agent-coordination-mcp/blob/cbb9b966612667cfffbaad342981d6feffa22299/ARCHITECTURE.md) | Architecture proposal | Glama |

**Worktree isolation tooling** — the incumbent answer, and the real competition. These do not
coordinate agents; they keep them apart, which for many teams is enough. All from the last
fourteen days on HN:

- [Clash](https://github.com/clash-sh/clash) — read-only merge simulation across worktrees,
  pre-edit `clash check`, Claude plugin hook on Write/Edit/MultiEdit. The nearest thing to
  Coordigent' warnings, built on git rather than a server.
- [Grove](https://github.com/NathanDrake2406/grove) — detects worktree conflicts at write time.
- [LaneGate](https://news.ycombinator.com/item?id=49487178) — git-native worktree orchestrator.
- [Redshift Hub](https://news.ycombinator.com/item?id=49520913) — agents in parallel across worktrees.
- [Agentdock](https://news.ycombinator.com/item?id=49515872) — agents across repos and worktrees.
- [Shed](https://news.ycombinator.com/item?id=49523609) — git repo management for terminal agents.
- [KanVibe](https://news.ycombinator.com/item?id=49509626) — worktree and tmux Kanban board.
- [L0/L1/L2 agents, leases, gates, audits](https://news.ycombinator.com/item?id=49472343) — leases, which is locking by another name.
- [Primer: Worktrees and Coding Agents](https://news.ycombinator.com/item?id=49488677) — explainer, useful for what the default mental model now is.

**Platforms** — [Raft](../compare/raft.md), [Buzz](../compare/buzz.md),
[Entire](../compare/entire.md), [Cursor Origin](../compare/cursor-origin.md). Covered in the
comparison pages; no change observed today.

## What this changes

Three things follow, and none of them is "write more documentation".

**The worktree answer is winning by default.** Nine of the items above are worktree tooling,
posted in two weeks. Every "how do I run agents in parallel" thread on HN answers itself with
worktrees. Coordigent' argument has to be against *that*, not against other MCP servers — and the
honest version of the argument is narrow: worktrees isolate, which is correct until agents
must touch the same files, and then isolation converts a live conflict into a merge conflict
you meet later.

**Coordigent is not the only one saying "coordination layer" any more.** Twing said it on
28 August with nine points, crew said it this morning. Whatever differentiates Coordigent needs to
be sharper than the category name, because the category name is now contested.

**The strongest objection is prior to all of this.** `apnabhidu47`'s comment — most people run
one agent, from one client — is the question underneath the whole category. A comparison page
does not answer it. Evidence from real teams would.

## Re-check

Re-run the HN Algolia query for `worktree`, `coordination agents` and `agents same repo`
filtered to the last fourteen days. Both launches above surfaced that way within hours.
