# Creative Studio System Map

This is the stable architecture map for the active Studio. IDE LLMs enter through
`CLAUDE.md`; mutable current work lives in `docs/AGENT_HANDOFF.md`; selected
release state lives in `studio/config/studio-release-history.yaml`.

## Canonical Roots

- Runtime and pipelines: `studio/`
- Operator control room: `studio-dashboard/`
- Active identity, memory, corpus, doctrine, and routing: `studio-brain/`
- Plans, audits, handoffs, and deployment documentation: `docs/`
- Project state and source material: `projects/` and `Data/`
- Retired agent archaeology: `_archive/agents-pre-redesign-2026-04-17/`

The legacy `Agents/` tree is not an active source of truth.

## Identity and Learning

- Agent identity: `studio-brain/identity/<id>/IDENTITY.md`
- Agent voice: `studio-brain/identity/<id>/SOUL.md`
- Live POV: `studio-brain/doctrine/pov/<id>-pov.md`
- Runtime observations and critiques: `studio-brain/memory/`
- Candidate doctrine: `studio-brain/doctrine/candidates/`
- Approved doctrine: `studio-brain/doctrine/{axioms,heuristics,rules,pov,anti-patterns}/`
- Promotion contract: `AGENTS.md` §2 and `studio-brain/doctrine/README.md`

The legal loop is work → critique → Archivist candidate → operator decision → live doctrine. There is no self-promotion path.

## Runtime Direction

- Quinn is the conversational and orchestration front door.
- Scout intakes external signals; Mercer researches; Rowan frames mechanism and strategy.
- Ivo leads art commissions and accepts Studio contributions. The legacy art
  makers are paused by `studio/config/art-ownership.json`; Ivo's on-demand tools
  and the Studio's design work remain available. Her private autonomous practice
  uses native opportunity checks, reviewed limits in `studio/config/ivo-practice.json`,
  and an explicit authenticated practice activation; missing control is paused.
- Zara supports art direction under Ivo's commission; Declan directs Writing.
  Makers join early for feasibility without silently replacing the inquiry.
- A daily static design study (`studio/scripts/design-study.ts`, policy
  `studio/config/design-practice.json`) runs Zara brief → Declan copy → Felix
  render → Deter pixel critique → one Felix revision → Deter critique → Declan
  account. Both versions are held for the operator's existing rating and
  publish controls; the loop does not restart paused art production.
- Deter enforces craft and repairs execution failures.
- Archivist synthesizes recurring evidence into gated candidates.
- Doctor records operational failures and repair signals.

Runtime architecture: `docs/plans/2026-04-23-studio-agent-runtime-plan.md`.

## Surface Contract

- Dashboard: operator control room and version/evidence memory.
- Quinn: conversational control plane.
- Artwork: canonical creative track; `/we-play` remains its public alias. Its legacy makers are paused since 2026-09-14.
- Ivo's stream: `jel.design/now/ivo` (reading view) and `/now/ivo/images` (images only). The reader fetches a fixed public manifest built only from her own image and writing receipts under `studio/config/ivo-public-stream.json`; it never calls private Studio endpoints.
- Writing: canonical editorial track; `/now/editorial` remains its public alias.
- Praxis: internal evidence spine; currently read-only foundation instrumentation.
- `jel.design`: public performance surface.
- `jel.design/research`: public research-backed evidence surface.
- Gristlepoint: agent habitat/world surface.

The surface and version contract is `docs/plans/2026-07-13-studio-surface-and-version-contract.md`.

## Verification

- Agent state: `npx tsx studio/scripts/verify-agent-state.ts`
- Strict Studio source + scripts: `npx --prefix studio tsc --noEmit -p studio/tsconfig.check.json`
- Legacy-path guard: `bash scripts/lint-no-legacy-agent-paths.sh`
- Studio build: `(cd studio && npm run build)`
- Studio integration: `(cd studio && bash src/tests/run-integration.sh)`
- Dashboard typecheck/build: `(cd studio-dashboard && npx tsc --noEmit && npm run build)`
- Current handoff commands: `docs/AGENT_HANDOFF.md`

## Deployment Boundary

Deployment, production VM state, secrets, tunnel configuration, and GitHub Actions secrets follow `docs/DEPLOY.md`. Studio self-modification happens only in an isolated branch/worktree, with tests and operator approval before merge or deploy.
