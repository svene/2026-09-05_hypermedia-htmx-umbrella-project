# Learnings

Learnings inferred from **how the projects changed over time** — reversals,
migrations, and things that were built and then simplified. See
[History.md](History.md) for the timeline and [Variant-Comparison.md](Variant-Comparison.md)
for the axes.

> **Status: seed.** These are Claude's reading of the observable history
> (project-name dates, git logs, architecture notes). They are starting points,
> not settled
> conclusions — extend, correct, and add the reasoning that isn't visible in the
> commits.

---

## View layer

1. **Java template engines share an ergonomic ceiling.** JTE's refusal to parse
   unclosed tags, path-string addressing, and general verbosity recurred across
   plain JTE, JTE-VC and Qute. Switching to TypeScript templates was the single
   biggest lever, not a marginal gain.
2. **Components as objects beat templates addressed by path.** JTE View
   Components — where a component owns its URL constant *and* its template, and
   the controller returns the component — removed a class of stringly-typed
   wiring. This idea carried forward (route enums, generated URL constants) even
   after JTE itself was dropped.
3. **For SSR-only hypermedia, `html``` tagged templates beat JSX.** The newest
   projects migrated `.tsx` → `.ts` and `hono/jsx` → `html\`\``. The `html\`\``
   variant is **simpler and closer to real HTML**, and needs **no JSX runtime and
   no extra dependencies**. JSX's real value is client-side reconciliation, which
   an HDA doesn't use. Plain `(vm) => html\`…\`` with `String(result)` is enough.

## Crossing the language boundary

4. **Don't over-engineer the cross-language contract.** zod validation and
   JSON-Schema / OpenAPI → Java codegen were built and then **reverted**. Plain
   "generate Java records from the TS DTOs" was sufficient. The elaborate contract
   tooling cost more than the drift it prevented.
5. **Pick one source of truth for shared types, generate the other side.** The
   direction flipped from TypeScript-first to **Java-first** — the user's settled
   preference: view models, route names and action URLs live in Java, and
   TypeScript consumes generated types and constants (Java→TS via the
   `typescript-generator` Maven plugin, which also replaces a hand-written
   generator). Java-first won because the whole point was to keep the existing
   Java code, and because the mature Maven plugin beats maintaining a custom one.
   **Not every project was migrated** — see the audit below.
6. **Three JVM+Hono architectures, all kept as valid options.** They appeared in
   this order, each trading one cost for another:
   - **Two processes** (Java → Hono over HTTP) — a network hop, two runtimes to
     deploy, a JSON contract to sync.
   - **GraalVM polyglot** — one process, but a GraalVM runtime and a Java↔JS
     boundary to manage.
   - **Browser-hono** (2026-09) — plain JDK 21 serving JSON, but template code
     ships to the client and first paint needs a JS round-trip.

   None supersedes the others; the right one depends on the use case (see the
   "which architecture for which use case" item in `../wip.md`).
7. **The Java↔JS boundary needs deliberate work — first for correctness, then
   speed.** A GraalVM `Context` is **not thread-safe**, so a **pool** of Contexts
   (with the engine/source shared but per-Context state isolated) is *required*
   for concurrent request handling, not an optimisation. On top of that:
   **cache** entry-function lookups, pass **JSON strings** across the boundary
   rather than marshalling object graphs, and pass Java **records**, not `Map`s.
8. **Collapse many entry points to one dispatcher.** One JS entry function per
   HTTP endpoint became a single `render(route, json)` with a switch. Fewer moving
   parts on both sides of the boundary.

## Dev experience

9. **The dev loop is solvable cheaply.** In dev only: rebuild the JS bundle with
   esbuild and rebuild the JS context per request — no app restart. And **SSE
   beat WebSockets** for triggering browser reloads ("much cleaner").
10. **htmx major version is worth keeping uniform across variants.** The 2 → 4
    upgrade happened late and across the board; mixed majors add cognitive load
    when comparing variants.

## Keeping a family of variants healthy

11. **Explicitly converge twins.** The Spring Boot and Quarkus GraalVM demos keep
    a per-repo `VARIANT-COMPARISON.md` stating what is *deliberately* different
    (framework idioms — JAX-RS vs Spring MVC, scheduler styles, H2 vs HSQLDB) and
    what must stay aligned. Without that, twins drift silently.
12. **One shared domain keeps comparisons meaningful.** Rendering the same
    "people / person" domain everywhere is a deliberate constraint; it's what
    makes the variants comparable at all.
13. **OOB swaps vs `hx-partial`: partial won on readability.** From the dynapage
    demo. Default to partials; reserve OOB for genuine multi-region updates.
14. **Unfinished experiments are still data.** The Thymeleaf variant was only
    started before interest moved on — that "moved on" is itself a signal about
    where the value was.

## Meta / documentation

15. **Docs-from-code is a separate concern, started later (2026-05).** Snippet
    extraction from real source keeps docs in sync; this umbrella project is the
    higher-level companion to those generators.

---

## Confirmed by the user

- **`html``` over JSX is a settled preference** — simpler, closer to real HTML,
  no JSX runtime or extra dependencies.
- **Java→TS code generation is the settled preference** (Java is the source of
  truth), reversing the earlier TS→Java direction.
- The **Thymeleaf variant stalled deliberately** and is planned to be implemented
  later (with Claude), not abandoned.
- **The GraalVM Context pool exists because a GraalVM `Context` is not
  thread-safe** — a correctness constraint, not a performance tweak.
- **Two-process, GraalVM, and browser-hono are all valid architectures**; which
  to use is use-case-dependent (none is retired or "the winner").

## Codegen-direction audit (2026-09-05)

Which projects have cross-language type generation, and in which direction:

| Project | Direction | Notes |
|---|---|---|
| `springboot-hono-poc` | **Java→TS** ✅ | migrated (`ab83834`); removed the TS→Java generator and its Maven plugin |
| `hda-dynapage-demo` | **Java→TS** ✅ | removed the old TS→Java ("Hono2Java") generator (`8b79818`); the `typescript-generator` Maven plugin is still active in `springboot/pom.xml`, generating `hono/src/generated/types/vm-types.d.ts` (VM interfaces + route/event unions) from Java |
| `springboot-graalvm-jsx-poc` | **TS→Java** — **kept on purpose** | still uses `javagen/generate-java-from-hono.ts` and `.tsx`; **decided (2026-09-05) to keep as a historical PoC**, superseded by `2026-03-09`; a note to that effect is in its `readme.md` |
| `hda-springboot-graalvm-jsx-demo` | **Java→TS** ✅ | migrated (`5ecb2e7`); `typescript-generator` + gmavenplus for consts/routes/events/action-URLs |
| `hda-quarkus-graalvm-jsx-demo` | **Java→TS** ✅ | migrated (`0fce481`) |
| `hda-springboot-browser-hono` | **Java→TS** ✅ | forked from the SB GraalVM demo; keeps `typescript-generator` + gmavenplus |
| `hda-quarkus-browser-hono` | **Java→TS** ✅ | forked from the Quarkus GraalVM demo; same setup |

Pure-Java and pure-Hono variants have no cross-language contract.

**Resolved (2026-09-05):** `springboot-graalvm-jsx-poc` is kept as a historical
PoC — no migration. Its `readme.md` now carries a "deliberately not updated" note.
Every other project is Java→TS.

## To confirm / expand (for the manual pass)

- Performance numbers, if any, behind the GraalVM boundary decisions.
- Anything learned that never made it into a commit message.
