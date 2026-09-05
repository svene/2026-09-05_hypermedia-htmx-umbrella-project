# History — how the variants evolved

The chronological story behind the [catalog](Variants.md): which concepts were
adopted or dropped from one variant to the next, and *why*. High-level only —
per-project detail lives in each project.

The constant throughout: a **Hypermedia-Driven Application** rendering roughly the
same small "people / person" domain, so each step is a change of *how the HTML is
produced*, not *what* it shows.

---

## Phase 1 — Java template engines on Spring Boot (2025-08)

Starting point: Spring Boot + htmx, HTML from a Java template engine.

- **Plain JTE** (`ssfe-patterns-jte-htmx`). Established the two ways to assemble a
  page: *Template-Injection* (the layout receives a content block) vs
  *Template-Inclusion* (the page pulls in header/nav/footer fragments). JTE's
  refusal to parse unclosed tags forced awkward workarounds (e.g. the `<body>`
  tag has to live in the page, not the fragment), which pushed Injection forward
  as the better default.
- **JTE + View Components** (`ssfe-patterns-jte-vc-htmx`). Moved from templates
  addressed by path string to **components as server objects** — each owns its
  URL constant and template, the controller returns the component, and an htmx
  event (`hx-trigger … from:body`) refreshes it in place. Less stringly-typed
  wiring; this became the most built-out of the trio.
- **Thymeleaf** (`ssfe-patterns-thymeleaf-htmx`). Begun as a side-by-side
  comparison, never finished — interest had already moved on.

**Recurring friction:** Java template-engine ergonomics — path strings, unclosed-tag
rules, verbosity.

## Phase 2 — A different JVM stack: Quarkus / Qute (2025-12)

`ssfe-patterns-quarkus-qute-htmx` re-ran the pattern exercise on Quarkus with the
Qute engine, restructured as a teaching course (`m00`–`m05` modules) with a live
code-snippet viewer, and native-image build files in place. Useful as a
stack comparison, but Qute is still a Java template engine, so the same class of
friction remained.

## Phase 3 — Discovering Hono (2025-12)

`ssfe-patterns-hono-htmx` rebuilt the *entire* module course in **Hono on Bun**,
no Java. It put Hono's two HTML styles side by side — the `html``` tagged
template (`.ts`) and `hono/jsx` (`.tsx`) — and generating HTML in TypeScript
turned out to be markedly more pleasant than any Java engine. The tagged template
started to win over JSX.

**New problem:** going all-Hono throws away the existing Spring Boot investment
(security, persistence, the rest).

## Phase 4 — Bridge: Spring Boot + Hono as two processes (2025-12 → 2026-01)

`springboot-hono-poc`: **Browser → Spring Boot → Hono over HTTP**. Spring keeps
everything it already does; the Java template engine is replaced by a **separate
Hono process** that receives the view model as JSON and returns HTML — a template
engine that just happens to run out-of-process.

- Contract tooling was explored and pruned: zod validation and JSON-Schema /
  OpenAPI → Java codegen were tried and **reverted**, settling on a simpler
  "generate Java records from the TypeScript DTOs". First encounter with the
  **cross-language type-sync problem**.
- Dev ergonomics: Hono reachable directly via GET while developing, Spring POST
  in production; Spring forwards static-resource requests to Hono.

`hda-dynapage-demo` forked from that PoC and used it to compare update
strategies on an editable table: **OOB swaps vs `hx-partial`** — `hx-partial`
judged more readable — plus the nested-form / `form=` attribute pattern for a
selection table.

**Cost of this phase:** two processes to run and deploy; type drift between the
two languages.

## Phase 5 — Collapse to one process with GraalVM (2026-03)

`springboot-graalvm-jsx-poc`, then `hda-springboot-graalvm-jsx-demo`: run the
JavaScript renderer **inside the JVM** via GraalVM Polyglot. No second server; the
templates stay TypeScript. esbuild bundles them to one `ssr.js`.

Things learned here:

- Pass Java **records**, not `Map`s, across the boundary.
- Dev loop: rebuild the JS context per request in dev only, so an esbuild
  re-bundle suffices — no app restart; dev vs prod split via
  `@ConfigurationProperties`.
- Generate Java view-model types from the TypeScript.
- Performance work in the full demo: a **pool of GraalVM Contexts** for
  concurrency, shared engine/source but per-context state, cached entry-function
  lookups, and passing **JSON strings** across the Java↔JS boundary.

## Phase 6 — Convergence and simplification (2026-03-15 onward)

`hda-quarkus-graalvm-jsx-demo` was built as the framework-agnostic twin of the
Spring Boot demo, then both repos were synced. The changes made along the way are
the current preferred style:

- **JSX → `html``` tagged templates**; `.tsx` → `.ts` — no JSX runtime, no
  virtual DOM, `String(result)` is the HTML.
- **Many entry functions → a single `render(route, json)`** that dispatches on the
  route.
- **Code-generation direction reversed:** TS→Java became **Java→TS**. Java now
  owns the view models *and* the action URLs / route names; TypeScript consumes
  the generated types and constants.
- **htmx 2 → htmx 4**.
- **WebSockets → SSE** for automatic browser reload ("much cleaner").

The Quarkus repo's `VARIANT-COMPARISON.md` pins what legitimately differs between
the twins (framework idioms — JAX-RS vs Spring MVC, `@Scheduled` styles, H2 vs
HSQLDB) versus what is deliberately kept aligned.

## Phase 7 — Documentation generation (2026-05)

`springboot-hono-docs` and `ssfe-patterns-jte-vc-htmx-docs`: Astro + Starlight
sites that generate documentation **from the real project source** (tagged-snippet
extraction), so docs stay in sync with code. Intended to grow into per-variant
code-docs; this umbrella project is the higher-level companion to them.

---

## Where this stands (September 2026)

Preferred stack: a Java framework (Spring Boot **or** Quarkus) + GraalVM Polyglot
+ Hono `html` tagged templates in `.ts`, with **Java as the source of truth** for
view models, route names and action URLs, htmx 4 on the browser, and SSE-based
live reload in dev.

## Throughlines

- **Template-engine ergonomics** drove the whole journey — from JTE's tag rules,
  through Qute, to "just write TypeScript".
- **Cross-language type sync** was the persistent tax of leaving the JVM: zod /
  OpenAPI codegen → TS→Java records → finally Java→TS generation with Java as the
  single source of truth.
- **The dev loop** (no-restart reload) was a first-class concern at every phase;
  the answer converged on esbuild re-bundle + SSE.
- **Same domain everywhere** keeps the variants honest and comparable.
- **Swap strategy** (full page vs OOB vs `hx-partial`) was explored explicitly in
  the dynapage demo and settled toward partials.
- **Process count**: two processes (Phase 4) was a real cost that GraalVM
  (Phase 5) removed without giving up TypeScript templates.
