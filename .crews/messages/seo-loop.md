# SEO loop → coding agents

Notes from the documentation and directory work that affect the product, not the docs.
Written 7 September 2026.

## Correction: Smithery and Glama have split apart again — two items, not one

**Supersedes the "one sprint item" note that was here earlier today.** That note said both
listings were gated on the same missing thing and should be tracked together. The artifacts
it asked for now exist, and with them in place the two blockers are no longer the same
blocker. Splitting them back apart is the correction.

Source for this: PR [#1 on the docs repo](https://github.com/ali8hsn/coordigent/pull/1) (branch
`registry/docker-and-mcpb`, commit `4f9776d`), open and unmerged at the time of writing.
That work reports:

- A root **`Dockerfile`** in the source repository. Built and run locally: the container
  answers `initialize`, lists 26 tools over stdio, and reaches `https://coordigent.com` — a
  deliberately wrong key returns `Unauthorized`, which is the hosted endpoint replying.
- **`dist/coordigent.mcpb`**, built by `bun run build:mcpb`, verified under Node 22: same
  `initialize`, same 26 tools, same reply from the hosted endpoint.

Both run `coord` in remote-client mode, take `CREWS_API_KEY` as their only required variable,
and use no database.

**One thing in the superseded note was simply wrong.** It said "`coord-mcp` is stdio, there
is no honest value to paste in that field." A production `/mcp` endpoint exists; it
authenticates with a Coordigent bearer token. The problem was never that we lack a remote
transport.

### Smithery — blocked on the auth scheme, not the transport

Production `/mcp` uses a bearer token, and Smithery requires **OAuth** for authenticated
remote servers. So the remote route stays shut until that changes. The **MCPB bundle is the
way in**, not the `/mcp` URL. The bundle has not been uploaded.

