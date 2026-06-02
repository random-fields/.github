# random-fields

Formalizing the mathematics of probability, statistical mechanics, and
(statistical / Euclidean / constructive) field theory in **Lean 4 / Mathlib**,
together with the knowledge-mapping tooling that plans and tracks that
formalization.

## Repositories

**[`planning`](https://github.com/random-fields/planning)** — the coordination
hub. Holds the project roadmaps (`plans/`: the literature knowledge graph,
formalization-target selection, Rajarshi Mukherjee's 16-layer topic outline,
acquisition workflow, and design proposals), the corpus bibliography + rights
(`sources/`: 2,276 sources, metadata only — no documents), and a self-contained
interactive knowledge-graph viewer (`kg-viewer.html`). It plans *what* to
formalize and tracks coverage against the frontier = Mathlib ∪ our own Lean
repos; it contains no Lean code itself.

**[`GibbsMeasure`](https://github.com/random-fields/GibbsMeasure)** — a Lean 4
formalization of the **finite-volume 2D Ising phase transition**: magnetization
bounded away from zero at low temperature (Peierls / contour argument) and
concentrating at zero at high temperature, packaged as the target
`temperature_statement` (constants β₁ > β₂ > 0). About 12.6k lines of Lean
across `definitions_codex.lean` (Ising objects), `high_temperature_codex.lean`
(the HT1–HT12 expansion → correlation-decay → concentration chain),
`low_temperature_codex.lean` (the Peierls argument), and `lattice.lean`, with a
master `blueprint_codex.md` and a `Proofideas/` scratch area. Lake build files
and agent-coordination files are gitignored, so only source + docs are tracked.

**[`free-probability`](https://github.com/random-fields/free-probability)** — an
early, planning-only effort to formalize **free probability** in Lean 4
(Apache-2.0). The substantive content is `plan/ZW.md`, a scratch note targeting
the **free central limit theorem**: go directly to the free CLT (skip building
classical CLT first), with the noted blocker that Mathlib has `Finpartition` and
Catalan numbers but lacks pair partitions / non-crossing pairings and their
enumeration. No Lean code or Lake project yet.

## Current state

The org is in its build-out phase: `planning` is the mature, actively-maintained
hub (knowledge graph at 16,833 nodes / 23,461 edges from 541 sources, grounded
against Mathlib + 10 foundation repos), while the two formalization repos sit at
opposite ends of maturity. **`GibbsMeasure`** is the most advanced: the
high-temperature side is complete (0 sorries) and `low_temperature_main` is fully
proven modulo exactly **two honest gaps** — `min_le_nine_allSqLen_small` (the
small-contour minority-coverage / discrete-Jordan geometric step) and
`expectedAllCountAtLength_le` (the open-orbit contour count+energy bound), both
already reduced in `Proofideas/` to concrete, Jordan-free residuals; the
definitions layer carries 0 axioms. It was deliberately **paused 2026-06-01** in
a green state pending a "dedup tracedContours" design decision.
**`free-probability`** is at the idea stage — a target (free CLT) and a known
missing-infrastructure list, no code. Net: one formalization near completion, one
just starting, and a planning layer that already maps far more of the literature
than either repo has yet formalized.
