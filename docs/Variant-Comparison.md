# Variant Comparison

The variants compared at the level of **concepts and architecture**, not
implementation detail. For what each project is, see the [catalog](Variants.md);
for how it got there, see [History.md](History.md).

Scope: the app / pattern-showcase variants. The two 2026-05 Astro/Starlight
projects are documentation generators, not variants, and are left out of the
tables.

---

## Overview matrix

| Variant (folder) | Backend + language | HTML generated where | View technology (concept) | Dynamic-update style | htmx |
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

The `…thymeleaf-htmx` row is only scaffolded — the patterns are planned to be
built out later (with Claude), mirroring the JTE variants.

---

## Axis 1 — Where the HTML is generated

Three models, in the order they were tried:

| Model | Variants | Upside | Downside |
|---|---|---|---|
| **In-JVM Java template engine** | all 2025-08 + Qute | one process, one language, one build; mature tooling | template-engine ergonomics (path strings, tag rules, verbosity) |
| **Separate Hono process** (Browser → Java → Hono over HTTP, view model as JSON) | `springboot-hono-poc`, `dynapage-demo` | write HTML in TypeScript; keep all existing Java (security, DB); Hono used exactly like a template engine | two processes to run/deploy; a network hop; a cross-language JSON contract to keep in sync |
| **GraalVM polyglot in the JVM** (JS renderer runs inside the JVM) | the three 2026-03 projects | TypeScript templates **without** a second process; one deployable | GraalVM runtime; a Java↔JS boundary to tune (context pool, JSON-string passing); JS bundle build step |

The pure-Hono variant (`2025-12-27_…hono-htmx`) is a fourth position: no JVM at
all — simplest of all, but it abandons the Java investment.

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

The direction of truth flipped over time: TypeScript-first → **Java-first**
(the current preference). The migration is **not uniform across projects** —
`springboot-hono-poc`, `hda-dynapage-demo`, `hda-springboot-graalvm-jsx-demo` and
`hda-quarkus-graalvm-jsx-demo` are Java-first; **`springboot-graalvm-jsx-poc`
still generates Java from TS** and has not been migrated (see the audit table in
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

- The **Quarkus** variants (`…qute-htmx`, `…quarkus-graalvm-jsx-demo`) carry
  native-image build files.
- The **GraalVM polyglot** demos run on a GraalVM **JDK** (so GraalJS JIT-compiles
  the hot JS) but are **not** native images.
- The two-process variants ship two runtimes (JVM + Bun/Node); Docker /
  docker-compose appears from `dynapage-demo` onward.

---

## When each model makes sense

| If you want… | Reach for |
|---|---|
| Simplest possible stack, no Java constraint | pure Hono (`2025-12-27_…hono-htmx`) |
| Stay entirely on the JVM, accept a Java template engine | JTE + View Components (Spring) or Qute (Quarkus) |
| TypeScript HTML but you have a large Java codebase, and a second process is acceptable | separate Hono process (`springboot-hono-poc` pattern) |
| TypeScript HTML, one Java codebase, **one** deployable | GraalVM polyglot (`2026-03-09` / `2026-03-15`) — current preference |
| The above on Quarkus with native-image on the table | `2026-03-15_hda-quarkus-graalvm-jsx-demo` |
