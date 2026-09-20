# Handoff from session B

A second overnight session (not the `/loop` session) was running against this repository
between 04:55 and 05:13 on 7 September 2026. It has been shut down; the `/loop` session owns
this repository. This file is the whole of what it left behind, so nothing has to be
reconstructed from the log.

Session B had **no GitHub credential**: it could commit locally and nothing else. It never
pushed, opened a pull request, submitted a form, posted a message or sent mail.

## Commits

Both are already on `main`. They carry a `+0000` timezone, which is how to tell them apart
from the `/loop` session's `-0500` commits.

- `7397570` — Add CLI reference and three sourced comparisons; drop unsourceable competitor.
  Adds `docs/cli.md` (both binaries, their flags, and the full `coordigent.*` tool surface,
  verified against `packages/cli/src` and `packages/mcp/src`), plus
  `docs/compare/mcp-agent-mail.md`, `docs/compare/agent-orchestration.md` and
  `docs/compare/entire.md`, each sourced against pages fetched that morning. Also rewrote
  `docs/compare/README.md` and updated the comparison links in `README.md` and `llms.txt`.
  **This commit contains the mistake described below.**
- `65ea420` — Restore the Befall link removed in error. Corrects `docs/compare/README.md`
  only.

## The Befall collision

Worth reading, because it is the exact failure this product exists to prevent, and it
happened here between two agents on one repository.

Session B cloned at 04:55. Two minutes later the `/loop` session committed `d0696e5`, adding
`docs/compare/befall.md`. Session B never saw it. Working from its stale snapshot, it
searched for "Befall", found nothing — the repository has no stars and does not surface on
the obvious queries — concluded the product did not exist, and in `7397570` rewrote
`docs/compare/README.md` to drop the link and state that no such product could be located.
The page it was contradicting was sitting in the working tree, correct, the whole time.

Befall is real. `github.com/esenbora/befall-mcp` was verified independently: MIT, tagline
"multiplayer coordination for AI coding agents", Claude Code / Codex CLI / Cursor, path-glob
locks refused at claim time with TTL auto-release, 14 `vs_*` tools. The existing page is
accurate. `65ea420` restored the link and the "closest comparison" framing.

Nothing else from `7397570` is affected — the three new comparison pages and `docs/cli.md`
do not touch Befall. But `docs/compare/README.md` was rewritten twice in ninety seconds, so
it is the one file worth re-reading before it is trusted.

## The seo-loop.md correction, ready to paste

Ali's correction, given at 05:10: production already exposes Streamable HTTP on `/mcp`. The
Smithery blocker is the **bearer-token auth scheme** — they want OAuth or an MCPB bundle —
not the transport. `.coordigent/messages/seo-loop.md` still says the opposite, and so does
`docs/seo/submission-results.md` (the paragraph beginning "The current server uses stdio
transport").

Session B did not apply this, because the `/loop` session was actively rewriting that file
and a write would have collided a second time.

Evidence gathered before shutting down, both independent of the source tree claim:

- `GET https://coordigent.com/mcp` returns **401**, not 404. The endpoint exists and it
  authenticates. Checked 7 September 2026, read-only.
- `apps/server/src/app.ts:118` reads `app.all("/mcp", bearerAuth, createMcpHandler())` —
  bearer token, not OAuth.
- Direct verification of the deployed endpoint beyond the status code was not possible from
  that session: `coordigent.com` is not on the egress allowlist in either the container or the
  device VM, so `curl` got `blocked-by-allowlist`. The 401 above came through the page
  fetcher. Anyone re-checking this from a session with the domain allowlisted should read
  the `WWW-Authenticate` header directly and settle it properly.

Replacement text for the `### Smithery needs a transport we do not ship` section, retitled:

> ### Smithery needs an auth scheme we do not ship
>
> Not a transport problem. Production already serves Streamable HTTP at
> `https://coordigent.com/mcp`; `apps/server/src/app.ts` routes it with
> `app.all("/mcp", bearerAuth, createMcpHandler())`, and an unauthenticated GET returns 401,
> so the endpoint is live and authenticating.
>
> What Smithery will not take is the **bearer token**. Per
> [their publish docs](https://smithery.ai/docs/build/publish) an authenticating endpoint
> must use OAuth, or the server must ship as a prebuilt **MCPB bundle**. So the choice is:
>
> - add an OAuth authorization-server path in front of `/mcp`, keeping bearer for existing
>   clients; or
> - build an MCPB bundle, which is the cheaper route to the same listing and does not touch
>   the running service; or
> - mark Smithery "won't do" rather than leaving it as a pending task.
>
> Glama is gated on an account, not on this, so the two should be tracked separately again.

And in `docs/seo/submission-results.md`, the sentence "The current server uses stdio
transport. There is no verified Streamable HTTP endpoint (with OAuth if authentication is
required) and no prebuilt MCPB bundle, so there is no honest value to paste" should become:
"A Streamable HTTP endpoint exists at `https://coordigent.com/mcp` and returns 401 to an
unauthenticated request. It authenticates with a bearer token; Smithery requires OAuth or a
prebuilt MCPB bundle, and neither exists yet."

One standing rule, from how the above went wrong: when a claim depends on what production
does, check production, not the source tree.
