# Claim — research session (cloud, no GitHub credential)

**This session works only in `~/coordigent-docs-research` and will never write to `~/coordigent-docs`
again.** From 7 September 2026, 10:50 UTC. The `/loop` session collects its work with
`git pull ~/coordigent-docs-research main` before each fire; see the section this session added to
`.coordigent/messages/seo-loop.md`. The claims below still describe which paths it writes, because
both checkouts share one history and the same collisions are possible on merge.

Claimed 2026-09-07 10:20 UTC. Held until this session stops; if the timestamp above is more
than a few hours old and nobody is running, treat the claim as expired.

This session owns **research and drafting only**. It cannot push, open pull requests, submit
forms or send mail — it has no GitHub credential and no authority to file anything
externally. The desktop `/loop` session owns every external action.

## Paths claimed

| Path | Mode |
| --- | --- |
| `docs/seo/submission-research.md` | exclusive — new file, directory reconnaissance and payloads |
| `docs/seo/submission-queue.md` | **shared** — the /loop session's filing gate; appending candidate entries in its own template only |
| `docs/seo/citations/` | exclusive — new directory, assistant-answer baselines |
| `docs/seo/reply-queue.md` | exclusive — new file, drafted replies, never posted |
| `docs/seo/competitor-watch.md` | exclusive — new file |
| `docs/seo/name-collisions.md` | exclusive — new file |
| `docs/compare/crew-0xmmo.md` | exclusive — new file, written at Ali's request |
| `docs/compare/README.md` | **surgical** — one link added for the page above |
| `docs/seo/inbox-drafts.md` | **shared** — appending only, will not rewrite existing sections |
| `docs/seo/submission-results.md` | **surgical** — one paragraph only, the stale transport claim |
| `LOG.md` | **shared** — appending new dated rows only |

## Not claimed, deliberately

`.coordigent/messages/seo-loop.md`, `posts/`, `docs/install/`, the rest of `docs/compare/`, `README.md`,
`llms.txt`, `CHANGELOG.md` and anything under `docs/seo/` not listed above belong to the
`/loop` session. This session will not write them.

`.coordigent/messages/seo-loop.md` in particular: the Smithery correction this session was asked
to apply was already applied there in `6436099`, more completely than the version drafted in
`.coordigent/messages/handoff-from-session-b.md`. Nothing further is needed and this session left
it alone. The same correction is still outstanding in `docs/seo/submission-results.md`, which
is why that file appears above.

## Collision on 2026-09-07, and what it cost

**This session broke its own protocol once.** At 10:18 UTC the `/loop` session created
`docs/seo/submission-queue.md` as a filing gate — status values, a filed/blocked/skipped
table, and an entry template. This session claimed that path at 10:20 without re-checking,
then at 10:30 wrote the file with `cat >` and destroyed all 65 lines of it.

Recovered from `879e580` and restored. The two files were never the same thing: theirs is the
**gate** that decides what may be filed, this session's is the **research** behind the
entries. They now live at `submission-queue.md` and `submission-research.md` respectively,
and the gate links to the research.

The lesson is narrow and worth writing down: claiming a path is not the same as checking it.
A claim staked at 10:20 says nothing about a file created at 10:18. Read the working tree
immediately before writing, not only the claims directory — and prefer appending to
overwriting when another session is live.

This is the second collision between these two sessions today; the first destroyed a correct
comparison page. Both were caused by acting on a snapshot that had already gone stale.

## Protocol

Read this directory before touching a file. If a path is claimed by another session, skip it
and record the skip rather than writing anyway. Two sessions already collided on
`docs/compare/README.md` this morning; that is what this directory exists to prevent.

## Mirror

Everything this session has written is mirrored to one Google Doc, so none of it depends on
either checkout:

https://docs.google.com/document/d/195-zy06QYo4YwrM7iiY5Q2shBHfuVBRsr_fwUYDdXOo/edit

Rebuilt as a single document on 7 September 2026 at 10:45 UTC, owned by alihsn@utexas.edu. The
two earlier partial documents (10:33 and 10:39) are in Drive trash, recoverable if wanted.

The Drive connector available to this session can create documents and rename them but cannot
edit the content of one that already exists, so every refresh means a new document and a new
URL. **When that happens, this file and `.coordigent/messages/seo-loop.md` are the two places the
current URL is recorded** — update both. The repository copies remain authoritative; the mirror
is a snapshot and does not update itself.
