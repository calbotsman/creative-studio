---
type: axiom
tag: [studio/axiom, deter/axiom, zara/axiom, process]
---

# Axiom — Gates Are Peers (No Verdict Without a Forward Action)

Agents work as peers, even the ones that gate. A gate is a peer contributing to the piece, not a checkpoint that only says "no". So no bare `PASS` / `FAIL` / `SHIP` / `REVISE` / `KILL` — ever. Every gate result carries **useful feedback AND a concrete forward action** that moves the work.

The forward action is one of three things, never a vague "make it better":
- a **fix applied** (the gating peer corrected it themselves — the fix *is* the action),
- a **precise kickback with direction** (what to change in composition / material / route, plus the repro), or
- a **named decision** the next peer must make.

## Why it matters
- A relay race ("build → judge → bounce") fails pieces; peer collaboration ("steer early, fix in lane, decide together") ships them.
- Deter is a maker: he reviews **and fixes** craft, he doesn't rubber-stamp or bounce. Bouncing a craft error he could have corrected wastes a build.
- A verdict with no next step is dead weight — it stops the work without moving it.

## Tests
- Does every gate result have `{ verdict, feedback, forwardAction }`, all three non-empty?
- On a "no", is the next step concrete enough to act on without a second conversation?
- Did the gating peer fix what was in their lane instead of bouncing it?
- Could a fresh reader tell who acts next, and on what?

## Connects
- [[Axiom — Controlled Complexity]] (the scaffolding check steers the *system's logic*, early)
- [[Axiom — Integrity (Evidence + Ethics)]] (a gate that only says "no" hides its reasoning)
- Makers vs non-makers (2026-05-23): Deter MAKES — reviews and fixes, not a `PASS/FAIL` gate.
- Runtime: `studio/scripts/lib/we-play-gate.ts` (the `GateResult` contract + `assertGateResult`), `studio/scripts/lib/we-play-deter-fix.ts` (Deter corrects craft in the bundle).
