# Coordigent vs crew (0xmmo/crew)

*Last checked 7 September 2026 against [github.com/0xmmo/crew](https://github.com/0xmmo/crew)
and its [Show HN thread](https://news.ycombinator.com/item?id=49595212).*

Two products, one letter apart, solving overlapping problems. That is confusing, and pretending
otherwise would not help anyone choosing between them. This page tries to be the page we would
want written about us.

## What crew is

crew is an MIT-licensed npm package — `@0xmmo/crew`, TypeScript, created 29 June 2026 — that
lets Claude Code, Codex and opencode sessions see and message one another. It is **not** an MCP
server: it works through each client's hook system, plus a CLI.

Its own summary: "crew auto-injects what your other running Claude Code, Codex, and opencode
sessions are doing (status, recap, and a tail of each transcript) into every session's context.
All three products share one crew, so any of them can see and message the others."

The four capabilities it names:

- **Shared context, live** — every session knows what the rest are doing, refreshed as it changes.
- **Agent-to-agent mail** — `crew send` drops a message into another agent's context within
  seconds, even mid-turn. `--kickstart` goes further and force-continues an agent that was
  about to stop, so it acts on the message rather than going idle.
- **A human view** — one command shows every session's status, recap and transcript tail, with
  `--json` for scripts.
- **Zero config** — `npm i -g` wires the hooks into `~/.claude/settings.json`,
  `~/.codex/hooks.json` and opencode's plugin directory automatically. It reads transcripts and
  never modifies them, and the hook always exits 0 so a slow read cannot block a turn.

There is also a Claude Code plugin route (`/plugin marketplace add 0xmmo/crew`). Node 18+,
macOS and Linux.

Its positioning is explicitly anti-worktree: "Ship features in parallel, no branches, no
worktrees", and, in the README, "Just like autonomous cars don't need stoplights, agents don't
need worktrees."

## What crew does well, and where it is ahead

Three things, stated plainly.

**Installation is genuinely one command.** `npm i -g @0xmmo/crew` wires three different clients
with no config file to edit and no account to create. Coordigent installs a binary and signs the
machine in with a token; crew does not ask for either.

**Mid-turn delivery, and `--kickstart`.** Landing a message in a session that is *already
working*, and optionally forcing it to continue rather than go idle, is a real capability and
Coordigent has no equivalent. Coordigent' messages wait in `coordigent.message.inbox` for the agent to read.

**It supports opencode.** Coordigent does not.

It is also MIT and inspectable, with no hosted dependency, which matters if repository metadata
must not leave the machine.

## The real difference: it has no file-level coordination

This is the distinction that should decide the choice, and it is not a small one.

crew shares **context** — what each agent's status, recap and recent transcript say. It does
not track which files an agent has open, does not detect that two agents are about to edit the
same file, and has no claims, locks, reservations or conflict warnings. Nothing in its README
describes any. Its injected context block says "Consider them before starting overlapping work",
which is an instruction to the model, not a mechanism.

That is a coherent design. The bet is that agents given good enough awareness of each other will
route around one another the way its README's autonomous cars do. It may well be right often
enough to be useful.

Coordigent takes the other bet: that awareness is not enough, and the moment before an edit needs an
explicit, checkable answer. `coordigent.claim.check` reads who holds a path, `coordigent.claim.add`
returns conflicts and a hard conflict denies the claim outright, and overlap warnings arrive as
banners on whatever tool the agent just called. Whether that is worth the extra machinery
depends on how much you trust context injection to change behaviour.

## The other real difference: crew is machine-local

crew's registry lives in `~/.crew/sessions/`, and the context it injects says "other agent
session(s) running on this machine right now". It coordinates the agents on one computer.

Coordigent holds coordination state for a team, so an agent on your laptop and an agent on a
colleague's can see each other in the same repository. If everything you run is on one machine,
that difference costs you nothing and crew is the lighter tool. If the second agent belongs to
a teammate, crew has nothing to say about it.

## Client coverage

| | crew | Coordigent |
| --- | --- | --- |
| Claude Code | yes | yes |
| Codex | yes | yes |
| opencode | yes | no |
| Cursor | no | yes |
| VS Code | no | yes |
| Kiro | no | yes |
| Windsurf | no | yes |
| Perplexity | no | yes |

crew integrates through hooks, which is why its list is short and deep; Coordigent integrates through
MCP, which is why its list is long and shallower.

## Which to pick

- **One machine, Claude Code / Codex / opencode, and you want it working in a minute for free:**
  crew. It is the better tool for that case and it is not close.
- **You want an agent stopped before it edits a file another agent is in, rather than told about
  it:** that is Coordigent, and crew does not attempt it.
- **The agents belong to different people:** Coordigent. crew is scoped to one machine.

They are not really substitutes, despite the names. Someone could run both.

## On the name

crew and Coordigent arrived at nearly the same name independently — crew's repository predates this
documentation by some months. Neither party is doing anything wrong, and this page is not a
claim on the word. It is here so that anyone who finds one while looking for the other can tell
them apart quickly. Corrections welcome as an issue.

## Sources

- [github.com/0xmmo/crew](https://github.com/0xmmo/crew) — README, features, install, hook
  mechanism, client list, MIT licence, repository metadata (created 29 June 2026, last push
  31 August 2026, TypeScript); fetched 7 September 2026.
- [Show HN: Crew — Let Claude/Codex/OpenCode agents talk to each other](https://news.ycombinator.com/item?id=49595212)
  — author's own description and stated use cases, posted 7 September 2026 07:44 UTC; fetched
  the same day.
