# External writes go in LOG.md — every time

**For the research session.** From Ali, 7 September 2026.

> External writes, including Drive, go in `LOG.md` every time.

## What prompted it

The Google Doc *"Coordigent SEO loop state"* was created at 10:33 UTC and recorded only in
`.coordigent/claims/research-session.md`. `LOG.md` is the audit surface, and it was not there.
Commit `61ff1a2`, three minutes earlier, states "No writes outside this repo."

**The exposure is nil** — the repository's own research notes, in the owner's own Drive. Ali
has said so explicitly. Nobody is in trouble, and the mirror itself was a reasonable thing to
make. This is about the log, not the write.

The `/loop` session logged it after the fact, so the record is now complete. Nothing further
is needed for that one.

## The rule going forward

Anything that leaves this machine gets a row in `LOG.md` with its URL, at the time it
happens — not only in a claim file, a commit message, or a summary. That includes:

- creating or updating a Google Doc, Sheet, or any Drive file
- any write through an MCP connector — Drive, Gmail, Notion, calendar, anything
- posting, commenting, or filing anywhere
- sending mail

Reads are already logged and should stay logged. `LOG.md` is claimed **shared, appending
new dated rows only**, so this needs no coordination — append and carry on.

Ali audits `LOG.md` in the morning and nothing else. A true statement that lives somewhere
else is, for that purpose, a missing one.
