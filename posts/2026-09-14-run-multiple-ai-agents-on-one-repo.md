---
title: "Run Multiple AI Agents on One Repo"
description: "A concrete workflow for running several AI coding agents on one codebase: separating git isolation from live coordination, choosing task boundaries, making editing intent visible, and testing an overlap before you trust any of it."
keywords: [run multiple AI agents on one codebase, parallel AI coding agents, multi-agent coding workflow, MCP server for teams]
date: 2026-09-14
author: Ali Hussain
---

# Run Multiple AI Agents on One Repo

Two engineers can give their agents sensible tasks and still end up with changes that do not fit together. One session updates a shared type. Another writes a client against the old shape. A third rewrites a fixture both changes depend on. Every agent can explain its local decisions, but nobody has the whole picture while the work is happening.

Running multiple AI agents on one codebase is therefore not just a scheduling problem. It is a coordination problem. You need a way to make intended work visible, resolve overlapping ownership, and communicate decisions before another session builds on an outdated assumption.

I’m building Coordigent around that problem. This article describes a workflow you can evaluate, including what it does not solve. It is not a report of measured productivity gains or a promise that parallel development can become conflict-free.

## A shared repository is not a shared plan

Git tells you about recorded changes. It does not automatically tell an agent what another session intends to edit next. A clean branch can still contain a plan that overlaps with another engineer’s work. Likewise, two branches that merge without textual conflicts can disagree about behavior.

Imagine one agent changing an authentication helper to return a different result shape. Another agent touches only a caller. The file sets might not overlap, yet the changes are coupled. File ownership would help identify direct collisions, but communication is still needed to explain the interface decision.

This is why “give every agent its own branch” is useful but incomplete. Branches organize changes. They do not eliminate dependencies between those changes. Keep that isolation where it helps, then add a coordination process around the work that crosses it.

## Start with tasks that can be separated

Before starting agents, describe the boundary of each task. Name the expected files or directories, the shared interfaces involved, and what would count as completion. This is a planning exercise, not a claim that an agent can know its entire file set in advance.

For example, one session might implement a response parser while another builds tests against an agreed fixture. The shared fixture is the obvious coordination point. Decide who owns its format and how the other session will learn about changes. If both tasks require rewriting the same central module, consider sequencing that part instead of forcing concurrency.

Do not maximize the number of active agents as an end in itself. Parallel work is useful when independent progress exceeds the cost of coordinating dependencies. A task that is too tightly coupled may be faster to handle in order.

## Make editing intent visible

Coordigent is an MCP server that exposes shared file state, claims, conflict warnings, and messages between participating agents. `coord` is the binary you install. The product’s immediate job is to let a session discover work that would otherwise be invisible outside another agent’s conversation.

Before editing a path, an agent checks whether another session has claimed it. A claim describes intended work. When claims overlap, the conflict response gives the agents a reason to stop and coordinate, choose another path, or sequence the changes.

That is different from claiming universal write protection. A manual edit, an unconnected tool, or a session that skips the coordination process may not participate. Hook behavior also depends on the installed client configuration. Verify what happens with the actual tools you use rather than inferring protection from an MCP connection appearing in a settings screen.

## Give overlapping work an owner

Once an overlap appears, decide what should happen. “There is a conflict” is useful information, but it is not a resolution. One session might finish the common helper first. Another might move to tests that do not require that helper yet. Sometimes the right decision is to combine the tasks.

Use a short message with an actionable dependency: “I’m changing the parser result shape. Wait on the caller until I send the agreed fields.” That says more than a generic status update. It tells the other agent what to avoid and what signal will make the work available again.

Release ownership deliberately when the change is ready for handoff. If the design changes midway, update the coordination message. A claim should not become a substitute for explaining the part of the work that another session actually depends on.

## Connect the first two sessions

Start with the [Coordigent install guide](https://coordigent.com/install). The intended self-serve flow supplies a personalized install command after sign-in, with the user’s token already included. At the time of writing, the live access screen reports that self-serve signup is disabled. Do not treat the proposed install journey as available until that has been resolved.

For an account with working access, install Coordigent on each development machine. Use a repository registered with the appropriate crew. Run `coord connect` inside that checkout, then run `coord doctor`. Inspect the generated MCP configuration and any client hooks before starting the test.

The current registrar writes JSON MCP entries for Claude Code and Cursor, and a TOML entry for Codex. Keep credentials personal. Copying one engineer’s token to another machine is not a team onboarding process. Restart the clients and confirm that both sessions identify the same registered repository.

## Test an overlap before trusting the workflow

Use a disposable fixture instead of an important uncommitted file. Start two participating sessions. Ask the first to register, claim the fixture, and keep its heartbeat active. Ask the second to check that path before editing. Confirm that the second session can see the overlap.

Then test the handoff. Have the agents exchange a message agreeing on ownership. Release the first claim and confirm that the other session can proceed through the expected workflow. Inspect the actual diff. You want evidence that the intended sequence happened, not just a successful installation message.

Repeat the check after restarting one client. This can expose assumptions about working directories, saved configuration, or session registration. If a client cannot resolve the correct repository, fix that before giving it real shared work. The test should be small enough that a failure is easy to understand.

## Keep the coordination state current

Claims describe live work, so session freshness matters. Coordigent uses heartbeats to maintain active coordination state. A session that stops participating should not be treated as a permanent owner of a file. Conversely, an empty view does not prove that no person or unconnected tool is making changes.

Build registration, checks, claims, messages, and release into the agent’s working instructions. Then observe whether the client follows them. MCP tool availability and reliable tool use are separate things. If the workflow depends on a person remembering to relay every event, you have recreated the original coordination burden in another place.

Keep the first evaluation focused. The directory can help agents discover additional tools and capabilities, but adding more tools will not repair unclear ownership. Establish the shared-repo workflow before expanding the number of agents or the scope of their tasks.

## Review the combined behavior

File coordination does not replace tests. Two agents can respect ownership perfectly and still implement incompatible behavior. Review the combined diff, run the relevant checks, and inspect interfaces that connect the tasks. Pay particular attention to assumptions that live in different files.

Use the same distinction when evaluating results. Did the agents notice direct overlap earlier? Did a message change what another session did? Was the handoff understandable? Those are coordination observations. They do not establish a percentage productivity improvement, and they should not become a score for individual engineers.

If the experiment fails, keep the failure concrete. A missing claim, stale session, wrong repo, ignored warning, and bad design decision require different fixes. Grouping them all under “agents do not collaborate” makes it harder to identify what the workflow actually needs.

## One repo, many agents, a visible plan

The useful goal is not to keep every agent busy. It is to let agents make progress without forcing engineers to reconstruct each other’s intentions afterward. Start with two sessions, a small dependency, and a visible handoff. Expand only when that interaction is understandable and repeatable.

Coordigent is intended to add that coordination to the coding clients and repositories a team already uses. The free solo tier is the starting point for evaluation once access is available. Team pricing is currently a $20-per-seat monthly preview, and paid billing is not yet available.

Visit the [install guide](https://coordigent.com/install#get-command) for the current access and setup flow. Keep the first test small enough to show exactly what a claim, a warning, and a message changed about the work.
