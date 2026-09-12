# Variants — Catalog

A lightweight index of the sibling projects. Each entry says **what the project
is** and **the one idea that sets it apart**. Implementation details live in the
individual project, not here.

Each project is referred to by its name only (which is also its GitHub repository
name — see the table below). The date prefix in the name is the start date and
roughly marks the point on the learning curve.

## Two groups of projects

The siblings fall into two families, plus the documentation tooling:

- **Group A · Hypermedia pattern showcases** — the same hypermedia pattern
  course (a landing page + the `s01` / `s03` / `s04` / `s05` demo series),
  re-implemented once per **template technology**. They exist to compare *how you
  express the patterns*, not to build a real application.
- **Group B · "person" use-case apps** — the same small *people / person* domain
  application (an editable table with row-edit and bulk-delete), re-implemented
  once per **technology or architecture**. They exist to compare *where and how
  the HTML is produced and updated*.
- **Documentation tooling** — `2026-05-02_hda-htmx-patterns-docs` (and its
  throwaway predecessor `2026-05-01_springboot-hono-docs`) is not a variant; it
  documents the others.

The catalog below is grouped into those three parts and, within each, ordered by
**era** — the learning-curve narrative it shares with [History.md](History.md).
The **Group** column in the table repeats the membership for quick scanning.

## Projects & repositories

All repositories are under **`github.com/svene/`**; the project name *is* the repo
name.

| Project | Group | Repository | Started |
|---|---|---|---|
| `2025-08-23_hypermedia-patterns-jte-htmx` | A · Patterns | <https://github.com/svene/2025-08-23_hypermedia-patterns-jte-htmx> | 2025-08 |
| `2025-08-23_ssfe-patterns-jte-vc-htmx` | A · Patterns | <https://github.com/svene/2025-08-23_ssfe-patterns-jte-vc-htmx> | 2025-08 |
| `2025-08-23_ssfe-patterns-thymeleaf-htmx` | A · Patterns | <https://github.com/svene/2025-08-23_ssfe-patterns-thymeleaf-htmx> | 2025-08 |
| `2025-12-21_ssfe-patterns-quarkus-qute-htmx` | A · Patterns | <https://github.com/svene/2025-12-21_ssfe-patterns-quarkus-qute-htmx> | 2025-12 |
| `2025-12-27_ssfe-patterns-hono-htmx` | A · Patterns | <https://github.com/svene/2025-12-27_ssfe-patterns-hono-htmx> | 2025-12 |
| `2025-12-31-springboot-hono-poc` | B · Person app | <https://github.com/svene/2025-12-31-springboot-hono-poc> | 2025-12 |
| `2026-01-24_hda-dynapage-demo` | B · Person app | <https://github.com/svene/2026-01-24_hda-dynapage-demo> | 2026-01 |
| `2026-03-07_springboot-graalvm-jsx-poc` | B · Person app | <https://github.com/svene/2026-03-07_springboot-graalvm-jsx-poc> | 2026-03 |
| `2026-03-09_hda-springboot-graalvm-hono-demo` | B · Person app | <https://github.com/svene/2026-03-09_hda-springboot-graalvm-hono-demo> | 2026-03 |
| `2026-03-15_hda-quarkus-graalvm-hono-demo` | B · Person app | <https://github.com/svene/2026-03-15_hda-quarkus-graalvm-hono-demo> | 2026-03 |
| `2026-05-02_hda-htmx-patterns-docs` | Docs tooling | <https://github.com/svene/2026-05-02_hda-htmx-patterns-docs> | 2026-05 |
| `2026-09-03_hda-springboot-browser-hono` | B · Person app | <https://github.com/svene/2026-09-03_hda-springboot-browser-hono> | 2026-09 |
| `2026-09-03_hda-quarkus-browser-hono` | B · Person app | <https://github.com/svene/2026-09-03_hda-quarkus-browser-hono> | 2026-09 |

Common ground across (almost) all variants: a **Hypermedia-Driven Application** —
the browser swaps in HTML fragments with htmx, no SPA, no virtual DOM. HTML is
rendered on the server in every variant *except* the 2026-09 browser-rendering
pair, where the same templates run client-side. They mostly render the same small
"people / person" domain so the variants stay comparable.

