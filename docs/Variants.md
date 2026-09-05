# Variants — Catalog

A lightweight index of the sibling projects. Each entry says **what the project
is** and **the one idea that sets it apart**. Implementation details live in the
individual project, not here.

Folder paths are relative to this umbrella project. The date prefix is the start
date and roughly marks the point on the learning curve.

Common ground across (almost) all variants: a **Hypermedia-Driven Application** —
HTML rendered on the server, the browser swaps in fragments with htmx, no SPA.
They mostly render the same small "people / person" domain so the variants stay
comparable.

---

## Java template-engine era (2025-08)

### `../../2025/2025-08-23_ssfe-patterns-jte-htmx`

- **Role:** pattern showcase.
- **Stack:** Spring Boot + plain [JTE](https://jte.gg/), htmx 2.
- **Distinguishing idea:** the two basic ways to assemble a page with a plain
  template engine — *Template-Injection* (parent takes a `Content` block) vs
  *Template-Inclusion* (child pulls in `pagestart` / `pagenavigation` / `pageend`
  fragments) — and why Injection scales better.
- **Status:** working, documents two patterns.

### `../../2025/2025-08-23_ssfe-patterns-jte-vc-htmx`

- **Role:** pattern showcase (the most built-out of the 2025-08 trio).
- **Stack:** Spring Boot + JTE + [spring-view-component](https://github.com/tschuehly/spring-view-component)
  (server-side View Components), htmx 2.
- **Distinguishing idea:** components as first-class server objects — a
  component owns its URL constant and its template, the controller returns the
  component instead of a template path, and htmx events (`hx-trigger … from:body`)
  refresh a component in place.
- **Status:** working; documentation was progressively extracted from the code
  (`s03`–`s05` commits).

### `../../2025/2025-08-23_ssfe-patterns-thymeleaf-htmx`

- **Role:** pattern showcase — the Thymeleaf counterpart to the JTE variants.
- **Stack:** Spring Boot + Thymeleaf, htmx 2.
- **Distinguishing idea:** re-express the same component/insertion patterns with
  Thymeleaf fragments and slots.
- **Status:** **only started** — controller wired up, patterns not yet filled in
  to the level of the JTE variants. Planned to be implemented later with Claude.

---

## Quarkus / Qute (2025-12)

### `../../2025/2025-12-21_ssfe-patterns-quarkus-qute-htmx`

- **Role:** pattern showcase, organised as a course (`m00`–`m05` modules:
  plain → JSX-ish → pages → UI patterns → htmx).
- **Stack:** Quarkus + [Qute](https://quarkus.io/guides/qute) templates, htmx;
  native-image build files present.
- **Distinguishing idea:** the same SSFE patterns on a Quarkus/Qute stack, with
  a module-per-concept teaching structure and a live code-snippet viewer built
  into the demo app.
- **Status:** working through module M05.

---

## Hono / TypeScript era (2025-12 →, current preference)

### `../../2025/2025-12-27_ssfe-patterns-hono-htmx`

- **Role:** pattern showcase — the Hono/TS re-do of the SSFE pattern course
  (same `m00`–`m05` module structure as the Qute variant).
- **Stack:** [Hono](https://hono.dev/) on Bun, htmx 4, no Java at all.
- **Distinguishing idea:** two ways to produce HTML in Hono side by side — the
  `html``` tagged template (`.ts`) vs `hono/jsx` (`.tsx`) — with the tagged
  template emerging as the preferred style.
- **Status:** working; the `tnt.md` notes were migrated into a docs project.

---

## Spring Boot ↔ Hono bridge (2025-12 → 2026-01)

### `../../2025/2025-12-31-springboot-hono-poc`

- **Role:** architecture PoC.
- **Stack:** Browser → Spring Boot (Java, security, DB) → Hono (Node/Bun,
  HTML only) over HTTP; htmx 4 + Alpine.
- **Distinguishing idea:** keep all existing Spring Boot code, but replace the
  Java template engine with a **separate Hono process** that receives the view
  model as JSON and returns HTML — Hono used exactly like a template engine, just
  out-of-process.
- **Status:** working PoC (login `user` / `x21`); has architecture diagrams.

### `../2026-01-24_hda-dynapage-demo`

- **Role:** demo app comparing update strategies.
- **Stack:** same two-process Spring Boot + Hono setup; docker-compose;
  htmx 4 + Alpine.
- **Distinguishing idea:** the same "dynamic page" (editable table with row edit
  and bulk delete) implemented as an **OOB-swap variant** vs an **`hx-partial`
  variant**, concluding the `hx-partial` version is more readable. Also captures
  the nested-form / `form=` attribute pattern for a selection table.
- **Status:** both variants working.

---

## GraalVM polyglot era (2026-03) — Hono templates *inside* the JVM

### `../2026-03-07_springboot-graalvm-jsx-poc`

- **Role:** PoC.
- **Stack:** Spring Boot + GraalVM Polyglot running `hono/jsx` (`.tsx`) inside
  the JVM; `javagen` step generates Java types from the TS view models.
- **Distinguishing idea:** collapse the two-process bridge back into **one
  process** — the JS renderer runs in the JVM via GraalVM, so there is no second
  server, while the templates stay TypeScript/JSX.
- **Status:** PoC — `hello` / `page` / `layout` components, no domain app.
  Predates the JSX→`html``` and the TS→Java→**Java→TS** codegen migrations, so it
  still uses `.tsx` and generates Java from TS. Superseded by `2026-03-09`; decide
  whether to migrate it or keep it as-is (see the audit in
  [Learnings.md](Learnings.md)).

### `../2026-03-09_hda-springboot-graalvm-jsx-demo`

- **Role:** full demo of the GraalVM-polyglot approach (Spring Boot).
- **Stack:** Spring Boot 4 (Java 21, `JdbcClient`, Flyway/HSQLDB) + GraalVM
  Polyglot 25 + **hono `html` tagged templates** bundled to one `ssr.js` by
  esbuild; htmx 4 + hyperscript; Playwright tests; Docker (GraalVM JDK runtime).
- **Distinguishing idea:** despite the folder name, **no JSX** — plain
  `(vm) => html``` functions, no virtual DOM, no `renderToString`. TS templates
  sit next to the Java web layer; `mvn` regenerates Java VM types and web-API
  constants from the TS.
- **Status:** working demo with architecture / java-ts-integration docs.

### `../2026-03-15_hda-quarkus-graalvm-jsx-demo`

- **Role:** the Quarkus twin of `2026-03-09` — same pattern, other framework.
- **Stack:** Quarkus (JAX-RS, `@ConfigMapping`, `@Scheduled`, H2) + GraalVM
  Polyglot + hono `html` templates; Playwright; native-image build files.
- **Distinguishing idea:** shows the GraalVM-SSR pattern is framework-agnostic;
  its `VARIANT-COMPARISON.md` records exactly what differs from the Spring Boot
  twin (framework idioms only) and what is deliberately kept aligned.
- **Status:** web layer converged with the Spring Boot twin.

---

## Documentation generators (2026-05)

These are not app variants; they explore generating documentation *from* the real
code. `wip.md` notes they may later be extended to produce code-docs for the
variants.

### `../2026-05-01_springboot-hono-docs`

- **Stack:** Astro + [Starlight](https://starlight.astro.build/).
- **Distinguishing idea:** a docs site for the Spring Boot + Hono line of work,
  with experiments in pulling examples/settings from source.
- **Status:** early — starter kit plus some examples.

### `../2026-05-02_ssfe-patterns-jte-vc-htmx-docs`

- **Stack:** Astro + Starlight, with an `extract-snippets` step and a `generated/`
  output folder.
- **Distinguishing idea:** docs for the JTE-VC pattern showcase built by
  **extracting tagged snippets from the actual project source** so the docs stay
  in sync with the code.
- **Status:** has generated content for the Hono/JSX modules (`m03`).
