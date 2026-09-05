# docs/ — index

High-level documentation of the hypermedia / htmx variant family. Scope: concepts
and cross-variant differences only. Per-project internals live in each project.

Read in this order:

1. **[Variants.md](Variants.md)** — the catalog. Opens with the project ↔ GitHub
   repository table, then for each project: what it is, its one distinguishing
   idea, and status. Start here.
2. **[History.md](History.md)** — the chronological story: which concepts were
   adopted or dropped from one variant to the next, and why. Told as 8 phases.
3. **[Variant-Comparison.md](Variant-Comparison.md)** — the variants compared on
   fixed axes (where HTML is generated, view technology, the cross-language
   contract, dynamic-update style, native-image/deployment), then a deep
   **two-process vs GraalVM vs browser-hono** trade-off section and a "when to
   pick which" table.
4. **[Learnings.md](Learnings.md)** — learnings inferred from how the projects
   changed over time. Seeded from the observable history; **meant to be extended
   manually.**
5. **[Analysis-Baseline.md](Analysis-Baseline.md)** — the commit each project was
   at when these docs were written, plus how to refresh the docs after upstream
   changes.

Working notes and the work-package plan are in [`../wip.md`](../wip.md).
