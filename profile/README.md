# Synod

A small, consistent language for describing distributed systems. A Synod program is simulated deterministically and animated, so you can watch a protocol run, predict what happens next, break it and compare designs.

![Paxos in Synod: two proposers race, and every node ends with the same chosen value](paxos.gif)

Single-decree [Paxos](https://github.com/synodlang/examples/tree/main/paxos) from the examples, drawn by the lumen look in the chalk theme. Two proposers race with values x and y. The second learns of x during its prepare phase and proposes x too, so every node chooses x. Acceptors write their promises to disk before they reply, which keeps the run safe across crashes.

## A taste of Synod

This is the start of the gossip example. Nodes keep a table of what they know. A node's version combines its generation and its heartbeat, so a restarted node is believed again.

```synod
# package gossip
use std/disk
use std/lists
use std/net
use std/random
use std/time

digest has
  set known to {}

Node has
  set Generation to 0
  set Heartbeat to 0
  set Known to {}
  set Down to {}
  set peers to {}
  set seenAt to {}

define Join [n: Node] to [seed: node]
  set n.peers to {seed}

# Versions combine generation and heartbeat, so a restarted node is believed again
define [n: Node] Version
  result ((n.Generation times 1000000) plus n.Heartbeat)
```

Every line reads as pseudocode, and there is one way to write each thing. The compiler accepts only canonical form, and `synod fmt` produces it. The same program and the same seed always give the same run.

Learn it at **[synodlang.github.io](https://synodlang.github.io/)**: a [tutorial](https://synodlang.github.io/docs/v0.3/tutorial/) that builds Raft from an empty file one idea at a time, with every step editable and runnable in your browser, plus the [reference](https://synodlang.github.io/docs/v0.3/reference/), a [library](https://synodlang.github.io/docs/v0.3/library/) with a runnable example for every phrase, the [examples](https://synodlang.github.io/docs/v0.3/examples/), [guides](https://synodlang.github.io/docs/v0.3/guides/) and a page for every [error](https://synodlang.github.io/docs/v0.3/errors/).

Synod 0.3 adds themes. A look decides what to draw and a theme decides how it looks, so any look combines with any theme. The [looks](https://github.com/synodlang/looks) module has the looks lumen and doodle and the themes solarized (light and dark), terminal, sketch and chalk; the [gallery](https://synodlang.github.io/docs/v0.3/looks/gallery/) plays every pairing.

## Install

```
brew install synodlang/tap/synod
```

On Windows, use Scoop. On macOS or Linux you can also run the install script. See https://synodlang.github.io/install/ for every option.

```
scoop bucket add synodlang https://github.com/synodlang/scoop-bucket
scoop install synod
```

Check it with `synod version`. The latest release is [compiler v0.3.0](https://github.com/synodlang/compiler/releases/tag/v0.3.0), which implements Synod 0.3. On a Mac, the [Synod app](https://github.com/synodlang/mac-app/releases) adds an editor, a live stage, Predict, Break it and Compare, and creates a new workspace in one click.

## Repositories

| Repository | What it is | Status |
| --- | --- | --- |
| [dsl](https://github.com/synodlang/dsl) | The language specification, the tutorial and the implementation guides | v0.3.1 released |
| [compiler](https://github.com/synodlang/compiler) | The `synod` command: `new`, `fmt`, `check`, `run`, `get`, `doc`, `explain`, `mcp`, and `synod.wasm` | v0.3.0 released |
| [std](https://github.com/synodlang/std) | The standard library packages and the default theme | v0.3.0 released |
| [examples](https://github.com/synodlang/examples) | Sample programs and acceptance tests | v0.3.0 released |
| [looks](https://github.com/synodlang/looks) | The looks lumen and doodle and the themes solarized, terminal, sketch and chalk | v0.3.0 released |
| [player](https://github.com/synodlang/player) | Canvas library that plays `scene.json` | v0.3.0 released |
| [mac-app](https://github.com/synodlang/mac-app) | The Mac app | v0.3.0 released |
| [agent-skills](https://github.com/synodlang/agent-skills) | Skills for coding agents (Claude Code plugin and `AGENTS.md`) | v0.3.0 released |
| [synodlang.github.io](https://github.com/synodlang/synodlang.github.io) | The website and documentation | v0.3.0 live |
| [homebrew-tap](https://github.com/synodlang/homebrew-tap) | Homebrew formula for `synod` | Updated by compiler releases |
| [scoop-bucket](https://github.com/synodlang/scoop-bucket) | Scoop manifest for `synod` | Updated by compiler releases |
| [.github](https://github.com/synodlang/.github) | Organization profile and shared workflows | Available |

The order of work is in the [roadmap](https://github.com/synodlang/dsl/blob/main/implementation/10-roadmap.md).

## Links

- [The documentation](https://synodlang.github.io/docs/v0.3/): tutorial, reference, library, examples, guides and errors
- [The specification](https://github.com/synodlang/dsl), the source of truth for the language
- [Install](https://synodlang.github.io/install/)
- [Examples](https://github.com/synodlang/examples): TCP, gossip, Paxos, Raft, two-phase commit, consistent hashing, Cassandra, a web app and a write-ahead log
- [Releases](https://github.com/synodlang/compiler/releases)
- [Contributing](https://github.com/synodlang/.github/blob/main/CONTRIBUTING.md)

## Why Synod

Synod is named after the Synod protocol, the core consensus algorithm in Leslie Lamport's paper "The Part-Time Parliament" (ACM Transactions on Computer Systems, 1998; first submitted in 1990). The paper tells it as the story of an invented parliament on Paxos, a Greek island, whose part-time legislators could agree on decrees although they came and went; today the algorithm is known as Paxos. Lamport later explained it plainly in "Paxos Made Simple" (2001), and he received the 2013 ACM A.M. Turing Award for fundamental contributions to the theory and practice of distributed and concurrent systems. His "Time, Clocks, and the Ordering of Events in a Distributed System" (1978) and his TLA+ specification language shaped how we reason about such systems. We are grateful for his work, and we hope Synod honours it by making these ideas easier to watch and understand. Everything in this organization is built with that in mind.
