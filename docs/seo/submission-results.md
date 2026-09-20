# Directory submissions

Status of every directory, awesome-list and registry Coordigent has been submitted to. Newest
activity first. Contact email is withheld here because this repository is public; it is
recorded in the private tracker.

| Directory | URL | Status | Last checked |
| --- | --- | --- | --- |
| punkpeye/awesome-mcp-servers | [PR #13844](https://github.com/punkpeye/awesome-mcp-servers/pull/13844) | **Open** — awaiting maintainer review | 2026-09-07 |
| mcpservers.org (wong2) | [Listing](https://mcpservers.org/servers/trycrews-com-install) | **Listed** — live, docs rendering from this repo | 2026-09-07 |
| Glama | https://glama.ai/mcp/servers | Not submitted — account required, submission fields not yet seen | 2026-09-06 |
| Smithery | https://smithery.ai/new | Blocked — see below | 2026-09-06 |
| mcp.so | — | Skipped: paid placement | 2026-09-06 |
| PulseMCP | — | Skipped | 2026-09-06 |

## Rename to Coordigent — 2026-09-20

The product is Coordigent; the binaries are `coord` and `coord-mcp`; the domain is
coordigent.com. This repository was renamed `ali8hsn/crews` -> `ali8hsn/coordigent`
(GitHub 301s the old URL, verified) and its README, docs and posts were rewritten.

Directory state after that rename:

| Directory | What it shows now | Who can fix it |
| --- | --- | --- |
| Glama ([listing](https://glama.ai/mcp/servers/ali8hsn/crews)) | Old README: "Crews", "Tower is the installed binary", trycrews.com | **Unclaimed.** Claiming is free and is done by signing in with the GitHub account that owns the repository — no form. Claim it, then use Profile to fix the displayed name and Repository syncs to request a re-sync rather than waiting for the scheduled crawl. |
| mcpservers.org ([listing](https://mcpservers.org/servers/trycrews-com-install)) | Old README, title still "Crews MCP Server" | The page has a **Request update** link. That is how the source was switched to this repository on 7 September, and the maintainer answered within the hour. The slug `trycrews-com-install` is the permalink and will not change. |
| punkpeye/awesome-mcp-servers | **Fixed.** [PR #13844](https://github.com/punkpeye/awesome-mcp-servers/pull/13844) is retitled "Add Coordigent MCP coordination server" and its entry now links `ali8hsn/coordigent`. | Done, still awaiting maintainer review. |

That PR mattered most: the list is synced to Glama, so merging it unchanged would
have published the old name a second time rather than corrected the first.

Search engines were not touched and do not need to be. They re-crawl; the earlier
entries below are kept as the record of what was true when they were written.

## Details

### punkpeye/awesome-mcp-servers — open

PR #13844, opened 2026-09-07 by `ali8hsn`, titled "Add Coordigent MCP coordination server 🤖🤖🤖".
This became possible only once this documentation repository was made public;
[their CONTRIBUTING](https://github.com/punkpeye/awesome-mcp-servers/blob/main/CONTRIBUTING.md)
requires a repository link, and previously there was no public repository to give.

**Title emoji: verified correct, no change needed.** An earlier note here guessed that the
`🤖🤖🤖` were attribute markers. They are not — they are documented in
[CONTRIBUTING](https://github.com/punkpeye/awesome-mcp-servers/blob/main/CONTRIBUTING.md):
automated agents append `🤖🤖🤖` to the PR title to opt into a fast-tracked merge process.
The title is right as filed.

**One fix was pushed to the branch** ([a73d749](https://github.com/punkpeye/awesome-mcp-servers/pull/13844/commits)).
The entry read "...; hosted at coordigent.com with a free solo tier." That list is
[synced to the Glama directory](https://glama.ai/mcp/servers), and "hosted at" is one of the
phrasings Glama's spam filter reacts to. It now reads ". Free solo tier; team pricing in
preview."

Still worth a human eye: the entry carries no programming-language marker, where nearly every
neighbouring entry does, and it claims 🍎 🐧 but not 🪟. Both are easy to correct if Windows
is supported and the language is one you want stated publicly.

### mcpservers.org — listed and live

Their README directs contributors to the form rather than accepting PRs. Free submission,
premium unchecked, no fee paid.

The listing is live at
[mcpservers.org/servers/trycrews-com-install](https://mcpservers.org/servers/trycrews-com-install)
under Development. It originally showed "No documentation available" because its source was
the website rather than a repository; a request to switch the source to this repository was
sent on 7 September at 08:20 UTC and the maintainer replied "Updated" at 08:57 UTC. Verified
in a browser the same day: the page now renders this repository's README in full, and the
sidebar shows the GitHub repository as its source.

That host returns HTTP 403 to automated fetches, so this had to be checked in a real browser.
A 403 there is not evidence of absence.

### Glama — account required

Submission is behind Add Server, which requires an account. Post-login field labels are
unknown, so no claim is made about them.

> **Filter note:** Glama's spam filter reacts to the phrasings "hosted at" and "at domain".
> Do not use either in a description.

### Smithery — blocked on packaging, not on login

Sign-in is required, but the real blocker is downstream: the server URL field must be a
working public HTTPS MCP endpoint, not a marketing site. A Streamable HTTP endpoint does
exist at `https://coordigent.com/mcp` and returns 401 to an unauthenticated request, so the
transport was never the problem. It authenticates with a **bearer token**, and Smithery
requires OAuth for authenticated remote servers. The MCPB bundle is therefore the way in
rather than the URL; a bundle has been built on branch `registry/docker-and-mcpb` but not
uploaded.

Documented routes out, per [Smithery's publish docs](https://smithery.ai/docs/build/publish):
a Streamable HTTP URL, or a local MCPB bundle. Logging in does not resolve this.

## Contact address — which listing is tied to which

**From 7 September 2026, `ali8husn@gmail.com` is the address for all registry and directory
correspondence.** Use it for every new submission.

Existing listings are split across two addresses, which matters when a maintainer wants to
verify that a submitter owns what they are submitting, and again whenever a listing has to be
corrected or claimed later:

| Listing or thread | Address on file |
| --- | --- |
| mcpservers.org — the [listing](https://mcpservers.org/servers/trycrews-com-install) and the "Update source" thread of 7 September | `alihsn@utexas.edu` |
| punkpeye/awesome-mcp-servers [PR #13844](https://github.com/punkpeye/awesome-mcp-servers/pull/13844) | GitHub account `ali8hsn`; no email exchanged |
| Everything filed from 7 September onward | `ali8husn@gmail.com` |

The mcpservers.org listing is the one to watch: if it ever needs claiming or correcting, the
address that owns it is the UT one, not the gmail one. Worth either migrating it deliberately
or simply remembering which key opens which door.

## Standard description

Use verbatim where a description is requested:

> MCP server for shared file state, overlap warnings, and messaging between AI coding agents
> working in parallel on one GitHub repo.
