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
formalization (Mathlib v4.30) with two strands. **(a) The finite-volume 2D Ising
phase transition** (`temperature_statement`): spontaneous magnetization at low
temperature (Peierls / contour) and correlation decay / concentration at high
temperature. **(b) Friedli–Velenik Chapter 6 — the general DLR theory of Gibbs
measures** (`Ch6Subtree/`, ~26k lines, **merged 2026-07-28, reviewed + approved**):
the DLR formalism (proper, consistent specification kernels), Gibbs-measure
existence, **Dobrushin & Kotecký–Preiss cluster-expansion uniqueness**, the
**extremal (Choquet) decomposition** (tail-triviality ⇔ short-range correlations,
with an a.e. Lévy-downward martingale theorem not yet in Mathlib), and the
**variational principle** (Gibbs ⟺ equilibrium state, incl. the Lanford–Ruelle
converse) — sorry-free, axiom-clean. This DLR base is now consumed by
`RandomClusterModel`.

**[`RandomClusterModel`](https://github.com/random-fields/RandomClusterModel)** — a
Lean 4 formalization of the **random-cluster (Fortuin–Kasteleyn) model** (Mathlib
v4.30), built on GibbsMeasure's Ch.6 DLR base (imported byte-for-byte). Grimmett,
*The Random-Cluster Model*, Ch. 2–3 (**reviewed + approved 2026-07-29**): the
FKG / Holley / monotone-coupling toolkit and the **KKL / BKKKL influence +
sharp-threshold** theory (transporting O'Donnell's `FABL` KKL to monotonic measures
via dyadic approximation), then the random-cluster measure
`φ_{p,q} ∝ p^{|open|}(1−p)^{|closed|}q^{k(ω)}` with positive association (`q ≥ 1`),
the Grimmett (3.21) comparison inequalities, Edwards–Sokal / Ising domination, and
a Russo-type differential. Sorry-free, axiom-clean, build-green — autoformalized via
`design-tools` and human/AI-reviewed.

**[`RandomFields`](https://github.com/random-fields/RandomFields)** — the
**foundations monorepo** (Primitive A + Layer 1, Track A): symmetric Markovian
Dirichlet forms, the Ornstein–Uhlenbeck semigroup with Bakry–Émery / log-Sobolev,
and the isonormal Gaussian process + **Wiener chaos + hypercontractivity** — the
richest launchpad for the analysis-side program. The isonormal / chaos /
hypercontractivity layer is axiom-free; a few interim Hermite / chaos-orthogonality
axioms and three isolated `sorry`s (unbounded generation) are flagged for discharge.

**[`graphons`](https://github.com/random-fields/graphons)** — a Lean 4
formalization of **graphons & dense graph limits** (Lovász; roadmap layer L9): the
cut metric, sampling, and limit theory, with a mature, sorry-free core and an
axiom-guard CI — the template for the org's plan-loop.

**[`optimal-transport`](https://github.com/random-fields/optimal-transport)** — a
Lean 4 formalization of **optimal transport & Wasserstein geometry** (L3 / Topic 3):
Kantorovich duality, the Monge ↔ Kantorovich relaxation, and **Brenier's theorem** —
0 `sorry` / 0 axiom. Foundation for the transport-entropy / functional-inequalities
roadmap.

**[`nlsm-massgap`](https://github.com/random-fields/nlsm-massgap)** — the **flagship
end-to-end target**: a constructive field-theory mass-gap goal that *consumes* the
foundation repos (a downstream application, not a base).

**[`free-probability`](https://github.com/random-fields/free-probability)** — a
Lean 4 formalization of **free probability** following **Arup Bose's textbook**
(`FreeProbability/Arup/Chapter1–6.lean`). An active, substantial library: roughly
385 lemmas/theorems across the six chapters — noncommutative probability & free
independence, non-crossing/pair partitions, moments & free cumulants, and (Ch. 6)
free additive/multiplicative convolution with the semicircle and free-CLT-adjacent
laws. Chapter 5 is sorry-free; ~114 `sorry`s remain, concentrated in Ch. 3 and the
newest Ch. 6 (the free-convolution / free-CLT frontier). Alongside the main body,
the `design-tools` autoformalization loop maintains **sorry-free `kg-*` branches**
(`kg-free-cumulants` — free cumulants via Möbius inversion over the non-crossing
lattice, moment–cumulant relation proven; `kg-noncrossing-catalan`;
`kg-semicircle-moments`). Target on deck: the **free CLT / semicircle law**.

**[`design-tools`](https://github.com/random-fields/design-tools)** — KG-driven
autoformalization tooling. `scaffold_target.py` turns any knowledge-graph node into
a ready-to-formalize Lean scaffold: a spec card (informal statement, suggested Lean
name, sources, and the *frontier cut* — each prerequisite's coverage against
Mathlib ∪ our repos, with the nearest reusable declaration) plus a starter `.lean`
skeleton. `build_roadmap.py` ranks the absent backbone into a prioritized,
dependency-ordered backlog (`mathlib2_queue.jsonl`, 298 Tier-1 targets), and
`docs/autoformalization-playbook.md` documents the loop with a reusable
formalizer-agent prompt — so *pick a target → scaffold → agent → verified Lean →
PR* becomes repeatable rather than bespoke. Worked example: free-probability's
free-cumulants module.

## Current state

The org has moved from "one repo near completion" into a **stack of interlocking
formalization bases**. `planning` remains the mature, actively-maintained hub
(knowledge graph at 16,833 nodes / 23,461 edges from 541 sources, grounded against
Mathlib + our own repos), and the `design-tools` autoformalization loop is now
producing **reviewed, sorry-free, axiom-clean** Lean rather than scaffolds only.

- **Statistical mechanics.** `GibbsMeasure` grew a full **Friedli–Velenik Ch.6 DLR
  theory** (specifications → existence → Dobrushin/Kotecký–Preiss uniqueness →
  extremal decomposition → variational principle), **merged 2026-07-28** and
  reviewed. `RandomClusterModel` builds the **random-cluster / FK model** (Grimmett
  Ch. 2–3: FKG/Holley, KKL/BKKKL, comparison, Edwards–Sokal) on that base,
  **reviewed + approved 2026-07-29**. `percolation` extends the same line (Grimmett
  percolation), autoformalized, review pending. The original
  **2D Ising phase transition** in `GibbsMeasure` is complete on the high-temperature
  side and proven low-temperature modulo two honest geometric residuals
  (`min_le_nine_allSqLen_small`, `expectedAllCountAtLength_le`), paused 2026-06-01
  in a green state.
- **Analysis foundations.** `RandomFields` (Dirichlet forms, Ornstein–Uhlenbeck /
  Bakry–Émery, Wiener chaos + hypercontractivity), `optimal-transport` (Kantorovich
  duality, Brenier — 0 sorry / 0 axiom), and `graphons` (dense graph limits) are the
  launchpads for the functional-inequalities and transport-entropy roadmaps.
  `nlsm-massgap` is the flagship downstream application that consumes them.
- **Free probability.** `free-probability` has its foundations (noncommutative
  probability, non-crossing/pair partitions, classical CLT) plus an agent-formalized
  free-cumulants module, with the free CLT next.

Net: several reviewed formalization bases across statistical mechanics and analysis,
an autoformalization loop turning the knowledge map into verified Lean, and a
planning layer that still maps far more of the literature than the repos have yet
formalized.
