# Instructions for AI

This file serves as the working document for Claude. It contains information and
instructions so that the prompt on the command line can refer to this file.
It is a living document and is maintained as work on this project progresses.
Claude also keeps its list of TODOs in this file.

## Umbrella project's purpose

This project is a place for documentation of the various variants of my
hypermedia / htmx applications. Some sibling projects implement the same app in
different variants; others are just a PoC or demonstrate hypermedia/htmx patterns.

### Sibling projects (folders relative to this one)

- ../../2025/2025-08-23_ssfe-patterns-jte-vc-htmx
- ../../2025/2025-08-23_ssfe-patterns-jte-htmx
- ../../2025/2025-08-23_ssfe-patterns-thymeleaf-htmx
- ../../2025/2025-12-21_ssfe-patterns-quarkus-qute-htmx
- ../../2025/2025-12-27_ssfe-patterns-hono-htmx
- ../../2025/2025-12-31-springboot-hono-poc
- ../2026-01-24_hda-dynapage-demo
- ../2026-03-07_springboot-graalvm-jsx-poc
- ../2026-03-09_hda-springboot-graalvm-jsx-demo
- ../2026-03-15_hda-quarkus-graalvm-jsx-demo

### Additional notes

- The date prefixes of the folder names indicate when each project was started and
  thus also reflect my learning experience over time.
- The timeline shows that I tried out various template engines for use with a Java
  web application.
- 2025-08-23_ssfe-patterns-thymeleaf-htmx: only started, still needs to be
  implemented like the JTE variants.
- Currently (September 2026) my preferred template engine is Hono/TS with its
  `html``` tagged template.
- There are also the folders ../2026-05-01_springboot-hono-docs and
  ../2026-05-02_ssfe-patterns-jte-vc-htmx-docs which I think I created to generate
  docs from the real code. In a later step these can most likely be extended to
  create code-docs for the variants.

## Scope of the umbrella project

The umbrella project documents **high-level things only**: concepts, the
architectural idea behind each variant, and how the variants differ from one
another. It is **not** the place to document the internals of a variant — that
belongs in the individual project. Every catalog entry therefore stays short and
points to the individual project for the details.

Deliverables:

- `docs/Variants.md` — a lightweight catalog: for each project a short paragraph
  on what it is, the one concept that distinguishes it, and a pointer to the
  project itself.
- `docs/History.md` — the chronological story: which concepts were adopted or
  dropped from one variant to the next, and why.
- `docs/Variant-Comparison.md` — the variants compared at the level of concepts
  and architecture, not implementation detail.
- `docs/Learnings.md` — learnings inferred from how the projects changed over
  time. Claude seeds this from the observable history; the user is expected to
  extend and correct it manually later.

## Approach

- `docs/Variants.md` is written first as the shared reference; `History.md`,
  `Variant-Comparison.md` and `Learnings.md` build on it.
- All documentation output lives in `docs/` as Markdown.
- This repo only reads the sibling projects; it never modifies them.
- Work is split into work packages. Each work package is one manual git commit by
  the user. Claude stops after finishing a work package and reports; the user
  inspects and commits.

## Work packages

| WP  | Status | Deliverable |
|-----|--------|-------------|
| WP0 | DONE   | This `wip.md` rewrite (plan + TODO list) and umbrella `README.md`. |
| WP1 | DONE   | `docs/Variants.md` — lightweight catalog of all sibling projects (concept + role + pointer). |
| WP2 | TODO   | `docs/History.md` — chronological story of concepts adopted / dropped and why. |
| WP3 | TODO   | `docs/Variant-Comparison.md` — concept- and architecture-level comparison. |
| WP4 | TODO   | `docs/Learnings.md` — learnings seeded from the observable history (user extends later). |
| WP5 | TODO   | `docs/README.md` index + cross-links; final `wip.md` cleanup. |

### Catalog entry shape (WP1)

Per project, a few lines only: folder path + start date, role (app variant /
PoC / pattern showcase / docs generator), the stack in one line, the one
distinguishing concept, current status, and "details: see the project". No
internals.

### Comparison dimensions (WP3)

Kept high-level: backend framework + language, where HTML is generated (in the
JVM / separate process / GraalVM polyglot), template/view technology as a
concept, how dynamic updates are done (full page / OOB / partial), and the main
trade-off / when this variant makes sense.

## TODO

- [x] WP1 — `docs/Variants.md` (all projects, lightweight)
- [ ] WP2 — `docs/History.md`
- [ ] WP3 — `docs/Variant-Comparison.md`
- [ ] WP4 — `docs/Learnings.md` (seed only)
- [ ] WP5 — `docs/README.md` index + cross-links, `wip.md` cleanup

## Open items (original)

- create a file History.md which includes the main differences between the
  variants — planned as WP2 (`docs/History.md`).
- create a file Variant-Comparison.md which includes the main differences between
  the variants. Analysis of the projects will be needed to do this — planned as
  WP1 (`docs/Variants.md` catalog) + WP3 (`docs/Variant-Comparison.md`).
