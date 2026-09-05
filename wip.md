# Instructions for AI

This file serves as the working document for Claude. It contains information and
instructions so that the prompt on the command line can refer to this file.
It is a living document and is maintained as work on this project progresses.
Claude also keeps its list of TODOs in this file.

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
- 2026-03-09_hda-springboot-graalvm-jsx-demo
- 2026-03-15_hda-quarkus-graalvm-jsx-demo
- 2026-09-03_hda-springboot-browser-hono
- 2026-09-03_hda-quarkus-browser-hono

### Additional notes

- The date prefixes of the project names indicate when each project was started
  and thus also reflect my learning experience over time.
- The timeline shows that I tried out various template engines for use with a Java
  web application.
- 2025-08-23_ssfe-patterns-thymeleaf-htmx: only started, still needs to be
  implemented like the JTE variants. Planned to be built out later with Claude
  (see "Future work" below).
- Currently (September 2026) my preferred template engine is Hono/TS with its
  `html``` tagged template.
- The two `2026-09-03_hda-*-browser-hono` projects are the newest step: the same
  hono `html` templates, but rendered **in the browser** — `/uiroute/*` is a JSON
  API and a small htmx 4 extension runs the template client-side. The GraalVM
  rendering layer from the March demos was removed.
- There are also `2026-05-01_springboot-hono-docs` (local only, not on GitHub) and
  `2026-05-02_ssfe-patterns-jte-vc-htmx-docs` which I think I created to generate
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

## Work packages

| WP  | Status | Deliverable |
|-----|--------|-------------|
| WP0 | DONE   | This `wip.md` rewrite (plan + TODO list) and umbrella `README.md`. |
| WP1 | DONE   | `docs/Variants.md` — lightweight catalog of all sibling projects (concept + role + pointer). |
| WP2 | DONE   | `docs/History.md` — chronological story of concepts adopted / dropped and why. |
| WP3 | DONE   | `docs/Variant-Comparison.md` — concept- and architecture-level comparison. |
| WP4 | DONE   | `docs/Learnings.md` — learnings seeded from the observable history (user extends later). |
| WP5 | DONE   | `docs/Analysis-Baseline.md` (per-project commit hashes), `docs/README.md` index + cross-links, `README.md` refresh, `wip.md` cleanup. |
| WP6 | DONE   | Follow-up: Java→TS codegen confirmed as preference + per-project audit (`docs/Learnings.md`), threaded through `History.md` / `Variant-Comparison.md` / `Variants.md`; "Open questions" section added below. |
| WP7 | DONE   | Added the two `2026-09-03_hda-*-browser-hono` projects (browser-side rendering) across all docs: sibling list, `Variants.md` (new section), `Analysis-Baseline.md`, `Variant-Comparison.md` (new Axis-1 model + matrix/axes), `History.md` (new Phase 8), READMEs. |
| WP8 | DONE   | Resolved open questions 1 & 3: `jsx` in folder names is historical (repo-rename item added to Future work); `hda-dynapage-demo` still runs the `typescript-generator` (Java→TS) plugin — audit table corrected. |
| WP9 | DONE   | Resolved open questions 4, 5 & 10: GraalVM `Context` is not thread-safe (reason for the pool); two-process / GraalVM / browser-hono are all valid, use-case-dependent. Added "which architecture for which use case" to Future work; updated `Learnings.md`, `History.md`, `Variant-Comparison.md`. |
| WP10 | DONE  | Resolved open question 6: older projects are on htmx 2 via webjars. Added a Future-work task to upgrade them to htmx 4 and switch to the vendored `static/js/...` asset approach. |
| WP11 | DONE  | Resolved open question 7: `dynapage-demo` is a copy of `springboot-hono-poc`; the user does this often and it should NOT be documented publicly. Noted internally in Claude memory. |
| WP12 | DONE  | Resolved open questions 8 & 9: docs-generator relationship undecided → added to Future work; Thymeleaf variant still wanted (no blocker, just deprioritised) → Future-work entry updated. |
| WP13 | DONE  | Decision: `2026-03-07_springboot-graalvm-jsx-poc` stays a historical PoC (no codegen migration). Added a "deliberately not updated" note to its `readme.md`; closed the "Codegen-direction consistency" Future-work item; updated `Learnings.md` / `Variants.md` / `Variant-Comparison.md`. |
| WP14 | DONE  | Replaced all relative directory references (`../…`, `../../2025/…`) with plain project names, since the repos are flat on GitHub. Added a project ↔ GitHub-repo table at the top of `docs/Variants.md` (repos under `github.com/svene/`; `springboot-hono-docs` is local-only). Updated `Analysis-Baseline.md`, both READMEs, `wip.md`. |

