# Variant Comparison

The variants compared at the level of **concepts and architecture**, not
implementation detail. For what each project is, see the [catalog](Variants.md);
for how it got there, see [History.md](History.md).

Scope: the app / pattern-showcase variants. The two 2026-05 Astro/Starlight
projects are documentation generators, not variants, and are left out of the
tables.

---

## Overview matrix

| Variant (project) | Backend + language | HTML generated where | View technology (concept) | Dynamic-update style | htmx |
|---|---|---|---|---|---|
| `2025-08-23_…jte-htmx` | Spring Boot, Java | in the JVM | plain JTE templates | full page + fragments | 2.x |
| `2025-08-23_…jte-vc-htmx` | Spring Boot, Java | in the JVM | JTE + server-side View Components | fragments + event-driven refresh | 2.x |
| `2025-08-23_…thymeleaf-htmx` | Spring Boot, Java | in the JVM | Thymeleaf fragments/slots | (planned) | 2.x |
| `2025-12-21_…quarkus-qute-htmx` | Quarkus, Java | in the JVM | Qute templates | fragments, per-module demos | 2.x |
| `2025-12-27_…hono-htmx` | Hono on Bun, TypeScript | in the (single) JS process | Hono `html``` **and** `hono/jsx` | fragments, per-module demos | 2.0.8 |
| `2025-12-31-springboot-hono-poc` | Spring Boot **+** Hono, Java + TS | separate Hono process (HTTP) | Hono `html``` / JSX | fragments | 2.0.8 → 4.0.0 |
| `2026-01-24_hda-dynapage-demo` | Spring Boot **+** Hono, Java + TS | separate Hono process (HTTP) | Hono components | **OOB vs `hx-partial`, compared** | 2.0.8 → 4.0.0 |
| `2026-03-07_…graalvm-jsx-poc` | Spring Boot + GraalVM, Java + TS | in the JVM via GraalVM polyglot | `hono/jsx` (`.tsx`) | fragments | 4.0.0 |
| `2026-03-09_hda-springboot-graalvm-jsx-demo` | Spring Boot + GraalVM, Java + TS | in the JVM via GraalVM polyglot | Hono `html``` (`.ts`) | `hx-partial` / fragments | 4.0.0 |
| `2026-03-15_hda-quarkus-graalvm-jsx-demo` | Quarkus + GraalVM, Java + TS | in the JVM via GraalVM polyglot | Hono `html``` (`.ts`) | `hx-partial` / fragments | 4.0.0 |
| `2026-09-03_hda-springboot-browser-hono` | Spring Boot 4, plain JDK 21, Java + TS | **in the browser** (htmx `hono` extension) | Hono `html``` (`.ts`) | `/uiroute/*` returns `{route, vm}` JSON; fragment built client-side | 4.0.0 |
| `2026-09-03_hda-quarkus-browser-hono` | Quarkus 3.32, plain JDK 21, Java + TS | **in the browser** (htmx `hono` extension) | Hono `html``` (`.ts`) | `/uiroute/*` returns `{route, vm}` JSON; fragment built client-side | 4.0.0 |

The `…thymeleaf-htmx` row is only scaffolded — the patterns are planned to be
built out later (with Claude), mirroring the JTE variants.

---

## Axis 1 — Where the HTML is generated

Four models, in the order they were tried:

| Model | Variants | Upside | Downside |
|---|---|---|---|
| **In-JVM Java template engine** | all 2025-08 + Qute | one process, one language, one build; mature tooling | template-engine ergonomics (path strings, tag rules, verbosity) |
| **Separate Hono process** (Browser → Java → Hono over HTTP, view model as JSON) | `springboot-hono-poc`, `dynapage-demo` | write HTML in TypeScript; keep all existing Java (security, DB); Hono used exactly like a template engine | two processes to run/deploy; a network hop; a cross-language JSON contract to keep in sync |
| **GraalVM polyglot in the JVM** (JS renderer runs inside the JVM) | the three 2026-03 projects | TypeScript templates **without** a second process; one deployable | GraalVM runtime; a Java↔JS boundary to manage — a **`Context` is not thread-safe**, so a Context pool is mandatory, plus JSON-string passing and entry-function caching; JS bundle build step |
| **In the browser** (htmx `hono` extension runs the templates client-side; `/uiroute/*` is a JSON API) | the two 2026-09 `…browser-hono` projects | plain JDK 21 — no GraalVM, no SSR process at all; server just serves JSON + a static shell; smallest server-side footprint | template code ships to and runs in the browser; first paint needs a JS round-trip; arguably crosses the line from "HTML over the wire" to "view model over the wire" |

The pure-Hono variant (`2025-12-27_…hono-htmx`) is a fifth position: no JVM at
all — simplest of all, but it abandons the Java investment.

