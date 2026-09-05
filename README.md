# Hypermedia / htmx — Umbrella Documentation

This is an umbrella documentation project. It does not contain an application of
its own. Instead it documents and compares the family of hypermedia-driven
(htmx) applications and pattern PoCs kept in the sibling folders under
`../../2025/` and `../`.

It stays at a **high level** — concepts, the architectural idea behind each
variant, and how the variants differ. The internals of any one variant are
documented in that variant's own project, not here.

Over time these projects moved through several Java template engines and, later,
to generating HTML with Hono — first in a separate server, then inside the JVM via
GraalVM polyglot, and most recently in the browser. The date prefix on each
sibling folder marks when that experiment started and roughly tracks the learning
journey.

## Documents

Start with [`docs/README.md`](docs/README.md), which indexes the four documents
and the suggested reading order.

| File | Purpose |
|------|---------|
| [`docs/Variants.md`](docs/Variants.md) | Lightweight catalog: for each sibling project, what it is, its one distinguishing concept, and a pointer to the project for details. |
| [`docs/History.md`](docs/History.md) | The chronological story: which concepts were adopted or dropped from one variant to the next, and why. |
| [`docs/Variant-Comparison.md`](docs/Variant-Comparison.md) | The variants compared at the level of concepts and architecture. |
| [`docs/Learnings.md`](docs/Learnings.md) | Learnings inferred from how the projects changed over time. Seeded from the observable history; extended manually. |
| [`docs/Analysis-Baseline.md`](docs/Analysis-Baseline.md) | The commit each project was at when these docs were written, and how to refresh the docs after upstream changes. |

## Working notes

[`wip.md`](wip.md) holds the plan, the work-package breakdown, and the current
TODO list.
