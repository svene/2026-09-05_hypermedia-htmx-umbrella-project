# Learnings

Learnings inferred from **how the projects changed over time** — reversals,
migrations, and things that were built and then simplified. See
[History.md](History.md) for the timeline and [Variant-Comparison.md](Variant-Comparison.md)
for the axes.

> **Status: seed.** These are Claude's reading of the observable history (folder
> dates, git logs, architecture notes). They are starting points, not settled
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
   direction flipped from TypeScript-first to **Java-first**: view models, route
   names and action URLs now live in Java, and TypeScript consumes generated
   types and constants. Both directions worked; Java-first won because the whole
   point was to keep the existing Java code.
6. **Two processes is a real, recurring cost** — run, deploy, a network hop, and
   a contract to keep in sync. It was tolerated for a while, then removed by
   GraalVM polyglot without giving up TypeScript templates. The GraalVM runtime
   plus boundary-tuning was judged the smaller price.
7. **The Java↔JS boundary needs deliberate performance work.** What the demos
   converged on: a **pool** of GraalVM Contexts for concurrency; share the
   engine/source but isolate per-context state; **cache** entry-function lookups;
   pass **JSON strings** across the boundary rather than marshalling object
   graphs; pass Java **records**, not `Map`s.
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
- The **Thymeleaf variant stalled deliberately** and is planned to be implemented
  later (with Claude), not abandoned.

## To confirm / expand (for the manual pass)

- Whether "codegen direction reversed to Java→TS" is a settled preference or just
  the `2026-03-15` repo's local choice.
- Performance numbers, if any, behind the GraalVM boundary decisions.
- Whether the two-process architecture is fully retired or still has a use case.
- Anything learned that never made it into a commit message.