The trajectory: HTML built **on the server in the JVM** → **in a second process**
→ **back in the JVM via GraalVM** → **in the browser**. Each step moved the
rendering further from the Java process; the last one removes server-side
rendering entirely.

## Axis 2 — View technology as a concept

- **Java engines.** *Plain JTE* teaches page assembly (Injection vs Inclusion).
  *JTE + View Components* raises the unit of composition from "template file" to
  "server object that owns its URL and template". *Qute* is the same idea on
  Quarkus. *Thymeleaf* is the fragment/slot take (not built out).
- **TypeScript.** Two styles, evaluated head-to-head across several projects:
  - `hono/jsx` (`.tsx`) — familiar JSX, a JSX runtime, virtual-DOM-ish.
  - `html``` tagged template (`.ts`) — plain functions `(vm) => html\`…\``,
    `String(result)` is the HTML, no runtime, no vdom.
  The tagged template is the current preference: **simpler, closer to real HTML,
  and no JSX runtime or extra dependencies**. The newest projects migrated
  `.tsx` → `.ts` and JSX → `html\`\``.

## Axis 3 — The cross-language contract

| Variants | Contract | How the type sync is handled |
|---|---|---|
| pure Java (2025-08, Qute) | none | n/a |
| pure Hono (`hono-htmx`) | none | n/a |
| Java + separate Hono | view model as **JSON over HTTP** | tried zod + OpenAPI→Java codegen, reverted; then migrated to **Java→TS** (`springboot-hono-poc`) |
| Java + GraalVM | in-process **Java↔JS** call, JSON string payload | early: generate Java view-model types from TS. Later reversed: **Java→TS** — Java owns the view models, route names and action URLs; TS consumes generated types/constants |
| Java + browser Hono | view model as **`{route, vm}` JSON to the browser** | **Java→TS** — `typescript-generator` + a gmavenplus script regenerate the `.ts` types and constants from Java on `mvn package` |

The direction of truth flipped over time: TypeScript-first → **Java-first**
(the current preference). Every project is Java-first **except
`springboot-graalvm-jsx-poc`**, which still generates Java from TS and is
**deliberately kept that way as a historical PoC** (see the audit table in
[Learnings.md](Learnings.md)).

## Axis 4 — Dynamic updates

- **Full page + fragment swaps** — the baseline everywhere.
- **Event-driven refresh** — `hx-trigger="… from:body"` on a component so it
  reloads itself when something elsewhere changes (introduced with JTE View
  Components).
- **OOB swaps vs `hx-partial`** — compared directly in `dynapage-demo` on an
  editable table with row-edit and bulk-delete; `hx-partial` came out more
  readable and is the style carried into the GraalVM demos.
- Nested-form avoidance — the `form=` attribute pattern for a selection table
  (from `dynapage-demo`).

## Axis 5 — Native image / deployment

- The **Quarkus** variants (`…qute-htmx`, `…quarkus-graalvm-jsx-demo`,
  `…quarkus-browser-hono`) carry native-image build files.
- The **GraalVM polyglot** demos run on a GraalVM **JDK** (so GraalJS JIT-compiles
  the hot JS) but are **not** native images.
- The two-process variants ship two runtimes (JVM + Bun/Node); Docker /
  docker-compose appears from `dynapage-demo` onward.
- The **`…browser-hono`** variants drop back to a **plain JDK 21** runtime
  (`eclipse-temurin:21-jre` in the Spring Boot Dockerfile) — no GraalVM, no second
  process; the only build-time extra is the esbuild bundle of `hx-hono.js`.

---

## Architecture trade-offs — two-process vs GraalVM polyglot vs browser-hono

These three are the live options for "Java framework + Hono `html` templates".
**The part a maintainer touches most — writing the templates — is identical in all
three:** the same hono `html` tagged-template `.ts` files, the same view models
and route/event names generated from Java. What differs is the **glue** each one
needs and **where the rendering runs**. So the comparison below is really about
the glue and its consequences.

