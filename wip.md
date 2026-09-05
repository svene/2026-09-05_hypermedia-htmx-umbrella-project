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

## Approach

- The analysis-heavy step is done once as a structured inventory of every sibling
  project (`docs/Variants.md`). Both `docs/History.md` and
  `docs/Variant-Comparison.md` are then derived from that inventory.
- All documentation output lives in `docs/` as Markdown.
- This repo only reads the sibling projects; it never modifies them.
- Work is split into work packages. Each work package is one manual git commit by
  the user. Claude stops after finishing a work package and reports; the user
  inspects and commits.

## Work packages

| WP  | Status | Deliverable |
|-----|--------|-------------|
| WP0 | DONE   | This `wip.md` rewrite (plan + TODO list) and umbrella `README.md`. |
| WP1 | TODO   | `docs/Variants.md` — catalog of the 2025 projects. |
| WP2 | TODO   | `docs/Variants.md` extended with the 2026 projects (incl. the two Astro/Starlight docs projects). |
| WP3 | TODO   | `docs/History.md` — narrative timeline / learning journey derived from the inventory. |
| WP4 | TODO   | `docs/Variant-Comparison.md` — dimension-by-dimension comparison tables. |
| WP5 | TODO   | `docs/README.md` index + cross-links; final `wip.md` cleanup. |

### Catalog entry schema (used by WP1 / WP2)

Per project: folder path, start date (from prefix), category (app variant / PoC /
pattern showcase / docs generator), backend framework, language(s), template /
view technology, build tool(s), htmx version, where HTML is generated (in the JVM
/ separate process / GraalVM polyglot), notable patterns demonstrated, current
status, key source files / docs.

### Comparison dimensions (used by WP4)

Backend framework, language, template/view tech, build tool, htmx version, HTML
generation location, OOB vs hx-partial swap patterns, dev hot-reload story,
native-image support, main trade-offs / when to pick it.

## TODO

- [ ] WP1 — `docs/Variants.md` for the 2025 projects
- [ ] WP2 — add the 2026 projects to `docs/Variants.md`
- [ ] WP3 — `docs/History.md`
- [ ] WP4 — `docs/Variant-Comparison.md`
- [ ] WP5 — `docs/README.md` index + cross-links, `wip.md` cleanup

## Open items (original)

- create a file History.md which includes the main differences between the
  variants — planned as WP3 (`docs/History.md`).
- create a file Variant-Comparison.md which includes the main differences between
  the variants. Analysis of the projects will be needed to do this — planned as
  WP1/WP2 (inventory) + WP4 (`docs/Variant-Comparison.md`).
