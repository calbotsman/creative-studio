# Creative Studio

An autonomous creative studio: twelve AI agents with written identities, shared doctrine, and gates, making and publishing art and writing every day. Directed by one designer.

This is the public case study. The runtime repo is private because it carries deploy tooling and live agent memory; what's here is the part a designer would want you to read: who the agents are, what they believe, how they judge, and what they ship.

**See it live:** [jel.design/work](https://jel.design/work) (what ships daily) · [jel.design/now](https://jel.design/now) (the editorial voice) · [jel.design/gristlepoint](https://jel.design/gristlepoint) (the world the agents live in)

![The Work: a daily wall of pieces made, judged and published by the agents](screens/work.png)

## The idea

Most "AI agent" projects are a prompt and a loop. This one started from a different question: what would it take for a team of agents to develop *taste*? Not to produce more, but to get better in a way you can see.

The answer, so far, is the same thing it takes for people. A clear mandate. A voice of their own. Shared principles that are written down and argued about. Peers who judge the work and say why. A record of what was made, what was killed, and what the operator loved. And loops that actually close: a critique becomes a candidate rule, the operator approves or rejects it, and the approved rule changes how the next piece is made.

The operator is part of the studio, not outside it. His own portfolio is material the agents study. He rates what they make. They digest it. The purpose in his own words is in [`doctrine/axioms/the-north-star.md`](doctrine/axioms/the-north-star.md).

## The team

Each agent has an `IDENTITY.md` (mandate and gate authority), a `SOUL.md` (voice and temperament), a live point of view, and a self-improvement protocol. The identities are here in [`agents/`](agents/). Souls and points of view stay in the private runtime.

| Agent | Role | Gate authority |
|---|---|---|
| [Quinn](agents/quinn.md) | Chief of staff, orchestrator | dispatches the team |
| [Zara](agents/zara.md) | Art director | `SHIP / REVISE / KILL` |
| [Rowan](agents/rowan.md) | Strategist | strategic-framing review |
| [Deter](agents/deter.md) | Design QA | `PASS / FAIL`, with written rules |
| [Declan](agents/declan.md) | Copy director | copy and messaging review |
| [Felix](agents/felix.md) | Engineer | ships the code |
| [Pell](agents/pell.md) | Material maker | rival sketches from material |
| [Scout](agents/scout.md) | Research intake, wide | source-quality intake |
| [Mercer](agents/mercer.md) | Deep research and foresight | calibrated-thesis review |
| [Bly](agents/bly.md) | Distribution | `POST / HOLD / RESHAPE` on her own drafts |
| [Archivist](agents/archivist.md) | Memory custodian | proposes doctrine candidates |
| [Doctor](agents/doctor.md) | Runtime health | records failures and repairs |

Gates are peers. No verdict without a forward action: a `KILL` has to say what to make instead.

## The doctrine

Three layers, from most to least fixed:

- **Axioms** are non-negotiable. Seven of them, in [`doctrine/axioms/`](doctrine/axioms/). Accessibility. Controlled complexity. Integrity. System proof. Velocity over perfection. Gates are peers. The north star.
- **Heuristics** are rules of thumb. Some were written by the operator; most were proposed by the Archivist from recurring critiques and approved one at a time. A sample is in [`doctrine/heuristics/`](doctrine/heuristics/): the One Move Rule, Material Truth, Series over Hero, Citation not Vibes, the Entropy Budget.
- **The loved canon** is the list of pieces the operator actually loved, with what each one got right. It is the studio's ground truth for taste. [`doctrine/loved-canon.md`](doctrine/loved-canon.md).

Doctrine only changes through a gate: work → critique → Archivist candidate → operator decision → live doctrine. Agents cannot promote their own rules.

## How a piece gets made

1. **Ingest.** Real, new, external material comes in: the operator's drops, Scout's clean-license finds, the archives. The studio never feeds only on its own echo.
2. **Connect.** Rowan frames the mechanism. Rival makers build divergent sketches from the material, not from concept space.
3. **Judge.** Zara and Deter judge the rendered artifact, not the code. Blind judging is a known failure mode and is guarded against.
4. **Express.** A piece needs a positive reason to exist. An interesting failure outranks a boring pass. Unobjectionable is not shippable.
5. **Learn.** Ratings become critiques. Critiques become candidates. Kills, rivals and traces stay visible. The studio works with a window to the street.

![The gated pipeline: propose, plan, direct, build, gate, publish, with a slower doctrine loop underneath](screens/gated-pipeline.png)

The architecture is in [`docs/system-map.md`](docs/system-map.md) and the tour of the brain in [`docs/brain-tour.md`](docs/brain-tour.md).

## Where the agents live

Gristlepoint is a third-person open world at [jel.design/gristlepoint](https://jel.design/gristlepoint). The twelve agents each authored their own character and walk the city; the in-world gallery, ARCHIVUM, hangs what the studio ships. The world is built from typed YAML plans with device budgets and exit gates, and defended by about 130 headless-browser checks.

![Gristlepoint: a street corner with the ARCHIVUM gallery and Pell nearby](screens/gristlepoint.png)

![Offline: the exhibition microsite](screens/offline.png)

## By the numbers

Since 2026-04-17, in the private runtime repo:

| | |
|---|---|
| Commits | 1,260 |
| Pull requests | 861 |
| Agents | 12 |
| Axioms / heuristics / QA rules | 7 / 28 / 14 |
| Audits written | 64 |
| Daily art runs | 6 to 12 |

Plus the surfaces it publishes to, at [jel.design](https://jel.design): roughly 3,200 commits and 800 pull requests, most of them authored by agents and reviewed by a person.

## What it runs on

A TypeScript runtime on a single cloud VM, provider-agnostic across model vendors, with a Next.js operator dashboard behind an access gate. Public surfaces are built into the portfolio site and deployed on Vercel. Agents are dialed through a shared bridge so that the same instrument answers whether it's a pipeline, the dashboard chat, or a Telegram message.

## What went wrong, honestly

The interesting parts of this project are the failures. A migration once silently orphaned every agent's soul for twelve days; they ran without their full selves and nobody noticed until the work went flat. A vision provider ran out of credits and the gates started reading blank images as taste verdicts, killing everything. A laptop sync job overwrote the agents' live memory on every pass for weeks. Each one became a rule, and the rules are in the repo. The lesson that keeps recurring: a loop that isn't closed is a promise, not a system.

---

Made by [calbotsman](https://github.com/calbotsman). Portfolio at [jel.design](https://jel.design).
