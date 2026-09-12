# Instructions for AI

This file serves as the working document for Claude. It contains information and
instructions so that the prompt on the command line can refer to this file.
It is a living document and is maintained as work on this project progresses.
Claude also keeps its list of TODOs in this file.

For the project's own purpose, scope and document set, see
[`../../README.md`](../../README.md) and
[`../../README_details.md`](../../README_details.md) — those are the
user-facing docs. **Completed work packages, resolved open questions, and the
full Thymeleaf build-out log live in
[`wip_done.md`](wip_done.md)** (split off 2026-09-11; moved into `docs/ai/`
alongside this file on 2026-09-12).

## Approach

- `docs/Variants.md` is written first as the shared reference; `History.md`,
  `Variant-Comparison.md` and `Learnings.md` build on it.
- All documentation output lives in `docs/` as Markdown.
- This repo only reads the sibling projects; it never modifies them.
- Work is split into work packages. Each work package is one manual git commit by
  the user. Claude stops after finishing a work package and reports; the user
  inspects and commits.

## Conventions

### Catalog entry shape

Per project, a few lines only: project name + start date, role (app variant /
PoC / pattern showcase / docs generator), the stack in one line, the one
distinguishing concept, current status, and "details: see the project". No
internals. A project ↔ GitHub-repo table sits at the top of `docs/Variants.md`.

### Comparison dimensions

Kept high-level: backend framework + language, where HTML is generated (in the
JVM / separate process / GraalVM polyglot), template/view technology as a
concept, how dynamic updates are done (full page / OOB / partial), and the main
trade-off / when this variant makes sense.

## TODO

