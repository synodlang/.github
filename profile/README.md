# Synod

A small, consistent language for watching distributed systems think.
Describe a protocol or a system design as Synod packages; it is simulated
deterministically and animated, so you can predict, break and compare.

| Repository | What it is |
| --- | --- |
| [dsl](https://github.com/synodlang/dsl) | The specification (start here) |
| [compiler](https://github.com/synodlang/compiler) | The `synod` command, native and WebAssembly |
| [std](https://github.com/synodlang/std) | The standard library |
| [examples](https://github.com/synodlang/examples) | Sample programs |
| [player](https://github.com/synodlang/player) | The animation player, shared by the app and the site |
| [mac-app](https://github.com/synodlang/mac-app) | The Mac app |
| [agent-skills](https://github.com/synodlang/agent-skills) | Skills for coding agents |
| [synodlang.github.io](https://github.com/synodlang/synodlang.github.io) | The website and documentation: https://synodlang.github.io |

## Why Synod

Synod is named after the Synod protocol, the core consensus algorithm in Leslie Lamport's paper "The Part-Time Parliament" (ACM Transactions on Computer Systems, 1998; first submitted in 1990). The paper tells it as the story of the parliament of the ancient Greek island of Paxos, whose part-time legislators could agree on decrees although they came and went; today the algorithm is known as Paxos. Lamport later explained it plainly in "Paxos Made Simple" (2001), and in 2013 he received the ACM A.M. Turing Award for fundamental contributions to the theory and practice of distributed and concurrent systems. His "Time, Clocks, and the Ordering of Events in a Distributed System" (1978) and his TLA+ specification language shaped how we reason about such systems. We are grateful for his work, and we hope Synod honours it by making these ideas easier to watch and understand. Everything in this organization is built with that in mind.
