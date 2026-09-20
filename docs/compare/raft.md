# Coordigent vs Raft

*Last checked 7 September 2026 against [raft.build](https://raft.build/).*

## What Raft is

Raft is a multi-agent collaboration platform — a shared workspace where humans and agents
work together. Its own site describes channels and threads, tasks that agents claim and run
in parallel, @mentions for directing work between agents, Joint Channels for human-agent
teamwork, agent reminders, and basic observability. It lists support for Claude, Codex,
DeepSeek and Hermes, plus external agents via connection guides.

Raft's pricing is a free tier (1 Joint Channel for a limited time, 30-day history, 100 MB of
uploads per month) and a Pro tier at $8.80 per seat per month billed annually, with
Enterprise listed as coming soon.

## The honest overlap

Both products exist because agents working in parallel cannot see each other, and both
provide agent-to-agent messaging. If what you need is a place where agents and people talk,
claim tasks and hand work off, those are Raft's central features and it is built around them.

## Where they differ

Raft organises work around a **workspace**: channels, threads, tasks, message history. Coordigent
organises around a **repository**: which files each agent currently has open, and a warning
when one agent's work overlaps another's. Raft's public page does not say whether it tracks
file-level state or detects overlapping edits, and does not specify whether it uses git
worktrees or branches.

Coordigent installs as an MCP server into the client you already use, so coordination shows up
inside the agent's own tool list rather than in a separate application. Raft is a platform
you also work in.

## Which to pick

- Team coordination, task hand-off and a shared human/agent workspace: Raft is designed for
  that and is cheaper per seat.
- Several agents editing one existing GitHub repository, where the thing you fear is two
  agents in the same file: that is what Coordigent watches.

They are not mutually exclusive.

## Sources

- [raft.build](https://raft.build/) — features, supported agents and pricing, fetched 7 September 2026.
- [Raft 1.0 puts AI agents in Team Mode — TestingCatalog](https://www.testingcatalog.com/raft-1-0-puts-ai-agents-in-team-mode/)
