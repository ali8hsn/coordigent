# Submission research — reconnaissance and payloads

**Nothing in this file has been submitted, and nothing here is approved for filing.**
[submission-queue.md](submission-queue.md) is the gate: an entry is only fileable once it
appears there with status `ready`. This file is the research behind those entries — what each
directory requires, and the exact text or payload to use when one is approved.

This session had no authority to file anything externally and no GitHub credential to do it
with. Everything was verified on 7 September 2026 against the live repository, API or page
named in each entry.

[submission-results.md](submission-results.md) records what has actually been filed.

## Standard description

Use verbatim wherever a description is requested:

> MCP server for shared file state, overlap warnings, and messaging between AI coding agents
> working in parallel on one GitHub repo.

Never write **"hosted at"** or **"at domain"** in any listing copy. Glama's spam filter reacts
to both, and the awesome-list entries sync into Glama.

---

## Read this first: one blocker gates most of the list

**Glama is not one directory among many. It is the dependency.**

PR [#13844](https://github.com/punkpeye/awesome-mcp-servers/pull/13844) on
punkpeye/awesome-mcp-servers — the 94,537-star list — is open, mergeable and **blocked**. The
repository's bot commented at 08:11 UTC today with its listing requirements:

> 1. **Ensure your server is listed on Glama.** If it isn't already, submit it at
>    https://glama.ai/mcp/servers and verify that it passes all checks (note: you must add
>    Dockerfile directly to Glama. For checks to pass, we only need the server to start and
>    respond to introspection requests).
> 2. **Update your PR** by adding a Glama score badge after the server description, using this
>    format: `[![OWNER/REPO MCP server](https://glama.ai/mcp/servers/OWNER/REPO/badges/score.svg)](https://glama.ai/mcp/servers/OWNER/REPO)`

It also notes: "If your server already has a hosted endpoint, you can also list it under
https://glama.ai/mcp/connectors."

