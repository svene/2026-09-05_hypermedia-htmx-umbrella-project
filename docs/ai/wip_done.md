# Completed work log

Split off from `wip.md` on 2026-09-11 to keep the active working document short
(both moved into `docs/ai/` alongside `Analysis-Baseline.md` on 2026-09-12, to
keep AI-facing tracking separate from the user-facing docs in `docs/`).
Everything below is **finished** — kept here as a record. See
`../../README.md` / `../../README_details.md` for the project's purpose and
scope, `wip.md` for Claude's working conventions and whatever is still open.

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
| WP17 | DONE  | Umbrella docs: corrected the 2026-05 framing. `2026-05-01_springboot-hono-docs` recast as a throwaway feasibility spike (Astro / Starlight as a docs tool — answered yes) and dropped from the repo table + `Analysis-Baseline.md`, kept only as a one-line footnote; `2026-05-02_hda-htmx-patterns-docs` recast as the real docs site (tagged-snippet extraction from live variant source; covers JTE-VC + Hono, sidebar scaffolded for the rest). Updated `Variants.md`, `History.md` (Phase 7), `Variant-Comparison.md`, `Learnings.md` #16, `Analysis-Baseline.md`, `wip.md` + Future-work bullets. |
| WP18 | DONE  | In `2026-05-02_hda-htmx-patterns-docs` (sibling repo — user commits there): `git mv README.md README_org.md`; rewrote `README1.md` with **Usage** (`npm install` → `npm run extract-snippets` → `npm run dev`, open `:4321`, note the `:3000` variant server for the demo iframes), **Dev cycle** (edit a variant's source → `npm run extract-snippets` rebuilds `generated/` → Starlight hot-reloads), a note on how to add a snippet, and the project's purpose. |
| WP19 | DONE  | Fixed the docs-snippet marker leak in `2025-12-27_ssfe-patterns-hono-htmx` (sibling repo — user commits there): in `src/m01html/m01d01.ts`…`m01d05.ts` (the only `html``` templates carrying inline markers) replaced `{/*docs:end page*/}` / `{/*docs:start page*/}` with `<!-- docs:end page -->` / `<!-- docs:start page -->`. `.tsx` modules untouched (real JSX comments there). Verified: re-ran `npm run extract-snippets` — `generated/` m01 snippets byte-identical (the `<a …>Docs</a>` back-link is still carved out), and the markers are now invisible HTML comments in the browser. |
| WP20 | **DONE 2026-09-09** | **Made the two project groups explicit in the docs.** `docs/Variants.md`: new "**Two groups of projects**" intro (Group A · SSFE pattern showcases / Group B · "person" use-case apps / docs tooling); a **Group** column added to the project↔repo table; the catalog restructured under `## Group A` / `## Group B` / `## Documentation tooling` headings with the era sub-sections demoted to `###` and project entries to `####` (heading-anchor slugs unchanged, so cross-links still resolve). `docs/README.md`: the Variants.md entry in the reading order now leads with the two groups. `docs/Variant-Comparison.md`: **Group** column in the overview matrix, scope paragraph notes that most axes only vary within Group B, Axis-4 bullet expanded. **`hda-dynapage-demo` entry rewritten** — confirmed against the repo (`hono/src/app/parts/`): it builds the editable-table screen **four ways** as separate app parts — `p01` OOB swap, `p04` `hx-partial`, `p02` event-driven/JSX (response is a client-side event, Alpine receiver, no HTML), `p03` event-driven/HTML — not just "OOB vs `hx-partial`". Files: `docs/Variants.md`, `docs/README.md`, `docs/Variant-Comparison.md`. **Corrected 2026-09-11:** `hx-partial` was only claimed more readable than its sibling swap mechanism **OOB** (the user's own preference) — not "most readable of all four", which had wrongly implied it beat the two event-driven takes too. Fixed in `Variants.md`, `Variant-Comparison.md`, `Learnings.md` #13. |
| WP21 | **DONE 2026-09-11** | **Terminology: "SSFE" → "Hypermedia" in umbrella-docs prose** (repo names unchanged — see **WP22** in `wip.md`). "SSFE" (server-side front end) was coined as a contrast to Angular-style client-side frontends, but reads less clearly than "Hypermedia" / "Hypermedia-Driven (Web) App" — and the newer `hda-*` project prefix already stands for "Hypermedia-Driven Application", so this unifies vocabulary that had split across two eras. Replaced every descriptive "SSFE" mention with "Hypermedia": `docs/Variants.md` (Group A label ×2, 2 "Distinguishing idea" bullets), `docs/Variant-Comparison.md` (scope paragraph, which now also flags the pending repo rename), `README.md`, `README_details.md`. **Left untouched:** the literal `ssfe-patterns-*` repo names (always in backticks, as identifiers) everywhere they're cited — those still name the real, not-yet-renamed repos. |
| WP23 | **DONE 2026-09-12** | **Separated AI-facing tracking from user-facing docs, and added an `update-docs` skill.** `git mv wip.md wip_done.md docs/Analysis-Baseline.md` all into a new `docs/ai/` folder (kept together since they're the same kind of Claude-bookkeeping content — `wip_done.md` wasn't explicitly named in the request but clearly belongs). Fixed every cross-reference: real markdown links got corrected relative paths (`wip.md`'s links to `README.md`/`README_details.md` → `../../`), `Analysis-Baseline.md`'s link to `Variants.md` → `../Variants.md`, and prose mentions in `README.md`, `README_details.md`, `docs/Variants.md`, `docs/Variant-Comparison.md` now say `docs/ai/wip.md` / `docs/ai/Analysis-Baseline.md`. `README.md`'s "Documents" reading-order list dropped `Analysis-Baseline.md` (it's not user reading material) and the "Working notes" section now lists all three `docs/ai/*` files with a one-line explanation each. `README_details.md` gained an "AI-facing tracking files" section explaining the split. Historical mentions of the old paths in this file's own past WP rows (and `docs/README.md`, deleted earlier) were left as accurate-at-the-time records, per established precedent. <br> **New skill** `.claude/skills/update-docs/SKILL.md` — formalizes "update the docs" as a repeatable operation: read `docs/ai/Analysis-Baseline.md`, resolve each sibling's local checkout path (`../../<year>/<project-name>`, split by the year in the project's own name), `git log --oneline <hash>..HEAD` per project, judge doc-relevance against the project's high-level-only scope rule, update the affected `docs/*.md`, bump that project's baseline row + analysis date, then report and stop (Claude edits, user commits — no change to that rule). |

## Future work (completed)

- ~~**Implement the Thymeleaf variant**~~ **DONE 2026-09-06** (with Claude) —
  `2025-08-23_ssfe-patterns-thymeleaf-htmx` built out as the fragment/slot take on
  the shared `m01/m03/m04/m05` course (WP-T0…WP-T4 + WP-T2.5; plan and per-WP
  detail in "[Thymeleaf variant build-out](#thymeleaf-variant-build-out)" below).
  `docs/Variants.md`, `docs/Variant-Comparison.md`, `docs/History.md`,
  `docs/Learnings.md` and `docs/Analysis-Baseline.md` updated (WP-T5). Left open:
  the docs-project side (**WP-T6**) and the two Qute clean-ups (**WP-T7**,
  **WP-T9**).
- ~~**Rename the `jsx` repos.**~~ **DONE 2026-09-09 (WP-T10c).** The two GraalVM
  *demo* repos are now `…graalvm-hono-demo` (they use hono `html``` tagged
  templates, not JSX); `2026-03-07_springboot-graalvm-jsx-poc` keeps its name
  (still `.tsx` + TS→Java, a deliberate historical PoC). Names swept across
  `docs/*` + `wip.md` and the affected sibling repos — see WP-T10c in
  "[Rename work packages](#rename-work-packages-wp-t10b-wp-t10c)".
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
  (htmx 4 + vendored assets instead of webjars). **All done** — the 4 buildable
  projects on 2026-09-05, and Thymeleaf on 2026-09-06 (htmx 4 + vendored
  `static/js|css` folded straight into WP-T0 of its build-out; no plan file
  needed). Each of the 4 was executed by the user in a separate Claude session from
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
  - `2025-08-23_ssfe-patterns-thymeleaf-htmx` → ☑ **done 2026-09-06** as WP-T0 of
    the variant build-out: htmx 4 vendored at
    `src/main/resources/static/js/htmx.org/4.0.0/`, bulma 1.0.4 at
    `static/css/bulma/1.0.4/`, `htmx.org` + `webjars-locator-lite` removed from
    `pom.xml`. No `htmx4-upgrade-plan.md` was needed (built on htmx 4 directly).

  Remaining: delete each of the 4 older projects' `htmx4-upgrade-plan.md` once
  merged.
- **Vendor bulma (versioned) everywhere, off webjars.** Reference:
  `2025-08-23_ssfe-patterns-jte-vc-htmx` commit `5089f49`. **Applied to all 8
  remaining projects on 2026-09-05 from this umbrella project** (working trees
  only — the user reviews/commits each): `quarkus-qute-htmx` off the webjar (and
  `quarkus-web-dependency-locator` dropped); the other 7 `git mv`'d their flat
  `css/bulma.min.css` into `css/bulma/1.0.4/` and repointed the `<link>` tags
  (plus stale `architecture.md` tree listings). `jte-htmx` has no bulma;
  Thymeleaf got bulma 1.0.4 vendored directly in its build-out (WP-T0,
  2026-09-06). **Done: all 8 committed + pushed 2026-09-05
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
- ~~**Every pattern variant documented in `2026-05-02_hda-htmx-patterns-docs`**~~
  **DONE** — JTE-VC (`01_JTE-VC`, `mNN`), Thymeleaf (**WP-T6**), Hono, Qute
  (**WP-T10**); taxonomy tidy-up + `sNN`→`mNN` done (**WP-T11**); the docs-project
  folder/repo rename done (**WP-T10b**). The JSX / Spring-Hono / Graal-JSX sidebar
  rows stay out of scope. This umbrella project stays the high-level companion.
- ~~**Playwright e2e tests for every pattern project**~~ **DONE 2026-09-07** via
  **WP-T12** — a self-contained `playwright/` folder per project (5 total),
  modelled on the browser-hono demos. All 5 suites verified green.
- ~~**Make the two project groups explicit in the docs**~~ **DONE 2026-09-09
  (WP20).** `docs/Variants.md` restructured under `## Group A — SSFE pattern
  showcases` / `## Group B — "person" use-case apps` / `## Documentation tooling`,
  with a "Two groups of projects" intro and a **Group** column in the repo table;
  `docs/README.md` + `docs/Variant-Comparison.md` echo the split; the
  `hda-dynapage-demo` entry now names all four htmx update strategies it builds
  (OOB / `hx-partial` / event-JSX / event-HTML), confirmed against the repo.
- ~~**Standardise on `sNN` naming (`s` = *series*, `d` = *demo*)**~~ **DONE
  2026-09-06** via WP-S1…WP-S4 (see the "sNN standardisation" table below). The
  Thymeleaf, Qute and Hono variant apps (packages, class names, routes, template
  folders, in-app Docs back-links) and every docs-site page + extractor now use
  `sNN`. `2025-08-23_ssfe-patterns-jte-vc-htmx` was already `sNN` and was left
  as-is (its stale `/demos/sNN/` back-links were repointed to the real
  `/technologies/01_jte-vc/sNN/` path). Renaming that project's files to `mNN`
  for consistency was considered and rejected — `s` is the target.
- ~~**Decide the relationship to the docs project**~~ **Decided (2026-09-06): keep
  it separate.** `2026-05-02_hda-htmx-patterns-docs` serves a **different
  purpose** from this umbrella project and is not to be folded in:
  - **This umbrella project** — high-level only: concepts, the architectural idea
    per variant, cross-variant differences, the timeline, learnings. Prose, no
    code extraction.
  - **The docs project** — per-variant, code-level: hand-written prose *plus* code
    samples **extracted from the real variant source** by `docs:start`/`docs:end`
    markers, page-per-module, with live demo `<iframe>`s. It documents *how one
    variant works*, in detail.

  They are companions, not duplicates: the umbrella links out to the docs project
  for the details; the docs project doesn't try to compare variants.
  (`2026-05-01_springboot-hono-docs` was only a feasibility spike — nothing to
  fold in either way.)

## Thymeleaf variant build-out

Plan for the "Implement the Thymeleaf variant" Future-work item. **Analysis done
2026-09-06; work packages below are for the user to review before implementation
starts.**

### Where the work happens

- All implementation edits are in the sibling repo
  `2025/2025-08-23_ssfe-patterns-thymeleaf-htmx` (currently a bare skeleton: one
  `page1.html`, one `PagesController`, empty `MyService`/`MyRepository`, htmx 2
  via webjars). Claude edits files only; **the user reviews and commits each work
  package** — in the Thymeleaf repo for WP-T0…WP-T4 + WP-T2.5, in the Qute repo
  for WP-T7 + WP-T9, in the docs-project repo for WP-T6, in this umbrella repo for
  WP-T5.
- This umbrella repo's usual "only reads the siblings" rule is deliberately
  suspended for this item — the user asked for the build-out to be done here with
  Claude.

### Reference projects and the target demo set

The **Quarkus/Qute course** (`2025-12-21_ssfe-patterns-quarkus-qute-htmx`) is the
structural model: it is the other "Java SSR template engine" course, so it
already shows what the module set looks like without JSX. The **JTE-VC project**
(`2025-08-23_ssfe-patterns-jte-vc-htmx`) is the Spring-Boot wiring model
(controllers, URL constants, `static/` asset layout, `main.css` / `simplepage.css`,
`maincard`). JTE-VC also shows how the in-app code docs were *removed* again and
replaced by `docs:start`/`docs:end` markers + a "Docs" back-link once the write-ups
moved to `2026-05-02_hda-htmx-patterns-docs` (commits `9e94470` →
`6dc16fb`) — Thymeleaf follows that end state, not the earlier code-panel one (see
decision 4 and WP-T2.5).

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
4. ~~**Per-demo code panel**~~ **Reversed 2026-09-06 by the user.** WP-T1/WP-T2
   built the in-app code panels (`CodeSnippet` record, `code-panel.html`,
   `M01Snippets`/`M03Snippets`); the user then pointed out JTE-VC did the same
   thing early on and later *pulled the docs out* into
   `2026-05-02_hda-htmx-patterns-docs`, leaving only `docs:start`/
   `docs:end` markers + a `<hr>` + "Docs" back-link in each demo (commits
   `9e94470`…`6dc16fb`). **WP-T2.5 removes the panels and applies that same
   pattern**; WP-T3/WP-T4 are built that way from the start (no panels). The
   Thymeleaf snippet pages + extractor on the docs-project side are WP-T6.
5. **Out of scope now** (optional follow-ups): authoring the Thymeleaf `.mdx`
   pages + a snippet extractor inside `2026-05-02_hda-htmx-patterns-docs`
   (WP-T6); native-image; tests beyond one context-loads smoke test.

### Work packages

Each row = one manual review + commit by the user. WP-T0…WP-T4 + WP-T2.5 commit
in the Thymeleaf repo; WP-T5 commits here; WP-T7 + WP-T9 in the Qute repo;
**WP-T6 and WP-T10 are two commits each** (a variant/sibling repo + the
docs-project repo); WP-T11 is one docs-project commit; WP-T12 spans every pattern
project. The manual-rename work packages (**WP-T10b**, **WP-T10c**) are split
into their own list — see "[Rename work packages](#rename-work-packages-wp-t10b-wp-t10c)"
below.

WP-T6…WP-T12 are follow-ups that came out of the Thymeleaf build-out but reach
past it: the docs site now covers more than Thymeleaf, and the user asked for the
Qute variant to get the same in-app→docs migration and for every pattern project
to get Playwright tests.

| WP | Repo | Status | Deliverable |
|----|------|--------|-------------|
| WP-T0 | thymeleaf | **DONE 2026-09-06** | **Skeleton + shared infra + build.** `pom.xml` (htmx 4 vendored, `htmx.org` + `webjars-locator-lite` removed); `application.properties` (`spring.application.name`) + `application-dev.properties` (`spring.thymeleaf.cache=false`); vendored `static/js/htmx.org/4.0.0/htmx.js` (102 KB) + `static/css/bulma/1.0.4/bulma.min.css` (662 KB) + `static/main.css` + `static/simplepage.css` (copied from JTE-VC); shared fragments `fragments/layout.html` (`page(title, content)` via `~{}` fragment expr), `fragments/page-head.html` (`head(title)`), `fragments/maincard.html` (`card(url,title,subtitle,recommendation)`, `th:utext`), `fragments/code-panel.html` (`panel(snippets)` over `List<CodeSnippet>`) + `ssfepatterns/components/CodeSnippet` record; `ssfepatterns/m00main/MainController` serves `/` → `m00main/index.html` shell (title/subtitle + a placeholder comment where module sections go); removed `web/PagesController` + `core/MyService` + `persistence/MyRepository` + `templates/pages/page1.html`; `readme.adoc`. **Verified:** `mvn clean compile` green; `mvn spring-boot:run -Dspring-boot.run.profiles=dev` boots, `GET /` → 200 renders the shell (the `CodeSnippet` record + `code-panel.html` here were later removed in WP-T2.5), `/js/htmx.org/4.0.0/htmx.js` + `/css/bulma/1.0.4/bulma.min.css` + `/main.css` → 200. |
| WP-T1 | thymeleaf | **DONE 2026-09-06** | **m01 Simple Pages** — `m01simplepages/M01Controller` (one controller, `D01_URL`…`D05_URL`, `menuUrls()`) + `M01Snippets` (illustrative code-panel excerpts); templates `m01simplepages/d01…d05.html`; fragments `fragments/helloworld.html` (no-param), `helloworldparams.html` (`(greeting, greetee)`), `helloworldcontent.html` (`(content)` slot via `<th:block th:replace="${content}">`). d03 reads `?greetee=` (default "You"); d04 passes markup with `~{::#slot/content()}`; d05 nests the same fragment (`~{::#outer/content()}` → inner `~{::#nested/content()}`). `MainController` now `model.addAllAttributes(M01Controller.menuUrls())`; `m00main/index.html` gained the "Simple Pages" `<section>` (5 `maincard` calls). **Verified:** `mvn clean compile` green; app boots (dev); `GET /`, `/m01/d01`…`/m01/d05` (+`?greetee=World`) all → 200; d02 shows the fragment, d03 → "Hey World!", d04 → slot markup inside `.area-border`, d05 → nested `.area-border`, code panels populated, menu cards link correctly. |
| WP-T2 | thymeleaf | **DONE 2026-09-06** | **m03 Page Patterns** — `m03pages/M03Controller` (`D01_URL`…`D03_URL`, `D04P1_URL`/`D04P2_URL`, `menuUrls()`) + `M03Snippets`. d01 content page via the shared `fragments/layout.html`; d02 same + `@RequestParam("greeting")` (default "Hello"); d03 custom page — builds its own document, only reuses `fragments/page-head` — + the same param; d04 MPA = `d04p1`/`d04p2` sharing new `fragments/m03d04-layout.html` (`layoutMpa(content)`; nav highlight from `selectedMenu`, `p1Url`/`p2Url` model attrs). `MainController` +`M03Controller.menuUrls()`; `m00main/index.html` +"Page Patterns" `<section>` (4 cards). Also fixed a WP-T0 carry-over: the multi-line HTML comment inside `fragments/layout.html` leaked into every page — converted it (and the new m03d04-layout one) to a Thymeleaf `<!--/* */-->` parser comment. **Verified:** `mvn clean compile` green; app boots; `GET /`, `/m03/d01`, `/m03/d02` (+`?greeting=Hey You!` and default), `/m03/d03?greeting=…`, `/m03/d04p1`, `/m03/d04p2` all → 200; d02/d03 echo the greeting, d03 renders its own `<head>`, d04p1/p2 nav shows `is-selected` on the current page, menu cards + query strings correct. |
| WP-T2.5 | thymeleaf | **DONE 2026-09-06** | **Drop the in-app code-snippet docs** (user request — mirror JTE-VC commits `9e94470`…`6dc16fb`). Deleted `components/CodeSnippet.java`, `fragments/code-panel.html`, `m01simplepages/M01Snippets.java`, `m03pages/M03Snippets.java` (+ empty `components/` pkg). `M01Controller`/`M03Controller` no longer put `snippets` on the model (handlers with no other model use lost the `Model` param; `M03Controller.addMpaModel` keeps only `selectedMenu`/`p1Url`/`p2Url`). Every m01 `d01…d05` + m03 `d01`,`d02`,`d03`,`d04p1`,`d04p2` template: `code-panel` include → `<!-- docs:start page -->` / `<!-- docs:end page -->` around the demo body + `<hr>` + `<a href="http://localhost:4321/technologies/02_thymeleaf/m0X/">Docs</a>` (m03 MPA link sits in `fragments/m03d04-layout.html`). `readme.adoc` updated (docs live in the separate site; `docs:*` markers noted; `code-panel` dropped from the fragment list). **Verified:** `mvn clean compile` green; app boots; all 11 routes → 200; rendered pages carry the markers + Docs link and **no `codearea`**; params (`?greetee=`, `?greeting=`) and the d04 nav highlight still work. Docs-URL slug (`02_thymeleaf/m0X` + anchors) to be finalised in WP-T6. |
| WP-T3 | thymeleaf | **DONE 2026-09-06** | **m04 UI Patterns** — `m04uipatterns/M04Controller` (`D01_URL`/`D02_URL`, `menuUrls()`); templates `m04uipatterns/d01.html`/`d02.html` (both via `fragments/layout`). d01 parent/child: `fragments/m04-parent.html` (`parent(greeting)`) builds slot markup interpolating `greeting` and passes it down to `fragments/m04-child.html` (`child(slot1)`, `<th:block th:replace="${slot1}">`) via `~{::#slot1/content()}`. d02 forwarder: `fragments/m04-forwarder-first.html` (`first(greeting)`) — `th:with` flag; if the greeting says "forward" it `th:replace`s `fragments/m04-forwarder-second.html` (`second(greeting)`), else renders `First: …`. **Gotcha hit & fixed:** `th:replace` outranks `th:if` in attribute precedence, so `th:if`+`th:replace` on one element replaced unconditionally — wrapped the `th:replace` in a separate `<th:block th:if>`. `MainController` +`M04Controller.menuUrls()`; `m00main/index.html` +"UI Patterns" `<section>` (2 cards). `docs:start`/`docs:end` markers + `<hr>`+"Docs" back-link (`…/m04/`), no code panels. **Verified:** `mvn clean compile` green; app boots; `GET /`, `/m04/d01`, `/m04/d02` → 200; d01 shows Parent→Child slot text "…Greeting: hello", d02 shows `First: hello` for the plain call and `Second: hello with forward` for the forwarding call; menu cards link correctly. |
| WP-T4 | thymeleaf | **DONE 2026-09-06** | **m05 htmx Patterns** — `m05htmxpatterns/M05Controller`: `D01_URL` page + `D01_MESSAGE_URL` (`/m05/d01/message`) fragment handler (`@RequestParam("message")`, default text). `templates/m05htmxpatterns/d01.html` (via `fragments/layout`) — button `th:attr="hx-get=${messageUrl + '?message=hello'}"` + `hx-target="#my-message"`, an empty `<div id="my-message">`, and a `<pre>` echoing the URL. `templates/m05htmxpatterns/d01-message.html` — bare `<h3 th:text="|${message}!|">` (no doctype/html wrapper; `docs:start component` markers as `<!--/* */-->` so the swapped fragment stays clean). `MainController` +`M05Controller.menuUrls()`; `m00main/index.html` +"HTMX Patterns" `<section>` (1 card: "URL Components"). **Verified:** `mvn clean compile` green; app boots; `/m05/d01` → 200 with `hx-get="/m05/d01/message?message=hello"` on the button; `/m05/d01/message` → `<h3>Hello from the message fragment!</h3>`, `?message=hello` → `<h3>hello!</h3>`. **Full-course smoke:** all 15 routes (`/`, m01×5, m03×5, m04×2, m05 + its fragment) → 200. |
| WP-T5 | umbrella | **DONE 2026-09-06** | **Umbrella docs catch-up.** `docs/Variants.md` — Thymeleaf entry rewritten (built out; htmx 4 + vendored; `th:fragment`/`th:replace`/`~{…}`; `m01/m03/m04/m05` course, `m02` gap kept; write-ups in the docs site). `docs/Variant-Comparison.md` — overview-matrix row → `fragments, per-module demos` / `4.0.0`; "only scaffolded" note replaced; Axis-2 bullet updated. `docs/History.md` — Phase 1 Thymeleaf bullet: built out 2026-09-06. `docs/Learnings.md` — #14 reframed ("deferred variant, finished on demand"), #10 now "every variant is on htmx 4", confirmed-by-user bullet updated. `docs/Analysis-Baseline.md` — Thymeleaf row → `b95869e` / 2026-09-06; top analysis-date note added. `wip.md` — Future-work "Implement the Thymeleaf variant" struck through as DONE, htmx-4 + bulma checklist lines ticked, sibling-list note updated. |
| WP-T6 | thymeleaf + docs project | **DONE 2026-09-06** (2 passes) | **Thymeleaf pages in the docs site** (the Thymeleaf slice of WP-T11). Two commits. <br> **Pass 1 — Part A (thymeleaf repo):** `docs:start`/`docs:end` markers on the fragments the pages show — `fragments/helloworld.html`, `helloworldparams.html`, `helloworldcontent.html`, `m04-parent.html`, `m04-child.html`, `m04-forwarder-first.html`, `m04-forwarder-second.html` (tag `component`); `layout.html`, `page-head.html`, `m03d04-layout.html` (tag `page`; markers as siblings of the `th:fragment` element, or `<!--/* */-->` inside it, so nothing leaks — re-verified all routes: still only the 2 intentional page-level markers). **Pass 2 (per user feedback):** also added `// docs:start`/`// docs:end` + `// docs: <demo>` + `// docs: class` markers to `M01/M03/M04/M05Controller.java` (mirrors `PlainJTEController.java`), so the pages can show the controller like the JTE pages do. <br> **Part B (docs-project repo):** `extract-thymeleaf-snippets.js` (srcRoot `../../2025/2025-08-23_ssfe-patterns-thymeleaf-htmx`), wired into `extract-all-snippets.js`; **pass 2** added controller extraction (`allowedTags: ['class', <demo>]` → `<demo>_java.mdx`, one per demo section — m03 `d04` covers `d04p1`+`d04p2`+`addMpaModel`, m05 `d01` covers page + message endpoint). `technologies/02_Thymeleaf/m01.mdx`,`m03.mdx`,`m04.mdx`,`m05.mdx` (modelled on the Hono `mNN` pages; `<D0NJava/>` before `<D0N/>` like the JTE pages), `s01.mdx` stub removed. **Page naming = `mNN`** (matches the module numbers + the demos' back-links). **iframe `min-height`** hand-tuned per demo from measured content heights (900px-wide render): m01 140/180/180/300/390, m03 140/140/340/620, m04 235/225, m05 380 — content no longer clipped. **Verified:** `npm run extract-snippets` clean; `npm run build` green — 4 pages at `/technologies/02_thymeleaf/m0X/`, each demo shows `M0XController.java` + the template + fragments, iframe heights applied. <br> ⚠️ thymeleaf-repo Part A never landed last round (HEAD still `b95869e WP-T4`); this turn's thymeleaf commit carries **both** the fragment markers and the controller markers, and the docs-project extractor depends on it. |
| WP-T7 | qute | **DONE 2026-09-06** | **Deleted greeting/archetype leftovers from `2025-12-21_ssfe-patterns-quarkus-qute-htmx`.** 7 files, all pure Quarkus/Qute archetype demo content, none referenced by any real code: `org/acme/GreetingResource.java` (`/hello`) + `src/test/java/org/acme/GreetingResourceTest.java` + `GreetingResourceIT.java`; `ssfepatterns/HomeResource.java` (`/home`) + `templates/home.html`; `ssfepatterns/p01greeting/P01GreetingPageResource.java` (`/greetingpage`) + `templates/…/p01greeting/greetingpage.html`. Empty dirs removed (`org/acme`, `test/java/org`, both `p01greeting/`). `rest-assured` + `quarkus-junit5` left in `pom.xml` (now unused, but standard scaffolding — removing them is a separate call). **Verified:** `./mvnw -DskipTests clean package` green; app boots; `/`, `/m01/d01`, `/m01/d02`, `/m03/d01`, `/m04/d01`, `/m05/d01` → 200; `/home`, `/hello`, `/greetingpage` → 404. **Commit only the 7 deletions** — the repo also has pre-existing untracked `0create.sh` + `components/CodeSnippet.java` + `codeexplanation.html` (WP-T9 territory, leave them). |
| WP-T9 | qute | **DONE 2026-09-06** | **Dropped the in-app code-snippet docs from `2025-12-21_ssfe-patterns-quarkus-qute-htmx`** (same treatment as Thymeleaf WP-T2.5 / JTE-VC `9e94470`…`6dc16fb`). **Deleted:** 12 `M0XD0XCode.java` `@TemplateData` interfaces (`m01plain/M01D01Code`…`M05htmx/M05D01Code`); 12 `*_code.html` panel templates; the orphaned `components/CodeSnippet.java` + `components/codeexplanation.html` (both were untracked — never wired in). **Edited** the 12 demo templates (`m01d01`…`m05d01`): removed the `{#include …_code}{/include}` call, wrapped the demo body in `<!-- docs:start page -->` / `<!-- docs:end page -->`, added `<hr>` + `<a href="http://localhost:4321/technologies/07_qute/m0X/">Docs</a>`. Also cleaned m03d03's dead `{!TODO:!}` / `{! ${new CustomPageWithParamCode…} !}` lines; converted m01d02's `{! Include Component: !}` → `<!-- -->`; m03d02 kept its CRLF line endings. **Back-link slug `07_qute` is provisional** — reconcile in WP-T10/WP-T11 (taxonomy). No Java controller/routing code referenced `*Code`. **Verified:** `./mvnw -DskipTests clean package` green (Qute build-time template validation passes); app boots; all 14 routes (`/`, m01×5, m03×5, m04×2, m05) → 200 with **zero** `_code`/`M0XD0XCode`/`codeexplanation`/`codearea` in any rendered page. This is the in-app half; the docs-site half (Qute `.mdx` pages + `extract-qute-snippets.js`) is WP-T10. |
| WP-T10 | qute + docs project | **DONE 2026-09-06** (rename deferred) | **Qute → docs site** (pairs with WP-T9). Two commits. <br> **Part A — qute repo:** `// docs:start`/`// docs:end` markers on the demo controllers (`m01plain/M01D01`…`M01D05` tag `page`; `m03pages/M03Routing` tags `d01`…`d04`; `m04uipatterns/M04Routing` `d01`/`d02`; `m05htmx/M05Routing` `d01`), `<!-- docs:* -->` markers on the fragments (`components/helloworld`, `helloworldparams`, `helloworldcontent`, `m04uipatterns/m04d01parent`/`m04d01child`/`m04d02first`/`m04d02second`, `m05htmx/m05d01message` = tag `component`; `components/bulmapage`, `components/page_head` = tag `page`), markers on `m03d04p1.html`/`m03d04p2.html`, and deleted the dead empty stub `m03pages/page04mpapage2.html`. `./mvnw -DskipTests clean package` green; all 15 routes → 200. <br> **Part B — docs-project repo:** `extract-snippets/extract-qute-snippets.js` (35 snippets → `generated/snippets/qute/`), wired into `extract-all-snippets.js`; `src/content/docs/technologies/07_Qute/m01.mdx`,`m03.mdx`,`m04.mdx`,`m05.mdx` (`<D0NJava/>` + `<D0N/>` + fragments, iframe heights measured from the running app: m01 140/180/180/300/390, m03 140/140/340/650, m04 235/225, m05 380); `astro.config.mjs` — added the `Qute` sidebar entry (`technologies/07_Qute`) and **generalised the site `title`** to "Server Side Frontend Patterns" (was "…with plain JTE and ViewComponents"). `npm run build` green — 4 pages at `/technologies/07_qute/m0X/`. **Slug `07_qute` matches the WP-T9 back-links** — provisional, may move if WP-T11 renumbers. <br> ⏸ **Rename NOT done** — folder + GitHub-repo rename is an outward-facing, user-only action. See the checklist under "Rename the docs project" below. |
| WP-T11 | docs project | **DONE 2026-09-06** | **Docs-site taxonomy tidy-up** — one commit, docs-project repo only. `git mv technologies/01_JTE/ → 01_JTE-VC/`, `git mv s0N.mdx → m0N.mdx` (×6); rewrote the `@snippets/s0…` import paths + `S0…`→`M0…` binding names inside the 6 pages (the `[Demo]` links keep the real `sNN` app routes); `extract-jte-vc-snippets.js` — `outFile` paths `${outRoot}/s0N…` → `${outRoot}/m0N…` (the `allowedTags: ['class','s01d01']` stay — those are the marker names in `PlainJTEController.java`, not user-visible); `astro.config.mjs` sidebar `label: 'JTE'` / `directory: '…/01_JTE'` → `'JTE-VC'` / `'…/01_JTE-VC'`. Clean `rm -rf generated/snippets && npm run extract-snippets && npm run build` → green, 6 pages at `/technologies/01_jte-vc/m0N/`, snippets render, sidebar shows "JTE-VC", heading anchors unchanged. <br> **The jte-vc variant's in-app "Docs" back-links were left untouched** (still `http://localhost:4321/demos/s0N/#…`): a `s→m` repoint was made and then reverted per the user — since `s` is the target scheme (see the "Standardise on `sNN`" Future-work item), repointing those to `m` now would be churn to undo later. They stay stale until that item repoints everything to `s` at once. <br> **Not in scope** (separate optional Future-work items): `2025-08-23_ssfe-patterns-jte-htmx` build-out; the `mNN`→`sNN` standardisation. |
| WP-T12 | each pattern project | **DONE 2026-09-07** | **Playwright e2e tests.** Added a self-contained `playwright/` folder to each of the 5 SSFE-pattern projects, modelled on `2026-09-03_hda-springboot-browser-hono/playwright/`: `package.json` (`@playwright/test ^1.59.1` + `@types/node`, `"test": "npx playwright test"`), `playwright.config.ts` (`testDir: './tests'`, chromium only, `reporter: 'html'`, `use.trace: 'on-first-retry'`, a `webServer` block — `reuseExistingServer: false`, `timeout: 120_000`), `.gitignore`, `tests/main.spec.ts`. **`main.spec.ts`** (4 variants share a shape; jte-htmx is bespoke): landing page has every module `section.section` heading; a route-sweep asserts every demo route → 200 + non-empty `<body>` (heading levels vary too much across variants to assert a specific tag); the s05 htmx demo clicks "Include Component" and asserts `#my-message > h3` == `hello!`. **webServer commands:** jte-vc / thymeleaf → `mvn -q package -DskipTests && java -jar target/demo-1.0-SNAPSHOT.jar` (thymeleaf jar `…thymeleaf-htmx-1.0-SNAPSHOT.jar`); qute → `./mvnw -q package -DskipTests && java -jar target/quarkus-app/quarkus-run.jar`; **jte-htmx → `mvn -q spring-boot:run -Dspring-boot.run.profiles=dev`** (no `jte-maven-plugin`, so the fat jar has no pre-compiled templates — must run from the exploded classpath in dev mode); hono → `npm ci && bun run src/index.ts` (:3000). **Verified:** all 5 suites green (`npx playwright test`) — jte-htmx 3, jte-vc 4, thymeleaf 3, qute 3, hono 3. Needs a one-time `npm install` + `npx playwright install chromium` per folder. One `playwright/` folder per project = one commit each (jte-vc repo also has unrelated `.idea/` churn — exclude it). |

### sNN standardisation (WP-S*)

The user chose (2026-09-06) the **full** `mNN` → `sNN` rename: the Thymeleaf,
Qute and Hono variant apps *and* the docs-site pages. `s` = *series* (a group of
demos), `d` = *demo*. `2025-08-23_ssfe-patterns-jte-vc-htmx` is left as-is (its
files / packages / routes are already `sNN`).

Mapping: `m00`→`s00`, `m01`→`s01`, `m02`→`s02` (Hono only), `m03`→`s03`,
`m04`→`s04`, `m05`→`s05`. `d0N` demo suffixes are unchanged.

Per variant this touches: package/dir names (`m01…` → `s01…`), class names
(`M0NController` / `M0ND0N` / `M0NRouting` / `M0NMenu*` → `S0N…`), `@Path` /
`URL` route strings (`/m01/d01` → `/s01/d01`), template folders + `{#include}` /
`th:replace` / import paths, menu-key strings, the in-app "Docs" back-links
(`…/technologies/<v>/m0N/` → `…/s0N/`), and `readme`. Each variant WP is paired
with its docs-project slice (the matching `extract-<v>-snippets.js` srcRoots +
outFiles, the `technologies/<Dir>/m0N.mdx` → `s0N.mdx` pages + their `@snippets`
imports + iframe `src` routes) so extraction stays working after each step.

| WP | Repos | Status | Deliverable |
|----|-------|--------|-------------|
| WP-S1 | thymeleaf + docs | **DONE 2026-09-06** | Renamed `2025-08-23_ssfe-patterns-thymeleaf-htmx` `mNN`→`sNN`. **Thymeleaf repo (1 commit):** `git mv` java packages `m00main`→`s00main` / `m01simplepages`→`s01simplepages` / `m03pages`→`s03pages` / `m04uipatterns`→`s04uipatterns` / `m05htmxpatterns`→`s05htmxpatterns`, classes `M0NController`→`S0NController` (`MainController` unchanged), fragments `m03d04-layout.html`→`s03d04-layout.html` + `m04-*`→`s04-*`, template dirs. Content: `/m0N/d0N`→`/s0N/d0N` routes, `menuUrls` keys `m0Nd0N`→`s0Nd0N`, `th:replace ~{fragments/s04-…}`, view-name strings, `S0NController` refs/imports, `maincard.html` comment, javadoc `m0N —`→`s0N —`, `readme.adoc` (module table + `s0X…/S0XController`), the "s02 = JSX" comment, Docs back-links `…/02_thymeleaf/s0N/`. `mvn clean compile` green; app boots; all 15 `/s0N/…` routes → 200, old `/m01/d01` → 404, menu hrefs + back-link (`…/02_thymeleaf/s04/`) correct. **Docs repo (1 commit):** `extract-thymeleaf-snippets.js` — `s01simplepages`…/`S0NController`/`s03d04-layout`/`s04-*`; `git mv technologies/02_Thymeleaf/m0N.mdx`→`s0N.mdx` (×4) + `@snippets/thymeleaf/pages/s0N…/` imports + iframe `src` `localhost:8080/s0N/d0N`. `rm -rf generated/snippets && npm run extract-snippets` clean; `npm run build` green — pages at `/technologies/02_thymeleaf/s0N/`. |
| WP-S2 | qute + docs | **DONE 2026-09-06** | Renamed `2025-12-21_ssfe-patterns-quarkus-qute-htmx` `mNN`→`sNN`. **Qute repo (1 commit):** `git mv` packages `m00main`→`s00main` / `m01plain`→`s01plain` / `m03pages`→`s03pages` / `m04uipatterns`→`s04uipatterns` / `m05htmx`→`s05htmx`; classes `M01D01`…`M01D05`→`S01D01`…, `M0NMenus`→`S0NMenus`, `M0NRouting`→`S0NRouting` (nested `M0ND0NRouting`/`M05D01MessageRouting`→`S…` via content replace); `MainResource`/`MainCardInfo` kept. Template dirs + files `m0N.html`/`m0Nd0N*.html`→`s…`. Content: `M0ND0`→`S0ND0` (classes + `M0ND0N_CARD_INFO`), `@CheckedTemplate` `Templates.m0Nd0N()`→`s0Nd0N()` + basePath, `{#include …/s0Nplain/s0N.html}`, `{S0ND0NRouting:URL}`, routes `/m0N/d0N`→`/s0N/d0N`, Docs back-links `…/07_qute/s0N/`. `./mvnw -DskipTests clean package` green; app boots; all 15 `/s0N/…` routes → 200, old `/m01/d01`→404, menu hrefs + `/s04/d01` back-link (`…/07_qute/s04/`) + `hx-get="/s05/d01/message…"` correct. **Docs repo (1 commit):** `extract-qute-snippets.js` (`s01plain`/`S01D0N`/`S0NRouting`/`s03d04mpalayout`/`s04d0N*` + `pages/s0N/` outFiles); `git mv technologies/07_Qute/m0N.mdx`→`s0N.mdx` (×4) + `@snippets/qute/pages/s0N/` + `components/s03d04mpalayout`/`s04d0N*` imports + iframe `src` `localhost:8080/s0N/d0N`. `rm -rf generated/snippets && npm run extract-snippets` clean; `npm run build` green — pages at `/technologies/07_qute/s0N/`. |
| WP-S3 | hono + docs | **DONE 2026-09-06** | Renamed `2025-12-27_ssfe-patterns-hono-htmx` `mNN`→`sNN`. **Hono repo (1 commit):** `git mv` `src/m00hello`→`s00hello` / `m01html`→`s01html` / `m02jsx`→`s02jsx` / `m03pages`→`s03pages` / `m04uipatterns`→`s04uipatterns` / `m05htmx`→`s05htmx` + every `m0N.tsx` / `m0Nd0N.ts(x)` / `m03d04mpa*.tsx` file. Content (global `\bm0[0-5]`→`s0$1`, `\bM0[0-5]`→`S0$1` across `.ts`/`.tsx`): `mainpage.tsx` imports + `<S0NMenu>` + `s0N.init()`, per-module `s0N.tsx` imports/exports (`S0NMenu`, `s0N`, `s0Nd0N_init`), `S01D01`/`S01D02` `URL` consts + all `s0Nd0N` module objects, `S03d04MpaLayout`, routes `/m0N/d0N`→`/s0N/d0N`, Docs back-links `…/03_hono/s0N/`. `bun run dev` — all 18 `/s0N/…` routes (incl. `s02` jsx) → 200, old `/m01/d01`→404, menu hrefs + `/s01/d01` back-link (`…/03_hono/s01/`) correct, no runtime errors. **Docs repo (1 commit):** `extract-hono-snippets.js` (`src/s01html`… + `s0Npage`/`s0N` vars + `pages/s0N/…` + `s0Nd0N*` args); `git mv technologies/03_Hono/m0N.mdx`→`s0N.mdx` (×5, incl. `m02`→`s02`) + `m90_tnt.mdx`→`s90_tnt.mdx` + `@snippets/hono/pages/s0N/s0N…` imports + `S0N…TSX` bindings + iframe `src` `localhost:3000/s0N/d0N`. `rm -rf generated/snippets && npm run extract-snippets` clean; `npm run build` green — pages at `/technologies/03_hono/s0N/` + `/s90_tnt/`. |
| WP-S4 | docs + jte-vc variant | **DONE 2026-09-06** | JTE-VC's *variant* was already `sNN` — only its docs pages + the stale back-links. **Docs repo (1 commit):** `git mv technologies/01_JTE-VC/m0N.mdx`→`s0N.mdx` (×6), `@snippets/m0N…`→`@snippets/s0N…` imports + `M0N…`→`S0N…` binding names (`[Demo]` links keep the real `/s01d01` app routes), `extract-jte-vc-snippets.js` outFiles `${outRoot}/m0N…`→`${outRoot}/s0N…` (the `allowedTags: ['class','s01d01']` marker names + `title="s01d01.jte"` stay). **jte-vc variant repo (1 commit):** 17 in-app back-links `http://localhost:4321/demos/s0N/#…` → `…/technologies/01_jte-vc/s0N/#…` (the real path — `/demos/` never existed). `mvn clean compile` green; anchors verified against built pages (e.g. `S02D01.jte` → `…/s02/#1-basic-view-component-page`). Full docs rebuild green — **every page now `sNN`**: `01_jte-vc/s01…s06`, `02_thymeleaf/s01/s03/s04/s05`, `03_hono/s01…s05` + `s90_tnt`, `07_qute/s01/s03/s04/s05`. |

Order: S1 → S2 → S3 → S4 (independent, but do docs slice within each so `npm run extract-snippets` never breaks between commits). **All four DONE 2026-09-06.**

### Rename work packages (WP-T10b, WP-T10c)

Outward-facing folder / GitHub-repo renames. **The user performs each rename
manually, on their own schedule** (local `mv` + GitHub repo rename + `git remote
set-url`); **then, when the user says so, Claude sweeps the references.** Kept in a
separate list because they block nothing else and can happen at any time.

| WP | Repo | Status | Deliverable |
|----|------|--------|-------------|
| WP-T10b | user, then umbrella | **DONE 2026-09-09** | **Renamed the docs project** `2026-05-02_ssfe-patterns-jte-vc-htmx-docs` → `2026-05-02_hda-htmx-patterns-docs` (no longer JTE-VC-only). **User:** `mv` the local folder, renamed the GitHub repo (`https://github.com/svene/2026-05-02_hda-htmx-patterns-docs`), `git remote set-url`. **Claude — reference sweep:** old name → new across the umbrella `docs/*` (`Variants.md` repo table + section heading + 2 prose refs, `Analysis-Baseline.md` baseline row, `History.md` ×2, `Learnings.md` #16, `Variant-Comparison.md` ×2) and `wip.md` (~10 refs + this row); dropped the now-stale "to be renamed" / "(and renamed…)" asides. Also in the **thymeleaf variant repo** — `readme.adoc` + 4 `S0NController` javadocs (**user commits there**) — and the docs project's own `package.json` + `package-lock.json` `name` field (**user commits there**). No in-app "Docs" back-link encoded the old name (all use `http://localhost:4321/…`); the `@app` vite alias + `extract-*-snippets.js` srcRoots point at the variant repos, unaffected by a same-depth folder rename. |
| WP-T10c | user, then umbrella | **DONE 2026-09-09** | **Renamed the two GraalVM *demo* repos** (`jsx` → `hono` — they use hono `html``` tagged templates, not JSX): `2026-03-09_hda-springboot-graalvm-jsx-demo` → `…-graalvm-hono-demo`, `2026-03-15_hda-quarkus-graalvm-jsx-demo` → `…-graalvm-hono-demo`. `2026-03-07_springboot-graalvm-jsx-poc` **keeps its name** — still `.tsx` + TS→Java, a deliberate historical PoC. **User:** `mv` the local folders, renamed the GitHub repos + `git remote set-url`. **Claude — reference sweep:** old → new across the umbrella `docs/*` (`Variants.md` repo table + 2 section headings, `Analysis-Baseline.md` ×2 rows, `History.md` Phase 5/6 prose, `Learnings.md` codegen-audit table ×2, `Variant-Comparison.md` capability table + "which variant" table) and `wip.md` (project list + Future-work pointer + this row). Also in sibling repos (**user commits there**): `2026-03-07…jsx-poc/readme.md` back-reference; `2026-09-03_hda-quarkus-browser-hono/VARIANT-COMPARISON.md`; and in the two renamed repos themselves — `pom.xml` (`artifactId` + Spring `<name>`/`<description>`, also fixing a stale `2026-03-07` date), the Quarkus repo's `VARIANT-COMPARISON.md` self/twin refs, the Spring repo's `playwright/playwright.config.ts` jar path. **Not touched:** `.idea/*` module names (IDE-regenerated); the separate `2026-06-07_se-homepage` project (published blog posts + project list — GitHub redirects the old repo URLs; user's call). |
| WP-T13 (WP22, 1 of 11) | user, then umbrella | **DONE 2026-09-12** | **First repo of WP22** (`docs/ai/wip.md` — the `ssfe`/`hda` → `hypermedia` naming decision, all 11 repos): renamed `2025-08-23_ssfe-patterns-jte-htmx` → `2025-08-23_hypermedia-patterns-jte-htmx`. **User:** renamed the GitHub repo. **Claude:** `git remote set-url`, `mv` the local folder; **project internals** — `readme.adoc` + 4 `.jte` files, `SSFE-Patterns` → `Hypermedia-Patterns` page titles and `SSFE-PATTERN:` → `HYPERMEDIA-PATTERN:` comment markers (checked first: the docs project's `extract-*-snippets.js` key off `docs:start`/`docs:end` markers, not these, and this plain-JTE variant isn't extracted from yet — no cross-repo tooling impact); **user commits there**. **Umbrella `docs/*` sweep:** `Variants.md` (repo table row + section heading), `History.md` (Phase 1 prose), `Analysis-Baseline.md` (baseline row), `wip.md` (WP22 mapping-table status + the low-priority build-out TODO), `.claude/skills/update-docs/SKILL.md` (path example) — this row. Historical mentions of the old name in `wip_done.md`'s own past log rows (WP-T4/WP-T11) left as-is. No cross-repo prose reference found elsewhere on disk. **10 repos remain** (see `wip.md` WP22 status column). |
| WP-T14 (WP22, 2 of 11) | user, then umbrella + docs project + thymeleaf variant | **DONE 2026-09-12** | **Second repo of WP22:** renamed `2025-08-23_ssfe-patterns-jte-vc-htmx` → `2025-08-23_hypermedia-patterns-jte-vc-htmx`. **User:** renamed the GitHub repo. **Claude:** `git remote set-url`, `mv` the local folder; **project internals** — one `SSFE-Patterns` → `Hypermedia-Patterns` subtitle in `MpaLayout.jte`; **user commits there**. **This one had live cross-repo path dependents, unlike WP-T13** — found and fixed before they broke: the **docs project** (`2026-05-02_hda-htmx-patterns-docs`)'s `astro.config.mjs` `@app` vite alias and `extract-snippets/extract-jte-vc-snippets.js` `srcRoot` both hardcode the sibling's folder path — updated both to the new folder name and re-ran `npm run extract-snippets` clean (all `s0N…_java.mdx`/`_jte.mdx` + component files regenerated) to confirm nothing broke; also fixed its `README.md` (2 prose path mentions). Also fixed a stale comment in the **thymeleaf variant repo**'s `pom.xml` ("htmx copied from …"). All three sibling-repo edits are **user commits there**. **Umbrella `docs/*` sweep:** `Variants.md` (repo table row + section heading + docs-tooling-section prose ref), `History.md` (Phase 1 prose), `Analysis-Baseline.md` (baseline row), `wip.md` (WP22 status) — this row. Left as historical: `Analysis-Baseline.md`'s WP-T10b subject note naming this project's *old* old-name (`…_ssfe-patterns-jte-vc-htmx-docs`, a different, already-completed rename). **9 repos remain.** |
| WP-T15 (WP22, 3 of 11) | user, then umbrella + docs project | **DONE 2026-09-12** | **Third repo of WP22:** renamed `2025-08-23_ssfe-patterns-thymeleaf-htmx` → `2025-08-23_hypermedia-patterns-thymeleaf-htmx`. **User:** renamed the GitHub repo. **Claude:** `git remote set-url`, `mv` the local folder. **Project internals — bigger than WP-T13/T14, this one had an actual Java package to rename:** `git mv src/main/java/org/svenehrke/demo/ssfepatterns` → `hypermediapatterns` (5 controller files: `S00`/`S01`/`S03`/`S04`/`S05`), updated the `package`/`import` statements (`MainController.java` imports the 4 sibling sub-packages); `mvn clean compile` green, classes land under the new package path. Also: `pom.xml` `artifactId`/`name`/`description`, `application.properties` `spring.application.name`, `playwright/playwright.config.ts` jar path, `readme.adoc` title (`Server Side Frontend Patterns` → `Hypermedia Patterns`) + prose, `s03d04-layout.html` subtitle. `.idea/compiler.xml` module name **not touched** (IDE-regenerated, per WP-T10c precedent). **User commits there.** **Docs-project dependent, same pattern as WP-T14:** `extract-snippets/extract-thymeleaf-snippets.js` hardcodes both the sibling's folder path *and* the old Java package path (`srcRoot` + `java`) — fixed both, re-ran `npm run extract-snippets` clean, `generated/snippets/thymeleaf/` regenerated with no errors. **User commits there.** **Not touched:** the Quarkus/Qute sibling's own `dev.svenehrke.demo.ssfepatterns` package — same name, unrelated project, its own turn later in WP22. **Umbrella `docs/*` sweep:** `Variants.md` (repo table row + section heading), `History.md` (Phase 1 prose), `Analysis-Baseline.md` (baseline row), `wip.md` (WP22 status) — this row. **8 repos remain.** |

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
   **resolved (2026-09-06): keep `2026-05-02_hda-htmx-patterns-docs`
   separate.** It serves a different purpose from this umbrella project —
   per-variant, code-level docs with source extracted from the real variant
   (page-per-module, demo iframes), versus this project's high-level concepts and
   cross-variant comparison. Companions, not duplicates. `2026-05-01_springboot-hono-docs`
   was only a feasibility spike. See the Future-work entry for the full framing.
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
