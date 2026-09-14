# Vision

**Status:** draft, 2026-09-14. Owner: Bruce.

## Thesis

Everyone will have one personal agent that runs everything else. The plumbing for that (spawning sessions, worktrees, multiplexers) will be commoditised by the model labs. What will not be commoditised is the supervision discipline: how a human stays in control of a fleet whose members confidently report wrong things.

Alfred is that discipline turned into a product.

## Origin

The method was not designed. It was extracted from about 80 sessions of running a real SaaS product with a strict command/executor split, where:

- the command session only plans and accepts, and never executes;
- executors only execute, and never talk to the human;
- every rule was added after a specific, dated failure.

Some measured facts that shaped it:

- In one session, premises handed to executors were overturned 34 times. Every time, the code was right and the brief was wrong.
- The highest-value executor behaviour observed was refusing the brief. One refusal stopped the deletion of 24 real customer rows across 5 organisations.
- The executor's dominant failure mode is not getting stuck. It is ending its turn on "about to do", silently. Supervision has to watch for idling, not just for crashes.
- "Zero" results are meaningless until the observation point is proven able to see the target (positive control in the same batch).

## Principles

1. **Silence is never consent.** A peer or agent cannot turn the human's silence into a decision. Only a live, in-session grant counts; relayed authorisation is void.
2. **Evidence, not self-report.** A task closes against a verification matrix written before the work started. Evidence reports are compared to the matrix, not read for their conclusions.
3. **The code wins.** When an executor finds the brief's premise wrong, reporting that is the success case. Briefs state symptoms and constraints, never prescribed mechanisms.
4. **Partial success is reported as partial.** Once the main write has landed, later failures never become "the whole thing failed". Name what landed, say whether retry is safe.
5. **Pre-authorisation is not acknowledgement.** A standing grant lets the executor proceed; it does not let the executor skip showing the evidence.
6. **Watch for idling, not just for death.** A state file silent for 15 minutes is an event.
7. **Refusal is a stop-and-investigate result, never an obstacle.** Executors that hit a credential prompt, a destructive step, or an unverifiable premise stop and report. Routing around a block is the failure case.

## Product shape

- **Core (this repo, open):** state directory format, supervision contract, brief and evidence templates, zero-token watcher, CLI.
- **Console (closed, later):** desktop window that reads the state directory and renders fleet state, open decisions, evidence-vs-matrix, gate approvals.
- **Sync + mobile (closed, paid, later):** executors run on a desktop; decisions are approved from a phone. The sync service is the paid object.

## v0 scope

One thing: replace the manual "check the state file every 15 minutes" with a watcher.

- A `state/` directory with one file per task, sparse `<state>: <note>` lines, supervisor-actionable events only.
- A watcher that sleeps and wakes the command seat on: silence beyond a threshold, `needs-decision`, `blocked`, `done`.
- Brief and evidence formats copied verbatim from the existing working rules. No redesign.

Explicitly out of v0: GUI, multi-backend support, remote executors, relay to chat apps, anything for a second user.

## Non-goals

- Competing on orchestration plumbing.
- Running inside a specific platform's sandbox. Executors are harness-agnostic.
- Being a chat product.