### Catalog entry shape (WP1)

Per project, a few lines only: project name + start date, role (app variant /
PoC / pattern showcase / docs generator), the stack in one line, the one
distinguishing concept, current status, and "details: see the project". No
internals. A project ↔ GitHub-repo table sits at the top of `docs/Variants.md`.

### Comparison dimensions (WP3)

Kept high-level: backend framework + language, where HTML is generated (in the
JVM / separate process / GraalVM polyglot), template/view technology as a
concept, how dynamic updates are done (full page / OOB / partial), and the main
trade-off / when this variant makes sense.

## TODO

All initial work packages are done.

- [x] WP1 — `docs/Variants.md` (all projects, lightweight)
- [x] WP2 — `docs/History.md`
- [x] WP3 — `docs/Variant-Comparison.md`
- [x] WP4 — `docs/Learnings.md` (seed only)
- [x] WP5 — `docs/Analysis-Baseline.md`, `docs/README.md`, `README.md`, cleanup

The two original open items are covered: `History.md` by WP2, `Variant-Comparison.md`
by WP1 (catalog) + WP3.

## Maintenance

- **Refreshing docs after upstream changes.** `docs/Analysis-Baseline.md` records
  the commit each sibling project was analysed at. To update: diff
  `<recorded-hash>..HEAD` in a project, revise the affected `docs/*.md`, then bump
  that project's row and the analysis date in `Analysis-Baseline.md`.
- `docs/Learnings.md` is a seed — the user extends it manually with reasoning that
  isn't visible in commit messages.

## Future work

- **Implement the Thymeleaf variant** (`2025-08-23_ssfe-patterns-thymeleaf-htmx`)
  with Claude, mirroring the JTE variants' patterns. Still wanted — brought to the
  same state as the other variants — but not top priority so far; no specific
  blocker. Update `docs/Variants.md`, `docs/Variant-Comparison.md` and
  `docs/Analysis-Baseline.md` afterwards.
- **Rename the `jsx` repos.** The `jsx` in `2026-03-07_springboot-graalvm-jsx-poc`,
  `2026-03-09_hda-springboot-graalvm-jsx-demo` and
  `2026-03-15_hda-quarkus-graalvm-jsx-demo` is historical — they use hono `html`
  tagged templates, not JSX (except the `2026-03-07` PoC, which still has `.tsx`).
  Rename e.g. `…graalvm-jsx-demo` → `…graalvm-hono-demo`, then update the project
  names in `docs/*` (the repo table in `docs/Variants.md` and
  `docs/Analysis-Baseline.md` included).
- ~~**Codegen-direction consistency.**~~ **Decided (2026-09-05):**
  `2026-03-07_springboot-graalvm-jsx-poc` stays as a **historical PoC** — it keeps
  `.tsx` and TS→Java generation. A "historical PoC, deliberately not updated" note
  was added to its `readme.md`. All other projects are on Java→TS
  (`docs/Learnings.md` audit table). No further action.
- **"Which architecture for which use case."** The two-process (Java → Hono over
  HTTP), the GraalVM-polyglot, and the browser-hono architectures are all
  considered valid for hypermedia/htmx webapps — the right choice depends on the
  use case. Write this up as guidance (extends the "When each model makes sense"
  table in `docs/Variant-Comparison.md`).
