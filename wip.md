# Instructions for AI

This file serves as the working document for Claude. It contains information and
instructions so that the prompt on the command line can refer to this file.
It is a living document and is maintained as work on this project progresses.
Claude also keeps its list of TODOs in this file.

For the project's own purpose, scope and document set, see
[`README.md`](README.md) and [`README_details.md`](README_details.md) — those
are the user-facing docs. **Completed work packages, resolved open questions,
and the full Thymeleaf build-out log live in
[`wip_done.md`](wip_done.md)** (split off 2026-09-11).

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

- [ ] **_(optional, low priority)_ Build out `2025-08-23_ssfe-patterns-jte-htmx`** —
  it is a very simple demo project and does **not** cover all the patterns the
  other pattern-course projects (JTE-VC, Thymeleaf, Qute, Hono) share. Bringing
  it up to the full `m01/m03/m04/m05` course would make the family complete, but
  the user has flagged this as low priority. Update `docs/*` afterwards.

Everything else that was ever tracked here has shipped — see
[`wip_done.md`](wip_done.md) for the full work-package history (WP0…WP20,
WP-T*, WP-S*), the completed Future-work items, and the resolved open questions.