| Dimension | Two-process (`springboot-hono-poc`, `dynapage-demo`) | GraalVM polyglot (`2026-03-09`, `2026-03-15`) | Browser-hono (`2026-09-03` pair) |
|---|---|---|---|
| **Template authoring** | hono `html` `.ts`, Java-generated types | same | same |
| **Glue you own** | a Hono HTTP service (routing, error→status, dev GET / prod POST) + a Java HTTP client + static-asset passthrough | a GraalVM bridge: `Context` pool, engine/source lifecycle, entry-function cache, Java↔JS JSON marshalling | a small htmx extension (`hx-hono.js`, ~7–12 KB) + client-side `render(route, vm)` dispatch; Java controllers just return JSON |
| **Extra tech to know** | a Node/Bun runtime in prod; otherwise mainstream | GraalVM JDK + polyglot API — **niche**, few devs know it, boundary debugging is specialised | none beyond a plain JRE; but you own some browser framework code |
| **Processes / containers** | 2 (app + render) | 1 | 1 |
| **Server image / footprint** | two images & runtimes to build, patch, deploy in step | one image, but GraalVM JDK (larger) + memory per pooled `Context` | smallest — slim `temurin:21-jre`; ships ~7–12 KB JS to each client once |
| **Where render cost lands** | the render service | the app instance (bounded by pool size) | the end user's device (server does DB + JSON only) |
| **Per-render latency** | one pod-local HTTP round-trip + JSON both ways — low-ms, fine but *not* a function call | in-process call, JIT-fast after warmup; cold `Context` / pool contention are the risks | no server render; client template call is cheap (but see first paint) |
| **First paint / no-JS / SEO** | full HTML in the first response — initial content works without JS, SEO-friendly | same | static shell, then JS parse + a JSON round-trip before content — slower first paint, **needs JS**, SEO needs care |
| **Native-image friendliness** | Java side can be native (Quarkus); render side is separate anyway | polyglot + native-image not done here — effectively rules it out | Java side is a plain JSON API — the **most** native-image-friendly |
| **Failure mode of rendering** | a network dependency: timeouts, retries, version skew, another thing to monitor & release in lockstep | shares fate with the request thread; a template error just throws in-process; no partition risk | failures happen on the client — invisible to server logs unless reported; but a struggling server blocks data, not cached template code |
| **Debugging a template bug** | two log streams, correlate across HTTP; stack traces stop at the boundary | one process, but mixed Java/JS stack traces; GraalVM tooling needed | reproduce & inspect in browser devtools (pleasant) — but needs the client's state |
| **What the client can see** | only final HTML; view-model JSON and template logic stay server-side | same | the `{route, vm}` JSON **and** the compiled templates ship to the client — VM shape and presentation logic are visible; keep secrets out of VMs (now enforced, not just good practice) |
| **Independent scaling / evolution** | render tier scales, versions, and could be reused by other clients on its own — at the cost of contract management | template bundle builds & ships with the app — always in sync, no separate scaling | same as GraalVM |
| **Testing rendering** | test the Hono service in isolation (fast); full path needs both up | invoke the renderer inside a JVM test; Playwright for end-to-end | only truly exercised through a browser (Playwright) — more end-to-end weight |

### Net

- **Two-process** shines when you already run Node comfortably and want the render
  tier decoupled — scaled, versioned, or reused independently, with app and UI
  work separable. It hurts when you don't want a second deployable, a network hop,
  or contract/version management; it adds the most operational surface.
- **GraalVM polyglot** shines when you want server-rendered HTML, TypeScript
  templates, and **exactly one deployable**, with no second process. It hurts when
  the team doesn't want to learn GraalVM polyglot, when you need native image, or
  when the bridge machinery (Context pool, marshalling) is unwelcome weight. In
  practice its niche-ness is the main cost — it is not used in many projects, so
  familiarity, examples, and debugging tooling are all thinner.
- **Browser-hono** shines when you want the slimmest server (plain JRE, JSON
  only), the best native-image story, and render cost off the server — and you are
  fine shipping template code to clients. It hurts when first paint / no-JS / SEO
  matter, when the view-model and presentation logic should not be visible
  client-side, or when you'd rather not own browser framework code.

### Low lock-in

Because the `.ts` templates and the Java view models are identical across all
three, moving between them is mostly swapping the glue — the browser-hono repos
were made *from* the GraalVM demos by deleting the rendering layer. The choice is
reversible, so it can follow the use case rather than being a one-way door.

---

## When each model makes sense

The Java + Hono options — **two-process**, **GraalVM polyglot**, **browser-side** —
are all valid; none supersedes the others (see the trade-off section above). Quick
picker:

| If you want… | Reach for |
|---|---|
| Simplest possible stack, no Java constraint | pure Hono (`2025-12-27_…hono-htmx`) |
| Stay entirely on the JVM, accept a Java template engine | JTE + View Components (Spring) or Qute (Quarkus) |
| TypeScript HTML but you have a large Java codebase, and a second process is acceptable | separate Hono process (`springboot-hono-poc` pattern) |
| TypeScript HTML, one Java codebase, **one** deployable, all rendering server-side | GraalVM polyglot (`2026-03-09` / `2026-03-15`) |
| TypeScript HTML, one Java codebase, **plain JDK** (no GraalVM), server does only JSON — and shipping template code to the browser + a first-paint JS round-trip is acceptable | browser-side Hono (`2026-09-03_hda-*-browser-hono`) — the most recent direction |
| Any of the GraalVM / browser variants on Quarkus with native-image on the table | `2026-03-15_hda-quarkus-graalvm-jsx-demo` or `2026-09-03_hda-quarkus-browser-hono` |
