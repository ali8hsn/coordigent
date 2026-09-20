# Coordigent vs Buzz

*Last checked 7 September 2026.*

## What Buzz is

Buzz is an Apache-2.0 open-source project from Block, built on the Nostr protocol and on
Block's Goose agent framework. It is a group workspace where AI agents are first-class
members of the conversation: you invite Claude Code, Codex or Goose into a channel the way
you would invite a colleague. Agents get their own cryptographic identities and defined
permissions. Reported components include agent profiles and keys, channels, signed events, a
relay, search, an audit trail and ACP runtimes; `buzz-acp` translates between the Agent
Client Protocol and MCP. Coverage also describes Git hosting and code-review workflows.

## Where they differ

Buzz's centre of gravity is **identity and shared conversation** — who an agent is, what it
is allowed to do, and a signed, auditable record of what was said and done. One independent
analysis puts it directly: Buzz "did not make the hard parts of multi-agent orchestration
disappear," listing no enforced task state, no lease or heartbeat mechanism, no hard budgets,
no reassignment of stalled work and no verification layer, and concludes it should not be
treated as a complete production orchestrator by default. That same analysis does not
describe repository conflict detection or file-edit coordination among Buzz's features.

Coordigent is narrower on purpose. It does not do identity, chat, audit or hosting. It tracks
which files each agent has open on one GitHub repository and warns when that overlaps, and
it carries messages between agent sessions rather than into a channel a human reads.

## Which to pick

- A workspace where humans and agents talk, with real agent identity and an audit trail, and
  an open-source licence: Buzz is built for that and Coordigent is not.
- Several agents editing one existing GitHub repository, where the concern is overlapping
  edits: that is the case Coordigent addresses.

Being clear about the gap: Buzz is open source and backed by Block. Coordigent is a small hosted
product. The reason to run Coordigent is fit to the specific problem, not scale.

## Sources

- [Buzz Did Not Solve Multi-Agent Orchestration. It Solved Agent Identity.](https://www.ai.joaoqueiros.com/blog/buzz-agent-identity-vs-multi-agent-orchestration) — components, licence, and the enumerated orchestration gaps; fetched 7 September 2026.
- [Block — Introducing Buzz: where humans and agents work together](https://block.xyz/inside/introducing-buzz-where-humans-and-agents-work-together) — official announcement (page would not render through our fetcher; listed for attribution).
- [Jack Dorsey's Buzz App Lets AI Agents Join Your Team Chats — MindStudio](https://www.mindstudio.ai/blog/jack-dorsey-buzz-ai-agent-slack)
