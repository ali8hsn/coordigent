# Name collisions — the evidence

Compiled 7 September 2026 so the naming decision can be made on what was actually observed
rather than on impressions. Three collisions, independent of each other, found in one morning.
Every query below was run through public web search on 7 September 2026; the results are
recorded as returned.

This file states findings. It does not recommend a decision, and the trademark question in
collision 2 is a lawyer's, not this file's.

---

## Collision 1 — CrewAI owns the search token

**Query run:** `Coordigent MCP server coordinate AI coding agents trycrews`

**What came back, in order:**

1. [Ai ml api MCP Integration with CrewAI — Composio](https://composio.dev/toolkits/ai_ml_api/framework/crew-ai)
2. [CrewAI (Near Intents) MCP server for AI agents — Playbooks](https://playbooks.com/mcp/coinbase-near-intents)
3. [Crew AI MCP Server — Glama](https://glama.ai/mcp/servers/@MatthewLaw1/Near-Intents-MCP-Agentkit)
4. [adam-paterson/mcp-crew-ai — GitHub](https://github.com/adam-paterson/mcp-crew-ai)
5. [MCP Servers as Tools in CrewAI — CrewAI docs](https://docs.crewai.com/en/mcp/overview)
6. [MCP Crew AI Server by adam-paterson — Glama](https://glama.ai/mcp/servers/adam-paterson/mcp-crew-ai)
7. [Supercharge CrewAI with Klavis MCP Servers — Klavis](https://www.klavis.ai/blog/crewai-klavis-multi-agent-ai-collaboration)

**Not one result is this product** — and the query contained the string `trycrews`.

**Why it matters.** CrewAI is an established multi-agent framework with its own MCP integration
surface, its own documentation site, and third-party integrations on Composio, Glama, Playbooks
and Klavis. It occupies "crew + agents" and "crew + MCP" comprehensively. This is not a ranking
gap that improves with backlinks or better documentation; the token is held by an incumbent
whose product is adjacent enough that search engines have no reason to distinguish them.

**Severity: high, and structural.** It affects every query a buyer would type.

---

## Collision 2 — trycrew.com is a funded company one character away

**Query run:** `"coordigent.com" OR "ali8hsn/coordigent"` — both exact strings, quoted.

**What came back:**

1. [Crew — Overview, News & Similar companies — ZoomInfo](https://www.zoominfo.com/c/crew-finance-inc/5000010778)
2. [Fast Crew — Wikipedia](https://en.wikipedia.org/wiki/Fast_Crew)
3. [Adrenaline Crew — Wikipedia](https://en.wikipedia.org/wiki/Adrenaline_Crew)
4. [Press Release: Crew Seed Round — Crew Finance](https://www.trycrew.com/blog/seed)
5. [The Crew — Wikipedia](https://en.wikipedia.org/wiki/The_Crew)
6. [Kick the Can Crew — Wikipedia](https://en.wikipedia.org/wiki/Kick_the_Can_Crew)
7. [Group 1 Crew — Wikipedia](https://en.wikipedia.org/wiki/Group_1_Crew)
8. [Crew Finance — Google Play](https://play.google.com/store/apps/details?id=com.trycrew.crew)
9. [Bad Crew — Wikipedia](https://en.wikipedia.org/wiki/Bad_Crew)
10. [Crew — Better than a Budget](https://www.trycrew.com/)

**Neither `coordigent.com` nor `github.com/ali8hsn/coordigent` appears at all.** A search for the
literal domain returns a different company's domain.

**What that company is.** [trycrew.com](https://www.trycrew.com/) — "Crew — Better than a
Budget" — a personal-finance app, incorporated as Crew Finance Inc, with a Google Play listing
and a published seed round. Different category, real company, funded.

**Two separate observations, which should not be blurred together.**

The absence of `coordigent.com` and the repository from these results is *expected* this early.
Neither is indexed yet under its own name. That will change on its own and is not a finding.

The domain proximity will not change. `trycrew.com` and `coordigent.com` differ by one character.
That means type-in traffic leaking to them, a support-confusion path in both directions, and a
trademark question — whether a funded incumbent in an adjacent-enough field has a claim, and
whether they would ever assert it. **That question is for a lawyer.** It is recorded here
because the cost of asking rises with every month of brand investment.

**Severity: unclear, and the only one with legal exposure.**

---

## Collision 3 — a direct competitor is called crew

**How it was found:** the Hacker News Algolia API, querying `worktree` filtered to the last
fourteen days, on 7 September 2026.

**[Show HN: Crew — Let Claude/Codex/OpenCode agents talk to each other](https://news.ycombinator.com/item?id=49595212)**
— posted 7 September 2026 at 07:44 UTC by `mmoustafa`, two points and one comment when checked
about three hours later. Repository: [github.com/0xmmo/crew](https://github.com/0xmmo/crew),
npm package `@0xmmo/crew`, MIT, TypeScript, 21 stars, created 29 June 2026, last pushed
31 August 2026.

**Its pitch, from its own README:** "Let agents talk to each other. Ship features in parallel,
no branches, no worktrees." It injects each running session's status and transcript tail into
the others and provides `crew send` for agent-to-agent mail.

**On the Show HN, the author's first listed use case is** "shipping on a single checkout without
worktrees."

**Why it matters more than the other two.** CrewAI is adjacent; trycrew.com is a different
category. This is the same problem, the same pitch, and the same word. A buyer comparing the two
has to hold "crew" and "Coordigent" apart while reading, and search engines will not help them.

Note also that it is not new — the repository is from late June and the HN post is simply its
launch — so this is not a case of someone arriving after Coordigent.

Full technical comparison, written to be fair: [docs/compare/crew-0xmmo.md](../compare/crew-0xmmo.md).
The short version is that crew does context sharing and messaging with no file-level claims,
and is scoped to one machine.

**Severity: high for buyer confusion, low for search** — at 21 stars it does not yet compete
for queries.

---

## What is not evidence of a problem

Worth stating, so the case is not overstated:

- Coordigent being absent from the three baseline queries is not caused by any of this. It is
  absent because it is new and unlisted. See [citations/2026-09-07.md](citations/2026-09-07.md).
- No user confusion has been observed, because there are not yet enough users to observe.
- Nothing here says the name is wrong. Collisions 1 and 3 are survivable with a distinctive
  enough product and enough listings; plenty of companies live beside a bigger namesake.

## If the name changes, this is what it costs today

Recorded now because the number only grows: an [mcpservers.org listing](https://mcpservers.org/servers/trycrews-com-install)
carrying the slug, an open [PR #13844](https://github.com/punkpeye/awesome-mcp-servers/pull/13844)
on a 94,537-star list, this documentation repository and its URL, the `coordigent.*` MCP tool names
that appear in every client config, the `coordigent` binary name, and eight drafted blog posts. All
of it is small today. None of it is smaller next month.

## Re-check

Re-run the two queries above verbatim and record what comes back. Watch
[github.com/0xmmo/crew](https://github.com/0xmmo/crew) for star growth, which is the signal that
collision 3 has become a search problem as well as a naming one.
