# Reply queue — drafted, not posted

**Nothing here has been posted anywhere.** These are drafts for a human to read, edit and
post under their own name. Every thread was verified live on 7 September 2026 via the Hacker
News Algolia API, which returns exact timestamps, so the ages below are real.

## Scope, and why it is not fifteen threads

The brief asked for fifteen threads across r/ClaudeAI, r/cursor, r/ChatGPTCoding,
r/ExperiencedDevs, r/mcp, Hacker News and forum.cursor.com. What this session could actually
reach was Hacker News only:

- **Reddit and forum.cursor.com are blocked at the network layer here.** Their public APIs
  return `blocked-by-allowlist` from both available environments, and public web search
  returns SEO blog posts about those forums rather than the threads themselves. No thread
  from either source could be verified, so none is listed. They are worth doing by hand.
- **Hacker News works properly**, and fifteen relevant items from the last fourteen days were
  found. Most are other people's Show HN launches.

That last point is the reason this file has five drafts rather than fifteen. **Turning up
under someone's launch to mention a competing product is spam**, and on Hacker News it
reliably backfires on the person doing it. Those threads are listed below under "do not
reply", with what to take from them instead. The drafts are only for threads where somebody
asked a question that Coordigent' authors can actually answer.

Each draft answers the question first and discloses the affiliation. Two mention Coordigent; three
do not, because a mention would not have helped the person asking.

---

## 1. Ask HN: What are your biggest problems and fixes with multisession engineering?

- **URL:** https://news.ycombinator.com/item?id=49503285
- **Posted:** 30 August 2026 · **age 8 days** · 5 points, 4 comments
- **Why:** The OP is stuck on getting agents to stop at chosen points. A commenter
  (`hydropax`) separately describes picking tasks "unlikely to have merge conflicts" — hand
  scheduling around the exact failure Coordigent addresses.
- **Draft (112 words):**

> On stopping: what worked for me was making the stop condition a *tool call* rather than a
> line in the prompt. Agents talk their way past "stop after step three" in prose, but they
> genuinely stop when the next action requires calling something that can return a refusal.
> A pre-edit hook, or any tool allowed to say no, gives you a real breakpoint instead of a
> polite request.
>
> On hydropax's answer — picking tasks unlikely to conflict is the part I'd push on. That is
> manual scheduling, and it stops scaling somewhere around the fourth agent. Either detect the
> overlap (Clash simulates merges across worktrees read-only) or have agents declare files
> before editing. I work on a tool that does the latter, so discount accordingly.

---

## 2. Ask HN: Any Software Engineers here who enjoy their AI-native dev workflow?

- **URL:** https://news.ycombinator.com/item?id=49586386
- **Posted:** 6 September 2026 · **age 1 day** · 6 points, 6 comments
- **Why:** `msejas` describes hand-building file-level coordination: "my orchestrator will
  assign the implementer subagent exactly which files it can touch, and explicitly which ones
  it cannot touch. The orchestrator knows what all the other subagents are doing." That is
  someone who has already built a private version of this product.
- **Draft (118 words):**

> The line I'd underline for anyone skimming this thread is msejas's: the orchestrator assigns
> each subagent exactly which files it may touch, because the orchestrator knows what every
> other subagent is doing. That is the whole problem stated in one sentence, and centralising
> the knowledge is the right shape of answer.
>
> Worth naming where it stops. It works because one orchestrator owns every agent in the
> picture. As soon as the other agents belong to a teammate, on their machine, in a different
> client, there is no shared orchestrator holding that map, and the file assignments go back to
> being guesses. That gap is what I work on, so weigh it accordingly.

---

## 3. Ask HN: How do you manage skills files?

- **URL:** https://news.ycombinator.com/item?id=49589914
- **Posted:** 6 September 2026 · **age 1 day**
- **Why:** Adjacent, not central. A useful place to be helpful with no product mention at all.
- **Draft (74 words), no Coordigent mention:**

