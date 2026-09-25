# studio-brain/ — the canonical tree

The source of truth for what every studio agent knows. Replaces the legacy
`Agents/` tree (archived 2026-04-17 to `_archive/agents-pre-redesign-2026-04-17/`).

This README is the tour. Every agent should know where things live so they can
read deeper into their own toolkit when a session calls for it.

## Tour

```
studio-brain/
├── identity/                          who the agents ARE
│   ├── _operator.md                   shared operator (the operator) profile
│   ├── _operator-note-2026-05-13.md   one-time note about the recovery
│   └── <agent>/                       one folder per agent
│       ├── IDENTITY.md                role, mandate, gate authority
│       ├── SOUL.md                    voice + temperament + Truth Discipline
│       ├── WORKING_MEMORY.md          VM-owned KEEP/AVOID/TEST/RECALL; absent locally
│       ├── SELF_IMPROVEMENT_LOOP.md   durable learning protocol (all agents)
│       ├── PRACTICE.md                (Ivo) inspectable studies, collaboration,
│       │                              recoverable project records
│       ├── Frameworks Index.md        (Rowan)
│       └── Signal Library.md          (Rowan)
│
├── doctrine/                          shared rules everyone reads
│   ├── axioms/                        non-negotiable principles
│   ├── heuristics/                    rules of thumb (incl. Cold Start Ritual,
│   │                                  Per-Round Designer Method, Heartbeat vs
│   │                                  Cron, Group Chat Speak or Stay Silent)
│   ├── rules/                         Deter's 14 QA rules + ENFORCEMENT.md
│   │   ├── README.md                  index + soft↔hard lifecycle
│   │   ├── ENFORCEMENT.md             how to enforce (3-layer model, gaps)
│   │   └── escalation-log.md          hard-failure log + pattern detection
│   ├── pov/                           per-agent live worldview, one file per
│   │   │                              agent, all thirteen
│   │   ├── quinn-pov.md
│   │   ├── zara-pov.md
│   │   ├── ...
│   │   └── ivo-pov.md                 founding claims, labeled provisional
│   │                                  (2026-09-14)
│   ├── candidates/                    Archivist-proposed doctrine changes
│   └── rejected/                      doctrine changes the operator rejected
│
├── corpus/                            the influence library
│   ├── references/                    dossiers (40+), YES.md, NO.md,
│   │                                  SYNTHESIS.md, DESIGN_SYSTEM.md, etc.
│   ├── baselines/                     quality bars by surface type
│   ├── cost-tiers/                    routing inputs
│   └── templates/                     authoring schemas for hand-written
│                                      doctrine, references, critiques
│
├── memory/                            what the studio has experienced
│   ├── critiques/                     per-piece evaluations
│   ├── decisions/                     strategic/creative decisions (Rowan
│   │                                  Decision Feed, ZARA_FEED, sync logs)
│   ├── sessions/                      session transcripts (gitignored)
│   ├── doctor_log/                    heartbeats (gitignored)
│   ├── design-studies/<date>/         daily design-study records, SVG + PNG
│   │                                  renders, critiques (VM-owned, gitignored)
│   └── dreams/                        consolidated dreams
│
├── routing/                           how agents are dispatched
│   ├── task_router.yaml               task → agent + tier
│   ├── llm_tiers.yaml                 tier → model chain
│   ├── budget.yaml                    cost caps
│   └── schedule.yaml                  cron / heartbeat cadence
│
├── budget/                            cost plan
├── projects/                          per-project agent state
└── hooks/                             session-start / session-end
```

## How to read your own files (any agent)

On cold-start, in order:

1. `identity/_operator.md` — who you're helping
2. `identity/<your-agent>/IDENTITY.md` — your mandate
3. `identity/<your-agent>/SOUL.md` — your voice
4. runtime `identity/<your-agent>/WORKING_MEMORY.md` — your recent calibration;
   retrieve it from the VM/runtime, never an empty or stale laptop copy
5. `doctrine/pov/<your-agent>-pov.md` — your live worldview
6. `identity/<your-agent>/SELF_IMPROVEMENT_LOOP.md` — your durable learning protocol

That's the minimum. From there, follow your IDENTITY's nav pointers into
`doctrine/` and `corpus/` as the task warrants.

This sequence is encoded in the **Heuristic — Cold Start Ritual** at
`doctrine/heuristics/`. Follow it.

## How content moves

- **Read direction:** agents read `identity/` + `doctrine/` + `corpus/` on every
  invocation. They never write to those directly.
- **Write direction:** agents write critiques to `memory/critiques/` and
  decisions to `memory/decisions/`. The Archivist proposes doctrine candidates
  into `doctrine/candidates/`. The operator approves; approved candidates move
  into `doctrine/{axioms,heuristics,rules,pov}/`.

Full contract: `AGENTS.md` §2 (The Self-Improvement Contract).

## Verifying the brain is wired correctly

```
npx tsx studio/scripts/verify-agent-state.ts
```

Inspects every agent's substantive tracked IDENTITY + SOUL + POV +
SELF_IMPROVEMENT_LOOP, plus onboarding and routing coverage. The canonical dial
and Dashboard prompt loaders have separate direct tests; this verifier is not a
synthetic substitute for them. The reported count changes as guards are added.
VM-owned WORKING_MEMORY may be
absent on a fresh checkout; its presence and freshness require a separate
runtime receipt. CI runs this on every relevant PR.

## History

- 2026-04-17: migrated from legacy `Agents/` tree. See `MIGRATION_MAP.md`.
- 2026-05-13: audit found the migration silently orphaned ~500 lines per
  agent. Full recovery via PR #49 restored SOUL, POV, axioms, heuristics,
  SELF_IMPROVEMENT_LOOPs, decisions, templates, and fixed 11 persona-loading
  code paths. See `MIGRATION_MAP.md` "Audit + recovery" section + the
  one-time apology at `identity/_operator-note-2026-05-13.md`.
- 2026-09-14: Ivo founded as resident artist (`identity/ivo/`, `pov/ivo-pov.md`),
  self-named in a workshop instance. The same day the operator paused the legacy
  autonomous art makers via `studio/config/art-ownership.json`; Ivo leads art and
  the studio contributes on her direction. Her working memory, journal and
  feedback are excluded from the automatic dream synthesis.
- 2026-09-16: Ivo's public stream policy (`studio/config/ivo-public-stream.json`)
  publishes only her own image and writing receipts to `jel.design/now/ivo`.
- 2026-09-21: daily design study restarted (decided 2026-09-17, merged
  2026-09-20). Records land in `memory/design-studies/`; each study writes one
  critique to `memory/critiques/` for the Archivist. Doctrine, identity and
  working memory are never written by the loop.
