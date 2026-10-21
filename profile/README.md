# Synod

A small, consistent language for describing distributed systems. A Synod program is simulated deterministically and animated, so you can watch a protocol run, predict what happens next, break it and compare designs.

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

The state today: `synod fmt`, `synod check` and `synod run` work. The animation, the player, the Mac app and the full site are still to come.

## Install

```
brew install synodlang/tap/synod
```

On Windows, use Scoop. On macOS or Linux you can also run the install script. See https://synodlang.github.io/install/ for every option.

```
scoop bucket add synodlang https://github.com/synodlang/scoop-bucket
scoop install synod
```

Check it with `synod version`. The latest release is [compiler v0.2.2](https://github.com/synodlang/compiler/releases), which implements Synod 0.2.

## Repositories

| Repository | What it is | Status |
| --- | --- | --- |
| [dsl](https://github.com/synodlang/dsl) | The language specification and implementation guides | Spec v0.2 |
| [compiler](https://github.com/synodlang/compiler) | The `synod` command: `fmt`, `check`, `run` | v0.2.2 released |
| [std](https://github.com/synodlang/std) | The standard library packages | In use by the compiler |
| [examples](https://github.com/synodlang/examples) | Sample programs and acceptance tests | Available |
| [player](https://github.com/synodlang/player) | Canvas library that plays `scene.json` | Planned (M7) |
| [mac-app](https://github.com/synodlang/mac-app) | The Mac app | Planned (M8, M9, M10) |
| [agent-skills](https://github.com/synodlang/agent-skills) | Skills for coding agents | Planned (M10) |
| [synodlang.github.io](https://github.com/synodlang/synodlang.github.io) | The website and documentation | Install page live; rest planned (M11) |
| [homebrew-tap](https://github.com/synodlang/homebrew-tap) | Homebrew formula for `synod` | Updated by compiler releases |
| [scoop-bucket](https://github.com/synodlang/scoop-bucket) | Scoop manifest for `synod` | Updated by compiler releases |
| [.github](https://github.com/synodlang/.github) | Organization profile and shared workflows | Available |

The order of work is in the [roadmap](https://github.com/synodlang/dsl/blob/main/implementation/10-roadmap.md).

## Links

- [The specification](https://github.com/synodlang/dsl), the source of truth for the language
- [Install](https://synodlang.github.io/install/)
- [Examples](https://github.com/synodlang/examples): TCP, gossip, Paxos, Raft, two-phase commit, consistent hashing, Cassandra, a web app and a write-ahead log
- [Releases](https://github.com/synodlang/compiler/releases)
- [Contributing](https://github.com/synodlang/.github/blob/main/CONTRIBUTING.md)

## Why Synod

Synod is named after the Synod protocol, the core consensus algorithm in Leslie Lamport's paper "The Part-Time Parliament" (ACM Transactions on Computer Systems, 1998; first submitted in 1990). The paper tells it as the story of the parliament of the ancient Greek island of Paxos, whose part-time legislators could agree on decrees although they came and went; today the algorithm is known as Paxos. Lamport later explained it plainly in "Paxos Made Simple" (2001), and in 2013 he received the ACM A.M. Turing Award for fundamental contributions to the theory and practice of distributed and concurrent systems. His "Time, Clocks, and the Ordering of Events in a Distributed System" (1978) and his TLA+ specification language shaped how we reason about such systems. We are grateful for his work, and we hope Synod honours it by making these ideas easier to watch and understand. Everything in this organization is built with that in mind.
