---
title: "Coordinate Claude Code and Cursor on One Codebase"
description: "Two engineers, two different agents, one repository. How to define a shared contract, expose editing intent across clients, and tell a warning apart from a guarantee."
keywords: [coordinate Cursor and Claude Code, Claude Code and Cursor same repo, AI agents overwriting files, MCP coordination]
date: 2026-09-21
author: Ali Hussain
---

# Coordinate Claude Code and Cursor on One Codebase

One engineer uses Claude Code. Another uses Cursor. Both know the repository, and both have an agent that can move through a task quickly. The awkward part starts when one session changes something the other session is still reasoning about. Neither engineer wants to spend the afternoon copying decisions between conversations.

The team does not necessarily need one standard editor. It needs a shared way to coordinate the work crossing those editors. That means identifying the same repository, exposing editing intent, and sending messages that explain dependencies while changes are still in progress.

I’m building Coordigent for this kind of situation. The example below is a proposed evaluation workflow, not a claim that every client configuration has been tested or that two agents will always produce compatible code. The distinction matters when deciding what to trust.

## Pick a dependency you can explain

Consider a small API change. Claude Code will update the server’s response type. Cursor will update a component that consumes it. The shared dependency is not simply a file name; it is the agreement about what the server returns and how the client handles it.

Write that agreement before asking either agent to implement the full change. Name the expected fields, error behavior, and test fixture. Decide which agent owns the first edit to the shared type. Give the other a task that can proceed without assuming the type has already changed.

This planning step does not need to be elaborate. Its purpose is to make one dependency explicit enough that a coordination message can refer to it. “Update authentication” is too broad. “Keep the response fixture stable until the new error field is agreed” gives both agents something they can act on.

## Understand what Coordigent adds

Coordigent is an MCP server for coordination among participating coding agents. It exposes shared file state, file claims, conflict warnings, and agent messages. `coord` is the installed binary. The repository remains in the team’s existing GitHub workflow; Coordigent is not a replacement Git host.

For this example, a claim tells Cursor that Claude Code intends to edit the shared type file. A conflict warning exposes a direct overlap if Cursor also needs that path. A message explains the decision that a file claim cannot fully express, such as the shape of the new response.

The clients still perform the coding work. Coordigent does not make Cursor control Claude Code or merge their reasoning into a single conversation. It supplies coordination information that each participating session can use. That narrower boundary is easier to test than a promise that two agents somehow become one team automatically.

## Keep identities and repository context separate

Each engineer should use their own access, and both should have appropriate membership in the same crew and registered repository. Sharing a token to make the demo easier hides an onboarding problem rather than solving it. It also makes it harder to understand which session represents which participant.

The local checkouts can differ. A shared repository is not the same thing as one shared working directory. Keep the branches or worktrees that suit your review process. What matters for coordination is that both sessions resolve the intended repository and use consistent repo-relative paths for the work.

Before any editing, ask each client to inspect the coordination state. If one points to another repo or does not appear as an active session, stop and fix that. Otherwise, an apparent absence of conflict may just mean the agents are looking at different coordination contexts.

## Install the same coordination server in both clients

The [Coordigent install guide](https://coordigent.com/install) describes a personalized command containing the user’s token. The live gate currently reports self-serve signup disabled, so the published article must be checked against the access flow before readers are told they can complete onboarding. Do not fill that gap with a guessed token or a shared credential.

With working access, install Coordigent on each machine and run `coord connect` inside the registered checkout. The current registrar writes a `coord` MCP entry in `~/.claude.json` for Claude Code and `~/.cursor/mcp.json` for Cursor. Its command points to the installed `coord-mcp` executable on that machine.

Run `coord doctor`, inspect the generated configuration, and restart both clients. Preserve other MCP entries. Configuration is not complete simply because a file exists: confirm that the clients can load the tools and that their sessions resolve the right repo.

## Make the first claim deliberately

Use a small test change, preferably in a disposable fixture. Ask Claude Code to register its session and claim the shared type or fixture before editing. Keep the session active with heartbeats. Then ask Cursor to check its intended paths and inspect the existing claim.

Observe what actually happens. Can Cursor see the overlap? Does it respond by changing the plan, waiting, or messaging the peer? Does the configured hook intercept the edit you expected it to intercept? These are separate questions, and a successful MCP connection does not answer all of them.

Do not begin by testing an overwrite against valuable uncommitted work. The point is to understand the mechanism safely and clearly. You need a baseline diff and a file whose intended owner is obvious, so unexpected behavior can be attributed to a specific step.

## Send a message that changes the next action

A useful message contains a decision or a dependency. In the API example, Claude Code might tell the other session that the response will include a nullable error field and that the fixture is ready for review. Cursor can then update its component against that agreed shape.

Avoid turning coordination into a second stream of narration. “Still working” does not help another agent decide what to edit. A note about the exact shared contract does. If the contract changes again, the message should identify what changed and which dependent work needs attention.

Release the claim when the handoff is ready. The next agent should not have to infer ownership from silence. If both still need the file, decide the order instead of hoping they will independently produce equivalent changes. Messaging provides the channel; the work still needs an explicit coordination decision.

## Separate warnings from guarantees

File claims reveal declared intent. They do not capture every possible semantic dependency, manual edit, or unconnected tool action. Two agents can touch different files and still disagree about behavior. An expired claim can also look different from an active session that is deliberately holding ownership.

Treat the first run as an integration test of the workflow. Confirm session registration, repository context, claim visibility, messages, and release. Test automatic interception separately if your client configuration relies on it. Do not turn a tool response into a blanket promise that overwrites cannot happen.

The same caution applies to model choice. Shared coordination does not require the agents to use the same model, but it does require them to follow the participation process. Different clients may expose tools or hooks differently. Verify the installed versions rather than assuming identical behavior everywhere.

## Review the server and client changes together

Once the handoff is complete, inspect the combined behavior. Does the server return the agreed shape? Does the component handle its error case? Does the fixture represent the real contract? Run the tests that cross the boundary, not only each task’s local checks.

This is also where you evaluate whether the coordination was useful. Did Cursor avoid implementing against an assumption that was about to change? Did the ownership message remove ambiguity? Did an engineer still have to relay every decision by hand? Record those observations without inventing an efficiency percentage.

If the task was too tightly coupled, sequencing more of it may be the correct result. A successful coordination tool should help the team make that choice. It does not need to make every pair of tasks suitable for parallel execution to be useful.

## Keep the tools, improve the handoff

Standardizing on one coding client would not automatically create shared editing intent. Keeping different clients does not have to mean keeping every agent isolated. The practical middle ground is a small, explicit coordination workflow around the parts of the repository that multiple sessions touch.

Start with one shared fixture and two active sessions. Once the behavior is clear, expand to a real dependency. The directory can help agents discover other capabilities later; it is not a substitute for establishing this basic handoff first.

The [free solo entry point](https://coordigent.com/install#get-command) is available through the install guide when self-serve access is enabled. Team pricing remains a $20-per-seat monthly preview. Before recommending a team rollout, verify the full access flow and the actual client behavior with two participating sessions.