- **Bring the older projects up to the current htmx / asset conventions.** For the
  projects still on **htmx 2 loaded via webjars** — `2025-08-23_ssfe-patterns-jte-htmx`,
  `2025-08-23_ssfe-patterns-jte-vc-htmx`, `2025-08-23_ssfe-patterns-thymeleaf-htmx`
  (once implemented), `2025-12-21_ssfe-patterns-quarkus-qute-htmx` — and the
  vendored-but-still-v2 `2025-12-27_ssfe-patterns-hono-htmx`:
  1. upgrade to **htmx 4**;
  2. drop the `/webjars/htmx.org/...` approach and instead **vendor** the htmx
     (and hyperscript / Alpine) files into the repo under `static/js/...`, as the
     2026 projects do.
  Update `docs/Variants.md` / `docs/Variant-Comparison.md` htmx-version columns
  and `docs/Analysis-Baseline.md` afterwards.
- Possibly extend the 2026-05 docs-generator projects to emit per-variant
  code-docs; this umbrella project stays the high-level companion.
- **Decide the relationship to the 2026-05 docs-generator projects**
  (`springboot-hono-docs`, `ssfe-patterns-jte-vc-htmx-docs`) — fold them into this
  umbrella project, or keep them separate. Not yet decided.

## Open questions

Collected while analysing the projects. All items below are resolved or moved to
Future work; kept here as a record. Each is also noted in the relevant
`docs/*.md`.

1. ~~`2026-03-09` / `2026-03-15` folder names say `...jsx...`~~ — **resolved:**
   `jsx` is historical, they use `html``` templates. Repo rename added to Future
   work.
2. **Codegen direction not uniform** — accepted; tracked in Future work.
   `2026-03-07_springboot-graalvm-jsx-poc` still uses TS→Java.
3. ~~`hda-dynapage-demo` — is any generator still in use?~~ — **resolved:** yes,
   the `typescript-generator` Maven plugin (Java→TS) is still active in
   `springboot/pom.xml`, generating `vm-types.d.ts`. Only the old *TS→Java*
   generator was removed. Nothing to remove.
4. ~~GraalVM boundary tuning — measured numbers or judgement calls?~~ —
   **resolved:** a **GraalVM `Context` is not thread-safe**, so the pool (and the
   engine/source vs context split) is a *correctness* requirement, not a
   perf-tuning guess. JSON-string passing / entry-function caching are the
   related optimisations on top.
5. ~~Two-process architecture — fully retired?~~ — **resolved:** not retired. The
   two-process, GraalVM, and browser-hono architectures are **all valid**; the
   choice is use-case-dependent. See the "which architecture for which use case"
   Future-work entry.
6. ~~htmx versions of the 2025 Java variants — assumed 2.x, not verified.~~ —
   **resolved:** they are on htmx 2 via webjars (`/webjars/htmx.org/...`).
   Converted into a Future-work task: upgrade to htmx 4 and switch to the vendored
   `static/js/...` approach used by the 2026 projects.
7. ~~`springboot-hono-poc` vs `hda-dynapage-demo` share identical early git
   history — forked?~~ — **resolved:** yes, `dynapage-demo` is a copy of
   `springboot-hono-poc`. The user has done this for several of these projects.
   It is an irrelevant implementation detail — **do not document project-copy
   lineage in the public docs.**
8. ~~The two 2026-05 docs-generator projects — fold in or keep separate?~~ —
   **not decided yet**; moved to Future work.
9. ~~Thymeleaf stall reason?~~ — **resolved:** no specific blocker. The user still
   wants it brought to the same state as the other variants; it just has not been
   the top priority. Tracked in Future work.
10. ~~Browser-side rendering vs GraalVM SSR — which is the future direction?~~ —
    **resolved:** neither supersedes the other; both (plus two-process) are valid,
    use-case-dependent choices. Covered by the "which architecture for which use
    case" Future-work entry.
11. ~~`2026-03-09` codegen wording — corrected from "regenerate Java from TS" to
    Java→TS.~~ — **resolved by evidence:** its `pom.xml` runs
    `typescript-generator-maven-plugin` + gmavenplus (Java→TS), matching commit
    `5ecb2e7 switched from TS->Java to Java->TS`. Flag if this is wrong.
