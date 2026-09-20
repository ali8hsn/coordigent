<!-- Mirrors the perplexity guide shown at https://coordigent.com/install -->
# Perplexity

## Install Coordigent first

One line per machine. It downloads `coord` and `coord-mcp` into `~/.tower/bin`, signs the
machine in with your own token, and registers Coordigent with every supported client it finds:

    curl -fsSL https://coordigent.com/install.sh | sh -s -- --token <your-token>

Get a command with your token already filled in at https://coordigent.com/install#get-command.
Then run `coord doctor`; a healthy setup reports PASS for Config, Server, and User MCP, and
names the clients Coordigent registered.

**Platform:** the installer and `coord` are used on macOS and Linux. **Windows is
untested** — not known to be broken, simply not verified, and the `curl … | sh`
one-liner above will not run on native Windows as written. Use WSL, or wait until
this note says otherwise.


`coord connect` does not register Perplexity — it only wires up Claude Code, Cursor,
Codex and Claude Desktop. Perplexity has no config file to merge into either; its
connectors are added through the app. So install Coordigent first, then run the command
below: it writes a launcher script and prints exactly what to type into the app.

    coord install perplexity

## What gets written

A small launcher, in the repo you ran it in: `.coordigent/perplexity-mcp.sh`

    #!/bin/sh
    cd '/Users/you/code/your-repo' || exit 1
    exec env 'CREWS_CLIENT=perplexity' '/Users/you/.tower/bin/coord-mcp'

The Perplexity helper does not inherit a repo working directory, so the launcher pins
one. That is also why the connector is bound to a single repo. No token is written into
it — `coord-mcp` reads credentials from `~/.tower/config.json`.

`coord install perplexity --user` puts the launcher under `~/.tower/perplexity/`
instead, named after a hash of the repo path, so several repos can each have their own
connector.

## Then add it in the app

The installer prints these lines; they are the whole setup:

    Perplexity Mac > Account settings > Connectors > Add Connector > Simple
    Install the PerplexityXPC helper when prompted.
    Server Name: Coordigent
    Command: /bin/sh '/Users/you/code/your-repo/.coordigent/perplexity-mcp.sh'
    Save; wait for Running; enable Coordigent under Sources.

There is no rules or steering file for Perplexity — it has nowhere to put one.

## Verify

Enable Coordigent under Sources, then ask Perplexity to call `coordigent.status`. Perplexity is
not installed on the machine these files were checked on: the generated launcher passes
a scripted stdio conformance run against the real server, but the Perplexity application
itself has not been exercised here.

## What degrades

The Perplexity adapter claims stdio and HTTP transport and nothing optional — no
resources, prompts, sampling, elicitation, roots or server notifications. It also cannot
be identified from its own `clientInfo`, which is why the launcher sets
`CREWS_CLIENT=perplexity`. Conflict notices never rely on any of that: they arrive as
banners on the result of whatever tool you just called, and stay readable in
`coordigent.message.inbox`.

## Remove

Delete the connector in Perplexity > Account settings > Connectors, then delete the
launcher script (`.coordigent/perplexity-mcp.sh`, or the file under `~/.tower/perplexity/`).
