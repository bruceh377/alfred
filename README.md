# Alfred

A personal agent that runs your fleet of coding agents so you only make decisions.

You talk to Alfred. Alfred briefs executors, watches their state, collects evidence, and brings you exactly the decisions that need a human. Nothing ships on an agent's self-report.

**Status:** pre-alpha, docs only. Nothing runs yet.

## What it is

- **One command seat, many executors.** You hold one session. Executors run in their own sessions and never talk to you directly.
- **Gates, not vibes.** Work is dispatched against a written brief and a verification matrix. It closes when evidence matches the matrix, not when the agent says "done".
- **Zero-token supervision.** A watcher sleeps on the state directory and wakes the command seat on silence, blockers, or decisions. Idle time costs nothing.
- **A console, not a chat.** The GUI shows fleet state, open decisions, and evidence-vs-matrix. Executors keep running in whatever harness you already use.

## What it is not

- Not an agent runtime. Alfred sits on top of Claude Code / Agent SDK style sessions.
- Not a chat UI, terminal emulator, or code editor.
- Not a compliance guarantee for your agents. It makes lying harder, not impossible.

## Where this comes from

The rules here were not designed up front. They were extracted from ~80 working sessions running a real product with a command/executor split, where every rule exists because a specific failure happened first. See [docs/00_Vision.md](docs/00_Vision.md).

## Repo policy

- **Open source, open core.** This repo holds the core: state format, supervision contract, watcher, CLI. Apache-2.0.
- **Not accepting pull requests.** This is a personal project built for one user first. PRs are closed automatically.
- **Issues are welcome** but triaged strictly against the author's own needs. No roadmap promises, no support commitments.
- A hosted sync service and native clients (web, macOS, iOS/iPadOS) may follow as closed-source paid products. The core stays open.

## Name

"Alfred" is a working name for the repo. The product will ship under a different name.