Known snag for whoever publishes it: the manifest deliberately declares no `tools` array,
because the Smithery registry validates MCPB tool entries as full MCP `Tool` objects and
returns HTTP 400 once per declared tool
([smithery-ai/cli#787](https://github.com/smithery-ai/cli/issues/787), open). Clients read
the live tool list over stdio regardless. Do not "fix" the manifest by adding the array.

### Glama — blocked on which repository holds the Dockerfile

Different problem entirely. Glama indexes `ali8hsn/coordigent`, which is documentation only. The
Dockerfile lives in the private source repository, so a Glama build from the public repo has
nothing to build. Two ways out, both operator decisions:

1. publish a prebuilt image to a public registry and point Glama at it, or
2. put a Dockerfile in the public repo that pulls that published image.

Nothing has been submitted or published, and no image has been pushed to any registry.

Glama also still needs an account before anything can be filed. The prepared listing copy is
in `docs/seo/submission-results.md`.

### Still true from the superseded note

Transport is becoming a listing-eligibility feature. Befall ships a local daemon plus a stdio
proxy and is listed on mcpservers.org; BountyVerdict, in the same Related Servers block,
advertises "Remote Streamable HTTP" explicitly.

## Docs discrepancy: Windows is neither claimed nor denied

Every install guide is written in macOS/Linux terms — `curl … | sh`, `~/.tower/bin`,
`/Users/you/.tower/bin/coord-mcp`. No guide states whether Windows is supported, and the
one-line installer as documented will not run on native Windows.

**Resolved for now, pending a real check.** All seven install guides, the FAQ and the README
now state plainly that macOS and Linux are what Coordigent is used on, that Windows is untested
rather than broken, and that the `curl … | sh` line will not run on native Windows as
written. That matches the 🍎 🐧 markers already on the awesome-mcp-servers entry, so no
change was needed there.

If a Windows check passes, three docs and one directory entry move together — do not update
one without the others.

Separately: that entry carries no programming-language marker, where nearly every
neighbouring entry does. If there is no objection to naming the implementation language
publicly, adding it makes the entry look less like a drive-by.

## Phrasing rule that now has teeth

Glama's spam filter reacts to "hosted at" and "at domain". The awesome-mcp-servers list
[syncs into the Glama directory](https://glama.ai/mcp/servers), so that rule applies to the
list entry too, not just to Glama's own form. The entry has been corrected on the branch.
Keep the phrasing out of any copy that could end up there.

## Competitors worth watching, from our own listing

mcpservers.org shows Related Servers on the Coordigent page. Two are direct:

- **[Befall](https://github.com/esenbora/befall-mcp)** — nearest competitor found. Same
  pitch, but claims are *refused at claim time* (first-writer-wins, TTL auto-release) rather
  than surfaced as warnings, with git dirty-path heartbeats as a backstop when an agent
  ignores the protocol. MIT, 14 `vs_*` tools, no commits since mid-August.
- **[Keelen](https://mcpservers.org/)** — "autonomous dev team steered from chat", GitHub
  repo in, merged PRs out, on your own model key. Different shape, same buyer.

The advisory-versus-enforced distinction is the sharpest question a prospect will ask after
seeing Befall. Worth an answer that is better than "warnings are safer."

## Needs a human — cannot be done from here

1. **Accounts on Glama and Smithery.** Both are behind a sign-up, and registering accounts is
   out of scope for an automated session.
2. **The Glama Dockerfile decision** — publish an image and point at it, or add a pulling
   Dockerfile to the public repo. Until one of those, Glama has nothing to build.
3. **Whether to pursue OAuth on `/mcp`** or accept that Smithery is an MCPB-bundle listing
   only.
4. **Merging or closing [PR #1](https://github.com/ali8hsn/coordigent/pull/1)**, which carries the
   Docker and MCPB documentation and is still open.
5. **The programming-language marker** for the awesome-list entry — only if there is no
   objection to naming the implementation language publicly.

Windows is settled for now: the guides, the FAQ and the README all say untested, which
matches the 🍎 🐧 markers already on the awesome-list entry. No change needed there. If
tomorrow's check passes, add 🪟 to that entry and reword all three docs together.

---

# Where the research session works now — read before each fire

*Added 7 September 2026 by the research session. This section is owned by that session; the
rest of this file belongs to the `/loop` session. Append below rather than rewriting here, and
a merge conflict in this block is the correct outcome rather than a silent loss.*

## Pull before each fire

**The research session no longer writes to `~/coordigent-docs`. It works only in its own checkout at
`~/coordigent-docs-research`, and commits there.** Before each fire, pull its work in:

```sh
cd ~/coordigent-docs && git pull ~/coordigent-docs-research main
```

Nothing it produces reaches `~/coordigent-docs` any other way. Skip the pull and you are working
from a stale tree — which is exactly how the two collisions below happened.

## Why the split exists

Two sessions wrote to `~/coordigent-docs` this morning and destroyed each other's work twice.

**First, a correct page.** The research session cloned at 04:55 CDT, two minutes before
`d0696e5` added `docs/compare/befall.md`. Working from that stale snapshot it searched for
"Befall", found nothing — the repository has no stars and does not surface on the obvious
queries — concluded the product did not exist, and in `7397570` rewrote `docs/compare/README.md`
to drop the link and assert that no such product could be located. The page it was contradicting
was in the working tree the whole time. Befall is real
([github.com/esenbora/befall-mcp](https://github.com/esenbora/befall-mcp)); `65ea420` restored
the link.

**Then, a filing gate.** At 10:18 UTC the `/loop` session created
`docs/seo/submission-queue.md` — status values, a filed/blocked/skipped table, an entry
template. The research session claimed that path at 10:20 without re-reading the tree and at
10:30 overwrote all 65 lines of it. Recovered from `879e580` and restored verbatim; the
research now lives separately in
[`docs/seo/submission-research.md`](../../docs/seo/submission-research.md) and the gate links
to it.

**The lesson, for whichever session reads this next:** claiming a path is not the same as
checking it. A claim staked at 10:20 says nothing about a file created at 10:18. Read the
working tree immediately before writing, not only `.coordigent/claims/`, and prefer appending to
overwriting whenever another session is live.

## What the research session owns

It writes only these, and only in its own checkout:

`docs/seo/submission-research.md`, `docs/seo/citations/`, `docs/seo/reply-queue.md`,
`docs/seo/competitor-watch.md`, `docs/seo/name-collisions.md`, `docs/compare/crew-0xmmo.md`,
and `.coordigent/claims/research-session.md`. It appends only to `docs/seo/inbox-drafts.md`,
`LOG.md`, this section of this file, and `docs/seo/submission-queue.md` (candidate entries in
your template, never marked `ready`). It made one surgical edit each to
`docs/seo/submission-results.md` and `docs/compare/README.md`.

Everything else — `posts/`, `docs/install/`, the rest of `docs/compare/`, `README.md`,
`llms.txt`, `CHANGELOG.md`, and the rest of this file — is yours and it will not touch them.

It has **no GitHub credential**: it cannot push, open pull requests, submit forms or send mail.
Every external action is yours.

## Off-repo mirror

Everything the research session has written is mirrored to one Google Doc, so none of it
depends on either checkout:

**https://docs.google.com/document/d/195-zy06QYo4YwrM7iiY5Q2shBHfuVBRsr_fwUYDdXOo/edit**

Rebuilt as a single document on 7 September 2026 at 10:45 UTC; the two earlier partial
documents are in Drive trash. The Drive connector cannot edit an existing document's content,
so each refresh creates a new document with a new URL — if this link is stale, the current one
is recorded in `.coordigent/claims/research-session.md`.

## Two things that changed today and affect your work

**Item 3 is paused.** No new directory submissions until the naming call is made.
`docs/seo/submission-queue.md` carries the notice; nothing is marked `ready`. The reason is
[`docs/seo/name-collisions.md`](../../docs/seo/name-collisions.md) — three independent
collisions on the name, one carrying a trademark question. Filing fifteen listings under a name
that may change means fifteen listings to correct or abandon.

**The correspondence address is now `ali8husn@gmail.com`.** The mcpservers.org listing was
created from `alihsn@utexas.edu`, so that is the address that owns it if it ever needs claiming
or correcting. The full split is in
[`docs/seo/submission-results.md`](../../docs/seo/submission-results.md).

Also worth your attention: **PR #13844 is blocked, not merely open.** The repository's bot
requires a Glama listing plus a score badge in the PR before it will merge, so Glama gates the
94,537-star listing and not just its own. And the **official MCP registry** is publishable via
its `remotes` route with no npm package, no Dockerfile and no OAuth — the exact `server.json` is
in `submission-research.md`. Both are on hold with the rest of item 3.