- [ ] **WP22 — Rename all `ssfe-*` and `hda-*` repos to `hypermedia-*`**
  (follow-up to WP21, `wip_done.md` — the terminology-only pass). **Naming
  decided 2026-09-12:** both prefixes collapse into `hypermedia-`, project by
  project, no fixed order. Mapping (old → new):

  | Old | New | Status |
  |---|---|---|
  | `2025-08-23_ssfe-patterns-jte-htmx` | `2025-08-23_hypermedia-patterns-jte-htmx` | ☑ **done 2026-09-12** — repo renamed, remote/folder/internals updated, umbrella docs swept; awaiting the project's own commit |
  | `2025-08-23_ssfe-patterns-jte-vc-htmx` | `2025-08-23_hypermedia-patterns-jte-vc-htmx` | ☑ **done 2026-09-12** — repo renamed, remote/folder/internals updated, docs-project paths fixed (would've broken extraction), umbrella docs swept; awaiting commits |
  | `2025-08-23_ssfe-patterns-thymeleaf-htmx` | `2025-08-23_hypermedia-patterns-thymeleaf-htmx` | ☑ **done 2026-09-12** — repo renamed, remote/folder/internals + `org.svenehrke.demo.ssfepatterns`→`hypermediapatterns` Java package updated (build verified), docs-project extractor path fixed, umbrella docs swept; awaiting commits |
  | `2025-12-21_ssfe-patterns-quarkus-qute-htmx` | `2025-12-21_hypermedia-patterns-quarkus-qute-htmx` | ☑ **done 2026-09-12** — repo renamed, remote/folder/internals + `dev.svenehrke.demo.ssfepatterns`→`hypermediapatterns` Java package AND its mirrored Qute-templates dir renamed (Quarkus `package -DskipTests` build verified, incl. `@CheckedTemplate` resolution), docs-project extractor path fixed, umbrella docs swept; awaiting commits |
  | `2025-12-27_ssfe-patterns-hono-htmx` | `2025-12-27_hypermedia-patterns-hono-htmx` | ☑ **done 2026-09-12** — repo renamed, remote/folder/internals (no Java package here — TS/Bun, just `package.json`/`package-lock.json` name + one JSX subtitle) updated, docs-project extractor path fixed, umbrella docs swept; awaiting commits |
  | `2026-01-24_hda-dynapage-demo` | `2026-01-24_hypermedia-dynapage-demo` | ☑ **done 2026-09-12** — repo renamed, remote/folder/internals (root + `springboot/` pom.xml artifactId; no docs-project dependency, Group B) updated, umbrella docs swept; awaiting commits |
  | `2026-03-09_hda-springboot-graalvm-hono-demo` | `2026-03-09_hypermedia-springboot-graalvm-hono-demo` | ☑ **done 2026-09-12** — repo renamed, remote/folder/internals (pom.xml artifactId/name/description, playwright jar path, `HDA` terminology in architecture.md/readme.md) updated (`mvn compile` verified), cross-repo refs in the quarkus twin + graalvm-jsx-poc fixed, umbrella docs swept; awaiting commits |
  | `2026-03-15_hda-quarkus-graalvm-hono-demo` | `2026-03-15_hypermedia-quarkus-graalvm-hono-demo` | ☑ **done 2026-09-12** — repo renamed, remote/folder/internals (pom.xml artifactId, VARIANT-COMPARISON.md self-ref, `HDA` terminology in architecture.md) updated (`mvn compile` verified), functional link in the browser-hono quarkus twin fixed, umbrella docs swept; awaiting commits |
  | `2026-05-02_hda-htmx-patterns-docs` | `2026-05-02_hypermedia-htmx-patterns-docs` | ☑ **done 2026-09-12** — repo renamed, remote/folder/internals (`package.json`/`package-lock.json` name) updated (`npm run build` verified, 25 pages), thymeleaf-htmx's back-references (readme + 4 javadocs) fixed, umbrella docs swept; awaiting commits |
  | `2026-09-03_hda-springboot-browser-hono` | `2026-09-03_hypermedia-springboot-browser-hono` | pending |
  | `2026-09-03_hda-quarkus-browser-hono` | `2026-09-03_hypermedia-quarkus-browser-hono` | pending |

  (`2026-03-07_springboot-graalvm-jsx-poc` and `2025-12-31-springboot-hono-poc`
  carry neither prefix — untouched. The throwaway `2026-05-01_springboot-hono-docs`
  spike is untracked and also untouched.)

  **Per repo, split of labor:** **user, manually, one repo at a time** — rename
  the repo on GitHub. **Then Claude does the rest for that repo:** `git remote
  set-url` to the new GitHub URL, `mv` the local folder to the new name, and
  sweep that project's own internals (README/docs mentioning its own old name,
  build-file `artifactId`/package/module names if any, docker-compose service
  names, etc. — scope depends on the repo). Claude edits and reports; the user
  reviews and commits inside that repo same as here. **Then, back in this
  umbrella repo:** sweep `docs/*` + `wip.md`/`wip_done.md` (project list,
  `Analysis-Baseline.md` row) + any cross-repo prose reference in sibling repos
  (WP-T10b/c found some — e.g. a readme or javadoc naming a sibling by its old
  name) + the docs-project's astro sidebar/`.mdx` pages for that variant, if
  they name the repo (its `extract-<v>-snippets.js` reads by relative path, not
  by name, so likely unaffected — verify per repo). **11 repos total**, so
  budget several sessions and expect repo-specific cross-references not listed
  here.
- [ ] **_(optional, low priority)_ Build out `2025-08-23_hypermedia-patterns-jte-htmx`** —
  it is a very simple demo project and does **not** cover all the patterns the
  other pattern-course projects (JTE-VC, Thymeleaf, Qute, Hono) share. Bringing
  it up to the full `m01/m03/m04/m05` course would make the family complete, but
  the user has flagged this as low priority. Update `docs/*` afterwards.

Everything else that was ever tracked here has shipped — see
[`wip_done.md`](wip_done.md) for the full work-package history (WP0…WP23,
WP-T*, WP-S*), the completed Future-work items, and the resolved open questions.
