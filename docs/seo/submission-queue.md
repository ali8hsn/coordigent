# Submission queue

**The gate for item 3.** The external session files only what appears here with status
`ready`, one per fire, and flips it to `filed` with a URL afterwards. Anything not in this
file does not get submitted — no exceptions, no judgement calls at filing time.

The drafting session proposes entries. A human, or the drafting session with the human's
say-so, marks one `ready`. That split is the point: research and authorisation are separate
steps, and the session that can push is not the session that decides what is worth pushing.

The research behind every entry below — what each directory requires, and the exact text or
payload to submit — is in [submission-research.md](submission-research.md).

## Status values

| Status | Meaning |
| --- | --- |
| `candidate` | Found, not yet researched. Do not file. |
| `researched` | CONTRIBUTING read, scope confirmed to fit, entry text drafted. Still do not file. |
| `ready` | Approved for filing. The external session may take exactly one of these per fire. |
| `filed` | Submitted. Record the PR or confirmation URL and the date. |
| `skip` | Rejected. Record why, so it is not rediscovered next week. |

## PAUSED — 7 September 2026

**Item 3 is paused by instruction. File nothing new until the naming decision is made.**

Everything below stays as drafts. No entry may be marked `ready` while this notice stands, and
the two already filed (mcpservers.org, PR #13844) are unaffected — they are filed, not pending.

The reason is in [name-collisions.md](name-collisions.md): three independent collisions on the
name, one of which carries a trademark question. Filing fifteen more listings under a name that
may change would mean fifteen listings to correct or abandon.

## Ready to file

*(none)*

Nothing is approved for filing right now, so nothing will be filed this fire.

## Filed

| Directory | URL | Date |
| --- | --- | --- |
| punkpeye/awesome-mcp-servers | [PR #13844](https://github.com/punkpeye/awesome-mcp-servers/pull/13844) | 2026-09-07 |
| mcpservers.org | [Listing](https://mcpservers.org/servers/trycrews-com-install) | 2026-09-06 |

Full detail on both, including the entry text and the open questions, is in
[submission-results.md](submission-results.md).

## Blocked — do not mark ready yet

| Directory | Blocker |
| --- | --- |
| Glama | Account needed, and `ghcr.io/ali8hsn/coordigent:latest` is not published. Submitting before the image is public gives a listing whose build fails. **Now also gates PR #13844** — see below. |
| Smithery | MCPB bundle built and verified but not uploaded; the remote route needs OAuth and production is bearer-token. |
| jaw9c/awesome-remote-mcp-servers | Their contributing rules accept OAuth 2.0 only. Production `/mcp` is bearer-token, so ineligible until OAuth ships — same trigger as Smithery. |
| docker/mcp-registry | Local route needs a Dockerfile in a *public* source repository; ours is private. Remote route asks for OAuth details. Worth asking a maintainer, not worth filing blind. |

**PR #13844 is no longer merely open — it is blocked.** The repository's bot commented at
08:11 UTC on 7 September requiring a Glama listing plus a Glama score badge in the PR before
it will be merged. Glama therefore gates the 94,537-star listing, not just its own. Detail
and the exact badge format are in [submission-research.md](submission-research.md).

## Skipped

| Directory | Reason |
| --- | --- |
| mcp.so | Paid placement. |
| PulseMCP | Was "skipped by instruction". Re-checked 7 Sep: the submit page cannot be fetched — `robots.txt` disallows it. Needs a human with a browser before it can be judged. |
| appcypher/awesome-mcp-servers | Repository is archived. PRs cannot be merged. |
| chatmcp/mcpso | Abandoned; last push 26 March 2025. |
| LobeHub | No self-serve submission route found. The page only invites you to ask them to add it. |

## Entry template

Copy this per candidate. An entry without a fetched CONTRIBUTING link and a scope sentence
is not `researched`, whatever it says.

```
### <directory name>
- Status: candidate
- URL:
- CONTRIBUTING: <link actually fetched, and the date>
- Scope fits because: <one sentence quoting or citing their stated scope>
- Paid? no
- Entry text: <exactly what gets submitted; never "hosted at" or "at domain">
- Filed: —
```

## Candidates and researched entries

Proposed by the research session on 7 September 2026. **None is `ready`.** Full payloads,
CONTRIBUTING quotes and rejection reasons are in
[submission-research.md](submission-research.md).

### Official MCP Registry
- Status: researched
- URL: https://registry.modelcontextprotocol.io
- CONTRIBUTING: [publishing quickstart](https://github.com/modelcontextprotocol/registry/blob/main/docs/modelcontextprotocol-io/quickstart.mdx), fetched 2026-09-07
- Scope fits because: it is the canonical registry MCP clients read, "like an app store for MCP servers", and accepts remote servers via a `remotes` entry.
- Paid? no
- Entry text: the `server.json` in [submission-research.md](submission-research.md) — streamable-http at `/mcp` with a secret `Authorization` header. Needs no npm package, no Dockerfile and no OAuth, so unlike Smithery it is **not blocked**.
- Open question before `ready`: confirm the header name against the deployed endpoint. This session could not reach `coordigent.com` (`blocked-by-allowlist`) and saw only a 401 status, no headers.
- Filed: —

### TensorBlock/awesome-mcp-servers
- Status: researched
- URL: https://github.com/TensorBlock/awesome-mcp-servers (837 stars, pushed 2026-09-07)
- CONTRIBUTING: none in the repository; fetched 2026-09-07 and confirmed absent. Follow the README's own entry format.
- Scope fits because: it is a general awesome-list of MCP servers, and this is an MCP server.
- Paid? no
- Entry text: see the shared Tier 2 line in [submission-research.md](submission-research.md).
- Filed: —

### MobinX/awesome-mcp-list
- Status: researched
- URL: https://github.com/MobinX/awesome-mcp-list (880 stars, pushed 2026-08-30)
- CONTRIBUTING: none in the repository; fetched 2026-09-07 and confirmed absent. Concise-entry format — keep the description to one line.
- Scope fits because: general MCP server list.
- Paid? no
- Entry text: see the shared Tier 2 line in [submission-research.md](submission-research.md).
- Filed: —

### apappascs/mcp-servers-hub
- Status: researched
- URL: https://github.com/apappascs/mcp-servers-hub (331 stars, pushed 2026-09-05)
- CONTRIBUTING: none in the repository; fetched 2026-09-07 and confirmed absent. Follow the README's format.
- Scope fits because: general MCP server list.
- Paid? no
- Entry text: see the shared Tier 2 line in [submission-research.md](submission-research.md).
- Filed: —

### wong2/awesome-mcp-servers
- Status: candidate
- URL: https://github.com/wong2/awesome-mcp-servers (4,293 stars, last push 2026-07-13)
- CONTRIBUTING: not yet read.
- Scope fits because: general MCP server list. Last push is nearly two months old, so expect it to sit.
- Paid? no
- Filed: —

### modelcontextprotocol/servers
- Status: candidate
- URL: https://github.com/modelcontextprotocol/servers (90,128 stars)
- CONTRIBUTING: **not read.** Its community-server inclusion policy must be read before anything is drafted — high value, and easy to get wrong.
- Filed: —

### e2b-dev/awesome-ai-agents
- Status: candidate
- URL: https://github.com/e2b-dev/awesome-ai-agents (29,921 stars)
- CONTRIBUTING: not read. Broader AI-agents list, not MCP-specific; fit is plausible but unverified.
- Filed: —

### cline/mcp-marketplace
- Status: candidate
- URL: https://github.com/cline/mcp-marketplace (785 stars, last push 2025-06-24)
- CONTRIBUTING: not read. Stale for over a year; low priority.
- Filed: —