> The thing that made these manageable for us was treating them as code rather than config:
> one file per capability, checked in, reviewed in the same PR as whatever motivated the
> change. The failure mode is a skills directory that nobody has read in two months and every
> agent loads on every run. If you cannot say what a file changed about an agent's behaviour,
> delete it and see whether anything gets worse.

---

## 4. Nobody Has Actually Built a Software Factory

- **URL:** https://news.ycombinator.com/item?id=49510843
- **Posted:** 31 August 2026 · **age 7 days**
- **Why:** Directly about whether multi-agent development actually works at scale. A place to
  be specific and honest, including about limits.
- **Draft (96 words), no Coordigent mention:**

> The factory metaphor breaks on a detail that sounds small: stations on a real assembly line
> do not both reach for the same part. Agents do, constantly, because the codebase is one
> shared mutable object and nothing in the toolchain represents "in use" — git only speaks up
> at merge, by which point both agents have burned context on divergent work.
>
> Most current answers isolate rather than coordinate: worktrees, containers, one agent per
> branch. That works until the change genuinely spans shared files, which is where the
> interesting work lives.

---

## 5. AI Agents and the Refactoring That Never Happens

- **URL:** https://news.ycombinator.com/item?id=49541496
- **Posted:** 2 September 2026 · **age 5 days**
- **Why:** Large refactors are the case where parallel agents cannot be isolated by worktree,
  because the change is cross-cutting by definition. Good thread to make that argument in.
- **Draft (91 words), no Coordigent mention:**

> Part of why the big refactor never happens with agents is that it is the one job worktree
> isolation cannot help with. Splitting a rename across forty files into four parallel agents
> means four agents in the same files by construction, so the standard advice — give each agent
> its own worktree, pick non-overlapping tasks — has nothing to offer.
>
> So they get done sequentially by one agent, slowly, or not at all. Anyone who has actually
> landed a large cross-cutting refactor with several agents at once, I would like to hear how.

---

## Do not reply — but read

Verified, on-topic, within fourteen days, and listed so nobody wastes time rediscovering them.
A Coordigent mention in any of these would be a product plug on someone else's launch.

| Thread | Posted | Age | Why not |
| --- | --- | --- | --- |
| [Show HN: Crew — Let Claude/Codex/OpenCode agents talk to each other](https://news.ycombinator.com/item?id=49595212) | 7 Sep | 3 hours | Direct competitor's launch. See [competitor-watch.md](competitor-watch.md). |
| [Show HN: Coordination Layer for Coding Agents (Twing)](https://news.ycombinator.com/item?id=49478737) | 28 Aug | 10 days | Direct competitor's launch. |
| [LaneGate — git-native worktree orchestrator](https://news.ycombinator.com/item?id=49487178) | 29 Aug | 9 days | Someone's launch. |
| [Redshift Hub — agents in parallel across worktrees](https://news.ycombinator.com/item?id=49520913) | 1 Sep | 6 days | Someone's launch. |
| [Agentdock](https://news.ycombinator.com/item?id=49515872) | 31 Aug | 7 days | Someone's launch. |
| [Shed — git repo management for terminal agents](https://news.ycombinator.com/item?id=49523609) | 1 Sep | 6 days | Someone's launch. |
| [KanVibe](https://news.ycombinator.com/item?id=49509626) | 31 Aug | 7 days | Someone's launch. |
| [L0/L1/L2 agents, leases, gates, audits](https://news.ycombinator.com/item?id=49472343) | 27 Aug | 11 days | Someone's launch; leases are locks, worth reading. |
| [Primer: Worktrees and Coding Agents](https://news.ycombinator.com/item?id=49488677) | 29 Aug | 9 days | Explainer, no question posed. Read it — it is the mental model to argue with. |

## Before posting any of these

1. Read the thread as it stands now. These were captured on 7 September and threads move.
2. Post from a real account with history. A new account replying about one product reads
   exactly as it looks.
3. Keep the affiliation disclosure. Both product-mentioning drafts carry one; do not trim it
   for length.
4. Space them out. Five replies about agent coordination from one account in one evening is a
   pattern, whatever each individual comment says.