---

## Group A — Hypermedia pattern showcases

One repo per **template technology**, all running the same pattern course
(landing + `s01`/`s03`/`s04`/`s05`). They compare *how the patterns are
expressed*, not a real app. Ordered by era below.

### Java template-engine era (2025-08)

#### `2025-08-23_hypermedia-patterns-jte-htmx`

- **Role:** pattern showcase.
- **Stack:** Spring Boot + plain [JTE](https://jte.gg/), **htmx 4** (vendored under
  `static/js/…`, upgraded from 2.0.4 on 2026-09-05, commit `e2cba81`).
- **Distinguishing idea:** the two basic ways to assemble a page with a plain
  template engine — *Template-Injection* (parent takes a `Content` block) vs
  *Template-Inclusion* (child pulls in `pagestart` / `pagenavigation` / `pageend`
  fragments) — and why Injection scales better.
- **Status:** working, documents two patterns.

#### `2025-08-23_ssfe-patterns-jte-vc-htmx`

- **Role:** pattern showcase (the most built-out of the 2025-08 trio).
- **Stack:** Spring Boot + JTE + [spring-view-component](https://github.com/tschuehly/spring-view-component)
  (server-side View Components), **htmx 4**. On 2026-09-05 htmx (`7384f38`) and
  then bulma (`5089f49`) were moved off webjars to vendored, versioned
  `static/js/htmx.org/4.0.0/` and `static/css/bulma/1.0.4/` — the reference for
  the [bulma-vendoring plan](../bulma-vendoring-plan.md).
- **Distinguishing idea:** components as first-class server objects — a
  component owns its URL constant and its template, the controller returns the
  component instead of a template path, and htmx events (`hx-trigger … from:body`)
  refresh a component in place.
- **Status:** working; documentation was progressively extracted from the code
  (`s03`–`s05` commits).

#### `2025-08-23_ssfe-patterns-thymeleaf-htmx`

- **Role:** pattern showcase — the Thymeleaf counterpart to the JTE / Qute
  variants.
- **Stack:** Spring Boot + Thymeleaf (core, **no** layout-dialect), **htmx 4**,
  vendored `static/js/htmx.org/4.0.0/` + `static/css/bulma/1.0.4/`.
- **Distinguishing idea:** the same component / insertion / slot patterns
  expressed with `th:fragment` / `th:replace` / `~{…}` fragment expressions.
- **Structure:** a landing page plus modules `m01` Simple Pages, `m03` Page
  Patterns, `m04` UI Patterns, `m05` htmx Patterns — the same course the Qute
  variant runs, with the JSX module and the "experiments" section deliberately
  omitted (the `m02` gap is kept so demos line up by number across variants).
- **Status:** built out 2026-09-06 (with Claude). Pattern write-ups live in
  `2026-05-02_hda-htmx-patterns-docs`, not in-app — the demo templates
  carry `docs:start`/`docs:end` markers and link back to it.

---

### Quarkus / Qute (2025-12)

#### `2025-12-21_ssfe-patterns-quarkus-qute-htmx`

- **Role:** pattern showcase, organised as a course (`m00`–`m05` modules:
  plain → JSX-ish → pages → UI patterns → htmx).
- **Stack:** Quarkus + [Qute](https://quarkus.io/guides/qute) templates, **htmx 4**
  (vendored under `META-INF/resources/js/…`, upgraded from 2.0.4 on 2026-09-05,
  commit `431e0d2`); native-image build files present.
- **Distinguishing idea:** the same hypermedia patterns on a Quarkus/Qute stack, with
  a module-per-concept teaching structure and a live code-snippet viewer built
  into the demo app.
- **Status:** working through module M05.

---

### Hono / TypeScript era (2025-12 →, current preference)

#### `2025-12-27_ssfe-patterns-hono-htmx`

- **Role:** pattern showcase — the Hono/TS re-do of the hypermedia pattern course
  (same `m00`–`m05` module structure as the Qute variant).
- **Stack:** [Hono](https://hono.dev/) on Bun, **htmx 4** (vendored under
  `static/js/…`, upgraded from 2.0.8 on 2026-09-05, commit `3daf3da`), no Java at
  all.
- **Distinguishing idea:** two ways to produce HTML in Hono side by side — the
  `html``` tagged template (`.ts`) vs `hono/jsx` (`.tsx`) — with the tagged
  template emerging as the preferred style.
- **Status:** working; the `tnt.md` notes were migrated into a docs project.

---

## Group B — "person" use-case apps

One repo per **technology / architecture**, all rendering the same *people /
person* domain app (an editable table with row-edit and bulk-delete). They
compare *where and how the HTML is produced and updated*. Ordered by era below.

### Spring Boot ↔ Hono bridge (2025-12 → 2026-01)

#### `2025-12-31-springboot-hono-poc`

- **Role:** architecture PoC.
- **Stack:** Browser → Spring Boot (Java, security, DB) → Hono (Node/Bun,
  HTML only) over HTTP; htmx 4 + Alpine.
- **Distinguishing idea:** keep all existing Spring Boot code, but replace the
  Java template engine with a **separate Hono process** that receives the view
  model as JSON and returns HTML — Hono used exactly like a template engine, just
  out-of-process.
- **Status:** working PoC (login `user` / `x21`); has architecture diagrams.

#### `2026-01-24_hda-dynapage-demo`

- **Role:** demo app comparing htmx update strategies for one screen.
- **Stack:** same two-process Spring Boot + Hono setup; docker-compose;
  htmx 4 + Alpine + hyperscript.
- **Distinguishing idea:** the same "dynamic page" (editable table with row edit
  and bulk delete) built **four ways**, as separate parts of the app:
  **OOB swap** (`p01`), **`hx-partial`** (`p04`), **event-driven, JSX** (`p02` —
  the action response carries no HTML, just a client-side event; an Alpine
  receiver reacts) and **event-driven, HTML** (`p03` — same idea but the response
  also returns markup). Of the two **swap mechanisms**, OOB and `hx-partial`, the
  user finds `hx-partial` the more readable and carried it into the GraalVM demos;
  the two event-driven takes are a separate line of exploration, not ranked
  against it. Also captures the nested-form / `form=` attribute pattern for a
  selection table.
- **Status:** all four parts working.

---

### GraalVM polyglot era (2026-03) — Hono templates *inside* the JVM

#### `2026-03-07_springboot-graalvm-jsx-poc`

- **Role:** PoC.
- **Stack:** Spring Boot + GraalVM Polyglot running `hono/jsx` (`.tsx`) inside
  the JVM; `javagen` step generates Java types from the TS view models.
- **Distinguishing idea:** collapse the two-process bridge back into **one
  process** — the JS renderer runs in the JVM via GraalVM, so there is no second
  server, while the templates stay TypeScript/JSX.
- **Status:** PoC — `hello` / `page` / `layout` components, no domain app.
  Predates the JSX→`html``` and the TS→Java→**Java→TS** codegen migrations, so it
  still uses `.tsx` and generates Java from TS. Superseded by `2026-03-09` and
  **kept as-is on purpose** — its `readme.md` carries a "historical PoC" note
  (see the audit in [Learnings.md](Learnings.md)).

#### `2026-03-09_hda-springboot-graalvm-hono-demo`

- **Role:** full demo of the GraalVM-polyglot approach (Spring Boot).
- **Stack:** Spring Boot 4 (Java 21, `JdbcClient`, Flyway/HSQLDB) + GraalVM
  Polyglot 25 + **hono `html` tagged templates** bundled to one `ssr.js` by
  esbuild; htmx 4 + hyperscript; Playwright tests; Docker (GraalVM JDK runtime).
- **Distinguishing idea:** despite the `jsx` in the name, **no JSX** — plain
  `(vm) => html``` functions, no virtual DOM, no `renderToString`. TS templates
  sit next to the Java web layer; `mvn` regenerates the **`.ts` types and
  constants from Java** (`typescript-generator`), Java being the source of truth.
- **Status:** working demo with architecture / java-ts-integration docs.

#### `2026-03-15_hda-quarkus-graalvm-hono-demo`

- **Role:** the Quarkus twin of `2026-03-09` — same pattern, other framework.
- **Stack:** Quarkus (JAX-RS, `@ConfigMapping`, `@Scheduled`, H2) + GraalVM
  Polyglot + hono `html` templates; Playwright; native-image build files.
- **Distinguishing idea:** shows the GraalVM-SSR pattern is framework-agnostic;
  its `VARIANT-COMPARISON.md` records exactly what differs from the Spring Boot
  twin (framework idioms only) and what is deliberately kept aligned.
- **Status:** web layer converged with the Spring Boot twin.

---

### Browser-side rendering (2026-09) — hono templates run in the browser

Forked from the March GraalVM demos, then the GraalVM rendering layer was
**deleted**. `/uiroute/*` is now a plain JSON API returning a `{ route, vm }`
envelope; a small **htmx 4 extension** (`hono`, esbuild-bundled to `hx-hono.js`)
intercepts each response and runs the matching hono `html` template
**client-side** to produce the fragment htmx swaps in. First paint is a static
`index.html` shell that bootstraps via `hx-trigger="load"`. Runs on plain
**JDK 21** — no GraalVM. Java stays the source of truth (`typescript-generator` +
a gmavenplus script regenerate the `.ts` types/consts on `mvn package`).

#### `2026-09-03_hda-springboot-browser-hono`

- **Role:** the browser-rendering variant of the Spring Boot / hono demo.
- **Stack:** Spring Boot 4 (plain JDK 21, Spring MVC, `JdbcClient`) + hono `html`
  templates in the browser; htmx 4 + hyperscript + the `hono` extension;
  Playwright; Docker (`eclipse-temurin:21-jre`); SSE dev-reload.
- **Distinguishing idea:** the view model goes over the wire as JSON, not HTML;
  templating moves to the client while htmx still drives the swaps. No SSR
  process of any kind.
- **Status:** working; migrated from the GraalVM demo in one step, docs updated.

#### `2026-09-03_hda-quarkus-browser-hono`

- **Role:** the Quarkus twin of the above.
- **Stack:** Quarkus 3.32 (plain JDK 21, `quarkus-rest` + `quarkus-rest-jsonb`,
  CDI, JDBC) + browser-side hono `html`; htmx 4; Playwright; native-image build
  files; supports minification of the bundle.
- **Distinguishing idea:** same browser-rendering pattern on Quarkus; built in
  numbered "slices"; keeps a `VARIANT-COMPARISON.md` against the Spring Boot twin.
- **Status:** working (slices 1–5 done).

---

## Documentation tooling (2026-05) — not a variant

A separate site that documents the variants. It is
**deliberately kept separate** from this umbrella project (decided 2026-09-06):
different purpose — per-variant, code-level docs with source extracted from the
real variant, versus this project's high-level concepts and cross-variant
comparison. It is to be extended to cover every pattern variant — see
`docs/ai/wip.md`.

### `2026-05-02_hda-htmx-patterns-docs`

- **Stack:** [Astro](https://astro.build/) + [Starlight](https://starlight.astro.build/),
  with an `extract-snippets/` step (Node) whose output lands in the git-ignored
  `generated/` folder.
- **Distinguishing idea:** the prose is hand-written, but every code sample is
  **extracted from the real variant source** by tag markers, so the docs cannot
  drift from the code. `npm run extract-snippets` rebuilds the samples; `npm run
  dev` serves the site.
- **Status:** covers the JTE-VC (`2025-08-23_ssfe-patterns-jte-vc-htmx`) and Hono
  (`2025-12-27_ssfe-patterns-hono-htmx`) variants; the sidebar is scaffolded for
  Thymeleaf, JSX-Spring-Hono and the two Graal-JSX demos as future additions.

> An earlier throwaway project, `2026-05-01_springboot-hono-docs` (local only),
> was just a spike to confirm Astro / Starlight is a workable documentation tool
> for these variants. It served that purpose and is superseded by the project
> above.