So the order is **Glama first, then the badge, then the PR merges** — and the Dockerfile that
Glama needs is exactly the artifact reported on branch `registry/docker-and-mcpb`
(PR [#1](https://github.com/ali8hsn/coordigent/pull/1)). The pieces exist; they have not been
connected.

Glama itself needs a person: submission sits behind an account, and creating accounts was
outside this session's remit.

---

## Tier 1 — do these

### 1. Official MCP Registry — **viable today, highest value, nobody has tried it**

- **URL:** https://registry.modelcontextprotocol.io · repo `modelcontextprotocol/registry` (7,226 stars, pushed 5 Sep 2026)
- **Mechanism:** `mcp-publisher` CLI, GitHub OAuth login. Not a form, not a PR.
- **Status:** Not attempted. **Not blocked.**

This is the canonical registry that MCP clients read — "like an app store for MCP servers" in
its own words. It is in preview, so breaking changes are possible.

The important finding: **the remote route needs no npm package, no Dockerfile and no OAuth.**
The schema accepts a `remotes` array with `streamable-http` and arbitrary auth headers marked
secret. Production already serves Streamable HTTP at `/mcp` with a bearer token, so this is
publishable now — unlike Smithery, which specifically demands OAuth.

GitHub authentication requires the server name to begin with `io.github.ali8hsn/`.

**Exact `server.json` to publish:**

```json
{
  "$schema": "https://static.modelcontextprotocol.io/schemas/2025-12-11/server.schema.json",
  "name": "io.github.ali8hsn/coordigent",
  "description": "MCP server for shared file state, overlap warnings, and messaging between AI coding agents working in parallel on one GitHub repo.",
  "repository": {
    "url": "https://github.com/ali8hsn/coordigent",
    "source": "github"
  },
  "version": "0.1.0",
  "remotes": [
    {
      "type": "streamable-http",
      "url": "https://coordigent.com/mcp",
      "headers": [
        {
          "name": "Authorization",
          "description": "Bearer token from your Coordigent account. Get one at https://coordigent.com/install",
          "isRequired": true,
          "isSecret": true
        }
      ]
    }
  ]
}
```

**Steps:** install `mcp-publisher` (Homebrew or the release binary), `mcp-publisher validate`,
`mcp-publisher login` with GitHub, `mcp-publisher publish`.

**Confirm before publishing:** that `Authorization` is the correct header name and that a
bearer token is accepted in it — this session could not reach `coordigent.com` from either
environment (`blocked-by-allowlist`), and the 401 observed came through a page fetcher that
does not expose response headers. Also set `version` to the real one; `0.1.0` is a placeholder.

An MCPB package entry can be added later alongside `remotes` once `dist/coordigent.mcpb` is
published somewhere fetchable.

### 2. Glama — account required, unblocks everything above it

- **URL:** https://glama.ai/mcp/servers ("Add Server")
- **Status:** Blocked on account creation. Needs a human.
- **What to supply:** repository `https://github.com/ali8hsn/coordigent`; the standard description;
  the Dockerfile from `registry/docker-and-mcpb`. Checks only require the server to start and
  answer introspection.
- **Then:** grab the resulting Glama path and add the badge to PR #13844 (next entry).
- **Also worth doing:** list the hosted endpoint separately at https://glama.ai/mcp/connectors.

### 3. punkpeye/awesome-mcp-servers — open PR, one step from merging

- **PR:** https://github.com/punkpeye/awesome-mcp-servers/pull/13844 · open, `mergeable_state: clean`, 1 file, 1 addition
- **Status:** Blocked only on the Glama badge above.
- **Current entry on the branch:**

```
- [ali8hsn/coordigent](https://github.com/ali8hsn/coordigent) 🎖️ ☁️ 🏠 🍎 🐧 - MCP server for shared file state, overlap warnings, and messaging between coding agents working in parallel on one GitHub repo. Works with Claude Code, Cursor, Codex, VS Code, Kiro, Windsurf and Perplexity. Free solo tier; team pricing in preview.
```

**Two corrections to make in the same push as the badge:**

- **No language marker.** Nearly every neighbouring entry carries one. The source is
  TypeScript — `packages/cli`, `packages/mcp` and `packages/shared` are all `.ts` — so the
  marker is 📇, which belongs after 🎖️. This is only a decision about whether to name the
  implementation language publicly; the fact itself is verified.
- **Windows.** The entry claims 🍎 🐧 and omits 🪟. Nothing in the docs states whether Windows
  works. If it does, this under-claims on a list that syncs into Glama; if it does not, the
  install guides should say so. Settle it before the badge push.

**Final line, assuming TypeScript is named and Windows stays unclaimed** — replace `OWNER/REPO`
with the real Glama path:

```
- [ali8hsn/coordigent](https://github.com/ali8hsn/coordigent) [![ali8hsn/coordigent MCP server](https://glama.ai/mcp/servers/OWNER/REPO/badges/score.svg)](https://glama.ai/mcp/servers/OWNER/REPO) 📇 🎖️ ☁️ 🏠 🍎 🐧 - MCP server for shared file state, overlap warnings, and messaging between coding agents working in parallel on one GitHub repo. Works with Claude Code, Cursor, Codex, VS Code, Kiro, Windsurf and Perplexity. Free solo tier; team pricing in preview.
```

Keep `🤖🤖🤖` in the PR title. Their CONTRIBUTING states it opts agent PRs into a fast-track
merge, so it is deliberate, not decoration. Category and alphabetical placement on the branch
were not re-verified by this session.

---

## Tier 2 — straightforward PRs, no blocker found

All three are active and take ordinary pull requests. Each needs a fork, a one-line addition
in the right category, alphabetical order preserved, and a PR.

| List | Stars | Last push | Notes |
| --- | --- | --- | --- |
| [TensorBlock/awesome-mcp-servers](https://github.com/TensorBlock/awesome-mcp-servers) | 837 | 7 Sep 2026 | Active today. No CONTRIBUTING file — follow README format. |
| [MobinX/awesome-mcp-list](https://github.com/MobinX/awesome-mcp-list) | 880 | 30 Aug 2026 | Concise-entry list; keep the description short. |
| [apappascs/mcp-servers-hub](https://github.com/apappascs/mcp-servers-hub) | 331 | 5 Sep 2026 | No CONTRIBUTING file — follow README format. |

**Entry line for all three** (adjust to each README's column shape; check the exact format at
the insertion point first, since none of the three documents one):

```
- [Coordigent](https://github.com/ali8hsn/coordigent) - MCP server for shared file state, overlap warnings, and messaging between AI coding agents working in parallel on one GitHub repo. Works with Claude Code, Cursor, Codex, VS Code, Kiro, Windsurf and Perplexity.
```

**PR title:** `Add Coordigent — coordination MCP server for parallel coding agents`

**PR body:**

> Adds Coordigent, an MCP server that lets AI coding agents working in parallel on one GitHub
> repository see each other's file claims, receive a warning when their work overlaps, and
> message one another.
>
> Repository: https://github.com/ali8hsn/coordigent — public documentation, install guides for
> seven clients, and the full tool surface.
>
> Entry placed in <category>, alphabetical order preserved. Happy to adjust the wording or
> placement.

`wong2/awesome-mcp-servers` (4,293 stars) is listed here too but its last push was 13 July
2026. Worth a PR; expect it to sit.

---

## Tier 3 — checked and ruled out, with reasons

Recorded so nobody spends the evening rediscovering them.

| Target | Verdict |
| --- | --- |
| [jaw9c/awesome-remote-mcp-servers](https://github.com/jaw9c/awesome-remote-mcp-servers) (1,110 stars) | **Not eligible.** Its contributing rules state "Only OAuth 2.0, following the MCP spec is supported". Production `/mcp` uses a bearer token. Becomes eligible the day OAuth ships — and that is the same work Smithery needs, so the two share a trigger. |
| [docker/mcp-registry](https://github.com/docker/mcp-registry) (549 stars, pushed today) | **Probably blocked, worth asking.** Local route needs a Dockerfile in a *public* source repository; ours is private. Remote route needs "OAuth configuration details (if authentication is required)" — softer wording than Smithery's, so a maintainer may accept a bearer header. Also requires a consumable licence (MIT/Apache preferred). |
| [appcypher/awesome-mcp-servers](https://github.com/appcypher/awesome-mcp-servers) (5,764 stars) | **Archived.** Read-only; PRs cannot be merged. |
| [chatmcp/mcpso](https://github.com/chatmcp/mcpso) (2,105 stars) | **Abandoned.** Last push 26 March 2025. |
| [cline/mcp-marketplace](https://github.com/cline/mcp-marketplace) (785 stars) | **Stale.** Last push 24 June 2025. Low priority; submit only if the others are done. |
| [LobeHub](https://lobehub.com/mcp) | **No self-serve route found.** The page only invites you to "let us know" and they will add it. No form, no public submission repository located. |
| [PulseMCP](https://www.pulsemcp.com/submit) | **Unknown.** The submit page could not be fetched — `robots.txt` disallows it. Needs a human with a browser. |
| mcp.so | **Skip.** Paid placement. |
| [Smithery](https://smithery.ai/new) | **Blocked on auth scheme.** Requires OAuth for authenticated remote servers, or an MCPB bundle. See [seo-loop.md](../../.coordigent/messages/seo-loop.md). |
| [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers) (90,128 stars) | **Not assessed.** The community-server section's inclusion policy was not read in this session. High value if it accepts third-party entries — check before writing a PR. |
| [e2b-dev/awesome-ai-agents](https://github.com/e2b-dev/awesome-ai-agents) (29,921 stars) | **Not assessed.** Broader AI-agents list, not MCP-specific. Fit is plausible but unverified. |

---

## Competitive note from the recon

The neighbouring entries in the punkpeye diff are worth reading. Two direct competitors are
**already listed** in the same section:

- `danieldoderlein/llm-bus` — "atomic gap-free claims, advisory file leases, a shared event
  ledger, presence, prose handoffs, and a task graph, so multiple coding agents (Claude Code,
  Cursor, Codex) stop colliding". Remote Streamable HTTP, AGPL-3.0.
- `polymatx/dibs` — "TTL file claims stored in the git common dir (visible across every
  worktree instantly), enforcement hooks that block colliding edits in Claude Code and at
  commit time, agent presence, handoff notes". Single static binary, no server.

Both carry Glama badges, which is how they got merged. Both are in
[competitor-watch.md](competitor-watch.md) territory and neither was in the 6 September
research.

One incidental observation, offered as an observation only: the `llm-bus` entry contains the
words "hosted at llm-bus.com" and is merged and live. That does not disprove the Glama
phrasing rule, but it is worth knowing before treating the rule as absolute.
