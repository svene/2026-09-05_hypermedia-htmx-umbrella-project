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
- `2026-05-01_springboot-hono-docs` (local only, not on GitHub) was a throwaway
  **experiment** to find out whether Astro / Starlight is a usable documentation
  tool for these apps/variants. It proved OK and is now superseded.
- `2026-05-02_ssfe-patterns-jte-vc-htmx-docs` is the **actual documentation
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
| WP15 | DONE  | Wrote the "Architecture trade-offs — two-process vs GraalVM polyglot vs browser-hono" section in `docs/Variant-Comparison.md` (14-dimension table, per-architecture "Net", low-lock-in note). Closed the matching Future-work item; repointed `History.md` / `Learnings.md` / `docs/README.md`. |
| WP16 | DONE  | Staged `htmx4-upgrade-plan.md` in the 4 ready older projects (`jte-htmx`, `jte-vc-htmx`, `quarkus-qute-htmx`, `hono-htmx`) for the user to execute in separate sessions. Each plan: copy the htmx 4 asset from an already-upgraded sibling (`5a61350` SB / `77fc6c5` Quarkus), and a "Part 0" step to study those upgrade commits first. Thymeleaf skipped (variant not implemented). Future-work item updated with a per-project checklist. |
| WP17 | DONE  | Umbrella docs: corrected the 2026-05 framing. `2026-05-01_springboot-hono-docs` recast as a throwaway feasibility spike (Astro / Starlight as a docs tool — answered yes) and dropped from the repo table + `Analysis-Baseline.md`, kept only as a one-line footnote; `2026-05-02_ssfe-patterns-jte-vc-htmx-docs` recast as the real docs site (tagged-snippet extraction from live variant source; covers JTE-VC + Hono, sidebar scaffolded for the rest). Updated `Variants.md`, `History.md` (Phase 7), `Variant-Comparison.md`, `Learnings.md` #16, `Analysis-Baseline.md`, `wip.md` + Future-work bullets. |
| WP18 | DONE  | In `2026-05-02_ssfe-patterns-jte-vc-htmx-docs` (sibling repo — user commits there): `git mv README.md README_org.md`; rewrote `README1.md` with **Usage** (`npm install` → `npm run extract-snippets` → `npm run dev`, open `:4321`, note the `:3000` variant server for the demo iframes), **Dev cycle** (edit a variant's source → `npm run extract-snippets` rebuilds `generated/` → Starlight hot-reloads), a note on how to add a snippet, and the project's purpose. |
| WP19 | DONE  | Fixed the docs-snippet marker leak in `2025-12-27_ssfe-patterns-hono-htmx` (sibling repo — user commits there): in `src/m01html/m01d01.ts`…`m01d05.ts` (the only `html``` templates carrying inline markers) replaced `{/*docs:end page*/}` / `{/*docs:start page*/}` with `<!-- docs:end page -->` / `<!-- docs:start page -->`. `.tsx` modules untouched (real JSX comments there). Verified: re-ran `npm run extract-snippets` — `generated/` m01 snippets byte-identical (the `<a …>Docs</a>` back-link is still carved out), and the markers are now invisible HTML comments in the browser. |

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
  `docs/Analysis-Baseline.md` afterwards. **Started 2026-09-06** — plan and work
  packages in "[Thymeleaf variant build-out](#thymeleaf-variant-build-out)" below.
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
- ~~**"Which architecture for which use case."**~~ **Done** — written up as
  "Architecture trade-offs — two-process vs GraalVM polyglot vs browser-hono" in
  `docs/Variant-Comparison.md` (14-dimension table + a "Net" per architecture +
  a low-lock-in note). Extend it later with real-world operational experience as
  it accrues.
- **Bring the older projects up to the current htmx / asset conventions**
  (htmx 4 + vendored assets instead of webjars). **All 4 buildable projects done
  (2026-09-05); only Thymeleaf remains, blocked on that variant being
  implemented.** Each was executed by the user in a separate Claude session from
  its `htmx4-upgrade-plan.md`; umbrella docs (`Variants.md` /
  `Variant-Comparison.md` htmx columns, `Analysis-Baseline.md` rows) already
  updated per project.
  - `2025-08-23_ssfe-patterns-jte-htmx` → ☑ **done 2026-09-05, commit `e2cba81`**
    ("htmx4 upgrade"): htmx 4 vendored at `src/main/resources/static/js/htmx.org/4.0.0/`,
    webjar + `webjars-locator` removed from `pom.xml`, both script refs updated.
    Docs updated. Plan file to be deleted after the user merges.
  - `2025-08-23_ssfe-patterns-jte-vc-htmx` → ☑ **htmx4 done 2026-09-05, commit
    `7384f38`** (was `ae4901e`, amended): htmx 4 vendored at
    `src/main/resources/static/js/htmx.org/4.0.0/`, webjar + `webjars-locator`
    removed from `pom.xml`, all 4 `.jte` script refs updated. **Bulma also
    vendored 2026-09-05, commit `5089f49`** — `static/css/bulma/1.0.4/bulma.min.css`,
    webjar removed; this is the reference for the bulma-vendoring plan below.
    Plan file to be deleted after the user merges.
  - `2025-12-21_ssfe-patterns-quarkus-qute-htmx` → ☑ **done 2026-09-05, commit `431e0d2`**
    ("upgrade to htmx4"): htmx 4 vendored at `src/main/resources/META-INF/resources/js/htmx.org/4.0.0/`,
    htmx webjar removed from `pom.xml` (`quarkus-web-dependency-locator` kept for
    bulma), all 3 template script refs updated. Docs updated. Plan file to be
    deleted after the user merges.
  - `2025-12-27_ssfe-patterns-hono-htmx` → ☑ **done 2026-09-05, commit `3daf3da`**
    ("upgrade to htmx4"): htmx 4 vendored at `static/js/htmx.org/4.0.0/`, old
    2.0.8 removed, 3 script refs updated, `upgrade-check` clean, demos verified.
    `docs/Variants.md` / `docs/Variant-Comparison.md` / `docs/Analysis-Baseline.md`
    updated. Plan file to be deleted after the user merges.
  - `2025-08-23_ssfe-patterns-thymeleaf-htmx` — **no plan yet**; the variant is
    not implemented, so fold the htmx-4 + vendored setup into that build-out.

  Remaining: delete each project's `htmx4-upgrade-plan.md` once merged, and cover
  Thymeleaf as part of building that variant out.
- **Vendor bulma (versioned) everywhere, off webjars.** Reference:
  `2025-08-23_ssfe-patterns-jte-vc-htmx` commit `5089f49`. **Applied to all 8
  remaining projects on 2026-09-05 from this umbrella project** (working trees
  only — the user reviews/commits each): `quarkus-qute-htmx` off the webjar (and
  `quarkus-web-dependency-locator` dropped); the other 7 `git mv`'d their flat
  `css/bulma.min.css` into `css/bulma/1.0.4/` and repointed the `<link>` tags
  (plus stale `architecture.md` tree listings). `jte-htmx` has no bulma;
  Thymeleaf is un-built. **Done: all 8 committed + pushed 2026-09-05
  (`vendored bulma`); `docs/Analysis-Baseline.md` rows refreshed.**
  `bulma-vendoring-plan.md` can be deleted.
- ~~**`2025-12-27_ssfe-patterns-hono-htmx`: docs-snippet markers leak into the
  rendered page.**~~ **DONE via WP19 (2026-09-06)** — `{/*docs:*page*/}` → HTML
  comments in `src/m01html/m01d0{1..5}.ts`; extraction verified unchanged.
  Original context kept below. The M01 "Simple Pages using HTML Helper" demos (module
  `m01html`, routes `/m01/d01`…) show the literal text `{/*docs:start page*/}` /
  `{/*docs:end page*/}` in the browser. Cause: those files (`src/m01html/m01d0*.ts`,
  `src/components/*.ts`) build HTML with hono's `html``` tagged template, where
  `{/* … */}` is plain string content, not a comment — unlike the `.tsx` modules
  (m02–m05) where it is a real JSX expression comment and renders nothing.
  Pre-existing; **not** caused by the htmx 4 upgrade. Fix: in the `html```
  templates switch the markers to real HTML comments
  (`<!-- docs:start page -->` / `<!-- docs:end page -->`); the snippet extractor
  in the 2026-05 docs generators only does `line.includes('docs:start page')`, so
  comment syntax is irrelevant to extraction and an HTML comment is invisible in
  the browser. Grep `src` for `docs:start` / `docs:end` in `.ts` files.
  (Copied from that project's Claude memory so it can be dropped there.)
- Possibly extend `2026-05-02_ssfe-patterns-jte-vc-htmx-docs` into per-variant
  code-docs for every variant — its sidebar is already scaffolded for JTE,
  Thymeleaf, Hono/JSX, JSX-Spring-Hono and Graal-JSX (Spring / Quarkus). This
  umbrella project stays the high-level companion.
- **Decide the relationship to `2026-05-02_ssfe-patterns-jte-vc-htmx-docs`** — fold
  it into this umbrella project, or keep it separate. Not yet decided.
  (`2026-05-01_springboot-hono-docs` was only a feasibility spike — nothing to
  fold in.)

## Thymeleaf variant build-out

Plan for the "Implement the Thymeleaf variant" Future-work item. **Analysis done
2026-09-06; work packages below are for the user to review before implementation
starts.**

### Where the work happens

- All implementation edits are in the sibling repo
  `2025/2025-08-23_ssfe-patterns-thymeleaf-htmx` (currently a bare skeleton: one
  `page1.html`, one `PagesController`, empty `MyService`/`MyRepository`, htmx 2
  via webjars). Claude edits files only; **the user reviews and commits each work
  package** — in the Thymeleaf repo for WP-T0…WP-T4/WP-T6, in the Qute repo for
  the optional WP-T7, in this umbrella repo for WP-T5.
- This umbrella repo's usual "only reads the siblings" rule is deliberately
  suspended for this item — the user asked for the build-out to be done here with
  Claude.

### Reference projects and the target demo set

The **Quarkus/Qute course** (`2025-12-21_ssfe-patterns-quarkus-qute-htmx`) is the
structural model: it is the other "Java SSR template engine" course, so it
already shows what the module set looks like without JSX. The **JTE-VC project**
(`2025-08-23_ssfe-patterns-jte-vc-htmx`) is the Spring-Boot wiring model
(controllers, URL constants, `static/` asset layout, `main.css` / `simplepage.css`,
`maincard`, the per-demo code panel).

Module set — **same demos as Qute**, i.e. the full course **minus the JSX module
and minus the "Experiments" section** ("the one named 'experimental'" — only
JTE-VC has it: `main_09_experiments-section`, the "Swap Webcomponent" PoC —
excluded):

| Module | Keep? | Demos |
|--------|-------|-------|
| `m00` main menu | yes | landing page: card menu linking every demo |
| `m01` Simple Pages | yes | d01 basic page from a template · d02 page includes a fragment · d03 page + fragment with parameters · d04 content/slot parameter page→fragment · d05 nested fragments |
| `m02` JSX | **no** | not applicable to a Java template engine (Qute skips it too) |
| `m03` Page Patterns | yes | d01 content page · d02 content page taking a request param · d03 custom page taking a param · d04 MPA example (two pages sharing a nav layout) |
| `m04` UI Patterns | yes | d01 parent/child (slot content passed down) · d02 forwarder (fragment delegates to another) |
| `m05` htmx Patterns | yes | d01 URL components (button `hx-get`s a fragment endpoint, htmx swaps the result) |
| `m09` Experiments | **no** | "the one named 'experimental'" — excluded per the user |

→ 12 demo pages + the main menu. **Module numbers stay `m00/m01/m03/m04/m05`
(gap at `m02`)** so demos line up by number with the Qute variant for
cross-variant comparison.

### Design decisions (please confirm on review)

1. **Thymeleaf idioms, core only** — `th:fragment` / `th:insert` / `th:replace` /
   `~{…}` fragment expressions for insertion and slots; `th:fragment="name(p)"`
   for parameters. **No `thymeleaf-layout-dialect` dependency** — the project's
   own `notes.adoc` frames this as "fragments and slots", and core Thymeleaf
   covers every demo. Templates are natural-templating `.html` under
   `src/main/resources/templates/`.
2. **Package layout** `org.svenehrke.demo.ssfepatterns.m0X…` (mirrors Qute's
   `dev.svenehrke.demo.ssfepatterns.m0X…`). The skeleton's
   `web.PagesController`, `core.MyService`, `persistence.MyRepository` and
   `templates/pages/page1.html` are removed.
3. **htmx 4 + vendored assets from the start** — drop `org.webjars.npm:htmx.org`
   and `webjars-locator-lite` from `pom.xml`; vendor
   `static/js/htmx.org/4.0.0/htmx.js` and `static/css/bulma/1.0.4/bulma.min.css`
   copied from `2025-08-23_ssfe-patterns-jte-vc-htmx`. This also clears the open
   htmx-4 checklist line for Thymeleaf (see "Bring the older projects up…" above)
   — no separate `htmx4-upgrade-plan.md` needed.
4. **Per-demo code panel** — each demo page shows its own template + controller
   source in a code panel (Qute's `codeexplanation` / JTE-VC's `simplepage.css`
   `.codearea`). Backed by a small `CodeSnippet` record. Done as part of each
   module WP, not a separate WP.
5. **Out of scope now** (optional follow-ups): `docs:start`/`docs:end` snippet
   markers + `http://localhost:4321/…` "Docs" back-links for the
   `2026-05-02_ssfe-patterns-jte-vc-htmx-docs` extractor (WP-T6, only if wanted);
   native-image; tests beyond one context-loads smoke test.

### Work packages

Each row = one manual review + commit by the user. WP-T0…WP-T4 and WP-T6 commit
in the Thymeleaf repo; WP-T5 commits here.

| WP | Repo | Status | Deliverable |
|----|------|--------|-------------|
| WP-T0 | thymeleaf | **DONE 2026-09-06** | **Skeleton + shared infra + build.** `pom.xml` (htmx 4 vendored, `htmx.org` + `webjars-locator-lite` removed); `application.properties` (`spring.application.name`) + `application-dev.properties` (`spring.thymeleaf.cache=false`); vendored `static/js/htmx.org/4.0.0/htmx.js` (102 KB) + `static/css/bulma/1.0.4/bulma.min.css` (662 KB) + `static/main.css` + `static/simplepage.css` (copied from JTE-VC); shared fragments `fragments/layout.html` (`page(title, content)` via `~{}` fragment expr), `fragments/page-head.html` (`head(title)`), `fragments/maincard.html` (`card(url,title,subtitle,recommendation)`, `th:utext`), `fragments/code-panel.html` (`panel(snippets)` over `List<CodeSnippet>`) + `ssfepatterns/components/CodeSnippet` record; `ssfepatterns/m00main/MainController` serves `/` → `m00main/index.html` shell (title/subtitle + a placeholder comment where module sections go); removed `web/PagesController` + `core/MyService` + `persistence/MyRepository` + `templates/pages/page1.html`; `readme.adoc`. **Verified:** `mvn clean compile` green; `mvn spring-boot:run -Dspring-boot.run.profiles=dev` boots, `GET /` → 200 renders the shell, `/js/htmx.org/4.0.0/htmx.js` + `/css/bulma/1.0.4/bulma.min.css` + `/main.css` → 200. |
| WP-T1 | thymeleaf | **DONE 2026-09-06** | **m01 Simple Pages** — `m01simplepages/M01Controller` (one controller, `D01_URL`…`D05_URL`, `menuUrls()`) + `M01Snippets` (illustrative code-panel excerpts); templates `m01simplepages/d01…d05.html`; fragments `fragments/helloworld.html` (no-param), `helloworldparams.html` (`(greeting, greetee)`), `helloworldcontent.html` (`(content)` slot via `<th:block th:replace="${content}">`). d03 reads `?greetee=` (default "You"); d04 passes markup with `~{::#slot/content()}`; d05 nests the same fragment (`~{::#outer/content()}` → inner `~{::#nested/content()}`). `MainController` now `model.addAllAttributes(M01Controller.menuUrls())`; `m00main/index.html` gained the "Simple Pages" `<section>` (5 `maincard` calls). **Verified:** `mvn clean compile` green; app boots (dev); `GET /`, `/m01/d01`…`/m01/d05` (+`?greetee=World`) all → 200; d02 shows the fragment, d03 → "Hey World!", d04 → slot markup inside `.area-border`, d05 → nested `.area-border`, code panels populated, menu cards link correctly. |
| WP-T2 | thymeleaf | TODO | **m03 Page Patterns** — `M03` controllers incl. the two MPA pages sharing `fragments/m03d04-layout.html` (nav with selected state); `@RequestParam("greeting")` demos (d02/d03); code panels; `m00` "Page Patterns" section. |
| WP-T3 | thymeleaf | TODO | **m04 UI Patterns** — d01 parent/child (slot content via `~{}`), d02 forwarder (`th:if` delegates to a second fragment); code panels; `m00` "UI Patterns" section. |
| WP-T4 | thymeleaf | TODO | **m05 htmx Patterns** — `M05D01` page + `M05D01Message` fragment endpoint (`@RequestParam("message")`), button with `hx-get` / `hx-target`, result swapped in; code panel; `m00` "HTMX Patterns" section. Full course now runs. |
| WP-T5 | umbrella | TODO | **Umbrella docs catch-up.** `docs/Variants.md` (status → built; htmx 4; module-course description). `docs/Variant-Comparison.md` (Thymeleaf row → `in the JVM` / `Thymeleaf fragments/slots` / built / htmx **4**; drop the "only scaffolded" caveat + the "not built out" aside). `docs/History.md` (Phase 1 Thymeleaf line: implemented 2026-09 as the fragment/slot take on the course). `docs/Learnings.md` (#14 "unfinished experiments" + the confirmed-by-user Thymeleaf line). `docs/Analysis-Baseline.md` (bump the Thymeleaf row hash + date to the user's WP-T4 commit). `wip.md` (this section → DONE; tick the Thymeleaf htmx-4 checklist line). |
| WP-T6 | thymeleaf | OPTIONAL | **Docs-extraction hooks** — add `docs:start`/`docs:end` markers and `http://localhost:4321/technologies/…` "Docs" back-links to the demo templates/controllers, mirroring the JTE-VC demos, so `2026-05-02_ssfe-patterns-jte-vc-htmx-docs` can extract Thymeleaf snippets. Only if the user wants it. |
| WP-T7 | qute | OPTIONAL | **Delete greeting leftovers from `2025-12-21_ssfe-patterns-quarkus-qute-htmx`** — the user confirmed the greeting bits are archetype leftovers "from the very beginning" and can go: `org/acme/GreetingResource.java` + its `*Test`/`*IT`, `HomeResource` + `home.html`, `p01greeting/` + `greetingpage.html`. Its own review + commit; scope-check the exact file list against that repo first. |

### Open choices — resolved (2026-09-06, by the user)

- **One `M0XController` per module** (not one class per demo). Applied from WP-T1 on.
- **`p01` greeting page: skip it.** The greeting demos are archetype leftovers
  "from the very beginning"; not replicated in Thymeleaf, and can be deleted from
  the Qute project — tracked as optional **WP-T7**.

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
   **clarified (2026-09-06):** `2026-05-01_springboot-hono-docs` was only a
   feasibility spike (Astro / Starlight as a docs tool); `2026-05-02_ssfe-patterns-jte-vc-htmx-docs`
   is the real docs project. Whether to fold the latter in is still **not decided
   yet**; kept in Future work.
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
