# How Coordigent works

Coordigent is an MCP server. Your coding client already knows how to talk to MCP servers, so
Coordigent adds coordination without asking you to change editors, models, or git workflow.

## The problem it addresses

Two or more coding agents on one repository do not know about each other. Each has its own
context window, its own working copy, and no way to see what the others have touched. The
usual failure is quiet: two agents edit the same file from different starting points, and
whoever writes last wins. You find out at merge, or later.

Git already handles the merge. What git does not do is tell an agent, *while it is still
deciding what to edit*, that another agent is in that file right now.

## The pieces

### Shared file state

Every agent connected to the same repository reports the files it is working in. Coordigent keeps
that as one shared view, so any agent can ask what the rest of the team currently has open
rather than guessing from the last commit.

### File-conflict warnings

When an agent's work overlaps a file another agent is already in, Coordigent raises a warning.
These arrive as banners attached to the result of whatever tool the agent just called, and
they stay readable afterwards in `coordigent.message.inbox`.

The banner-on-result design is deliberate. MCP has optional capabilities — server
notifications, sampling, elicitation — that some clients implement and others do not. A
warning that rode on an optional capability would silently vanish on the clients that skip
it. Riding on the tool result means the warning arrives on every client that can call a tool
at all, which is all of them. The per-client notes in
[docs/install/](install/) list exactly what each client supports.

### Agent-to-agent messaging

Agents send each other messages with `coordigent.message.send` and read them with
`coordigent.message.inbox`. This is how an agent hands off work, asks another to hold off on a
file, or reports that a shared interface changed. Messages are addressed between sessions,
not broadcast into a chat log a human has to watch.

### One repository, many agents

Coordigent is built around a single existing GitHub repository with several agents on it, rather
than around giving each agent its own isolated universe. Nothing is migrated. The repository
stays where it is, on GitHub, with the history and permissions it already has.

### Directory

Coordigent also provides a directory where agents discover tools and capabilities.

## What it does not do

Being specific about this is more useful than a feature list.

- It does not merge code, run CI, or resolve conflicts for you. Git and your existing CI
  keep doing that.
- It does not host your repository. Your code stays on GitHub.
- It does not schedule, budget, or supervise agents. It does not decide which agent takes
  which task, cap anyone's spend, or verify that finished work is correct.
- It does not replace review.

A warning that two agents are in `src/auth.ts` is worth having before either of them
finishes. That is the job.

## Where the pieces live

`coord` and `coord-mcp` install into `~/.tower/bin`. Credentials live in
`~/.tower/config.json` and never in client config — every client config entry is just a
command path. See any guide under [docs/install/](install/) for the exact file each client
writes.
