# Hypermedia / htmx — Umbrella Documentation

This is an umbrella documentation project. It does not contain an application of
its own. Instead it documents and compares a family of hypermedia-driven (htmx)
applications and pattern PoCs, each kept in its own repository under
[`github.com/svene`](https://github.com/svene). See
[`docs/Variants.md`](docs/Variants.md) for the project ↔ repository table.

It stays at a **high level** — concepts, the architectural idea behind each
variant, and how the variants differ. The internals of any one variant are
documented in that variant's own project, not here.

Over time these projects moved through several Java template engines and, later,
to generating HTML with Hono — first in a separate server, then inside the JVM via
GraalVM polyglot, and most recently in the browser. The date prefix in each
project name marks when that experiment started and roughly tracks the learning
journey.

For the local repository layout, the project categories, and how the
documentation set is kept current, see
[`README_details.md`](README_details.md).

## Documents

Read in this order:

1. **[docs/Variants.md](docs/Variants.md)** — the catalog. Opens with the two
   project groups — **A · Hypermedia pattern showcases** (one per template technology)
   and **B · "person" use-case apps** (one per technology/architecture), plus
   the docs tooling — then the project ↔ GitHub repository table (with a
   **Group** column) and, per project, what it is, its one distinguishing idea,
   and status. Start here.
2. **[docs/History.md](docs/History.md)** — the chronological story: which
   concepts were adopted or dropped from one variant to the next, and why. Told
   as 8 phases.
3. **[docs/Variant-Comparison.md](docs/Variant-Comparison.md)** — the variants
   compared on fixed axes (where HTML is generated, view technology, the
   cross-language contract, dynamic-update style, native-image/deployment), then
   a deep **two-process vs GraalVM vs browser-hono** trade-off section and a
   "when to pick which" table.
4. **[docs/Learnings.md](docs/Learnings.md)** — learnings inferred from how the
   projects changed over time. Seeded from the observable history; **meant to be
   extended manually.**

## Working notes

AI-facing tracking, kept separate from the docs above — see
[`README_details.md`](README_details.md) for why. [`docs/ai/wip.md`](docs/ai/wip.md)
holds the current TODO list and the conventions used when extending this
documentation set; completed work packages are logged in
[`docs/ai/wip_done.md`](docs/ai/wip_done.md);
[`docs/ai/Analysis-Baseline.md`](docs/ai/Analysis-Baseline.md) tracks the
commit each sibling project was last analysed at, so the docs above can be
refreshed after upstream changes (automated by the `update-docs` skill).
