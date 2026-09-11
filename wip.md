# Instructions for AI

This file serves as the working document for Claude. It contains information and
instructions so that the prompt on the command line can refer to this file.
It is a living document and is maintained as work on this project progresses.
Claude also keeps its list of TODOs in this file.

**Completed work packages, resolved open questions, and the full Thymeleaf
build-out log live in [`wip_done.md`](wip_done.md)** (split off 2026-09-11 to
keep this file short) — this file only tracks the project's live purpose /
scope / conventions and whatever is still open.

## Umbrella project's purpose

This project is a place for documentation of the various variants of my
hypermedia / htmx applications. Some sibling projects implement the same app in
different variants; others are just a PoC or demonstrate hypermedia/htmx patterns.

### Sibling projects (GitHub repos, all under `github.com/svene/`)

The project name *is* the repo name. Locally they are organised into `2025/` and
`2026/` sub-folders by start year, but on GitHub they are flat — so the docs
refer to them by name only. Full list + links: `docs/Variants.md`.

- 2025-08-23_ssfe-patterns-jte-vc-htmx
- 2025-08-23_ssfe-patterns-jte-htmx
- 2025-08-23_ssfe-patterns-thymeleaf-htmx
- 2025-12-21_ssfe-patterns-quarkus-qute-htmx
- 2025-12-27_ssfe-patterns-hono-htmx
- 2025-12-31-springboot-hono-poc
- 2026-01-24_hda-dynapage-demo
- 2026-03-07_springboot-graalvm-jsx-poc
- 2026-03-09_hda-springboot-graalvm-hono-demo
- 2026-03-15_hda-quarkus-graalvm-hono-demo
- 2026-09-03_hda-springboot-browser-hono
- 2026-09-03_hda-quarkus-browser-hono

### Additional notes

- The date prefixes of the project names indicate when each project was started
  and thus also reflect my learning experience over time.
- The timeline shows that I tried out various template engines for use with a Java
  web application.
- 2025-08-23_ssfe-patterns-thymeleaf-htmx: **built out 2026-09-06** (with Claude)
  — the fragment/slot take on the shared `m01/m03/m04/m05` course; htmx 4 +
  vendored assets. See "Thymeleaf variant build-out" in
  [`wip_done.md`](wip_done.md#thymeleaf-variant-build-out).
- Currently (September 2026) my preferred template engine is Hono/TS with its
  `html``` tagged template.
- The two `2026-09-03_hda-*-browser-hono` projects are the newest step: the same
  hono `html` templates, but rendered **in the browser** — `/uiroute/*` is a JSON
  API and a small htmx 4 extension runs the template client-side. The GraalVM
  rendering layer from the March demos was removed.
- `2026-05-01_springboot-hono-docs` (local only, not on GitHub) was a throwaway
  **experiment** to find out whether Astro / Starlight is a usable documentation
  tool for these apps/variants. It proved OK and is now superseded.
- `2026-05-02_hda-htmx-patterns-docs` is the **actual documentation
  project** that came out of that experiment: an Astro / Starlight site that
  extracts tagged snippets from the real variant source (`extract-snippets/`,
  output in the git-ignored `generated/`). It already documents the JTE-VC and
  Hono variants and is meant to show snippets from more variants over time. In a
  later step it can be extended into per-variant code-docs.

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
- `docs/Analysis-Baseline.md` — the commit hash each sibling project was at when
  the docs were written, so the docs can be refreshed against later upstream
  commits.
- `docs/README.md` — index of the above with the suggested reading order.

## Approach

- `docs/Variants.md` is written first as the shared reference; `History.md`,
  `Variant-Comparison.md` and `Learnings.md` build on it.
- All documentation output lives in `docs/` as Markdown.
- This repo only reads the sibling projects; it never modifies them.
- Work is split into work packages. Each work package is one manual git commit by
  the user. Claude stops after finishing a work package and reports; the user
  inspects and commits.

## Conventions

### Catalog entry shape

Per project, a few lines only: project name + start date, role (app variant /
PoC / pattern showcase / docs generator), the stack in one line, the one
distinguishing concept, current status, and "details: see the project". No
internals. A project ↔ GitHub-repo table sits at the top of `docs/Variants.md`.

### Comparison dimensions

Kept high-level: backend framework + language, where HTML is generated (in the
JVM / separate process / GraalVM polyglot), template/view technology as a
concept, how dynamic updates are done (full page / OOB / partial), and the main
trade-off / when this variant makes sense.

## Maintenance

- **Refreshing docs after upstream changes.** `docs/Analysis-Baseline.md` records
  the commit each sibling project was analysed at. To update: diff
  `<recorded-hash>..HEAD` in a project, revise the affected `docs/*.md`, then bump
  that project's row and the analysis date in `Analysis-Baseline.md`.
- `docs/Learnings.md` is a seed — the user extends it manually with reasoning that
  isn't visible in commit messages.

## TODO

- [ ] **_(optional, low priority)_ Build out `2025-08-23_ssfe-patterns-jte-htmx`** —
  it is a very simple demo project and does **not** cover all the patterns the
  other pattern-course projects (JTE-VC, Thymeleaf, Qute, Hono) share. Bringing
  it up to the full `m01/m03/m04/m05` course would make the family complete, but
  the user has flagged this as low priority. Update `docs/*` afterwards.

Everything else that was ever tracked here has shipped — see
[`wip_done.md`](wip_done.md) for the full work-package history (WP0…WP20,
WP-T*, WP-S*), the completed Future-work items, and the resolved open questions.
