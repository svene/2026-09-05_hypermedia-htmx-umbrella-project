# Umbrella project — details

Background that doesn't fit in the top-level [`README.md`](README.md).

## Repository layout

Each sibling project is its own GitHub repository under
[`github.com/svene`](https://github.com/svene); the project name is the repo
name. Locally, the checkouts are organised into `2025/` and `2026/`
sub-folders by start year — but on GitHub they are flat, so all the
documentation in `docs/` refers to projects by name only, never by a local
path.

## Project categories

The sibling projects fall into two families, plus documentation tooling — see
[`docs/Variants.md`](docs/Variants.md) for the full catalog and the project ↔
repository table:

- **SSFE pattern showcases** — the same server-side-frontend pattern course,
  one implementation per template technology (JTE, JTE + View Components,
  Thymeleaf, Qute, Hono).
- **"Person" use-case apps** — the same small people/person domain
  application, one implementation per technology or architecture (two-process
  Spring Boot + Hono, GraalVM polyglot, browser-side rendering).
- **Documentation tooling** — a separate Astro/Starlight site that extracts
  code snippets from the real variant source; not a variant itself.

## Keeping the docs current

`docs/Analysis-Baseline.md` records the commit each sibling project was
analysed at. To refresh a document after upstream changes: diff
`<recorded-hash>..HEAD` in that project, revise the affected files under
`docs/`, then bump that project's row and the analysis date in
`Analysis-Baseline.md`.

`docs/Learnings.md` is seeded from the observable history and meant to be
extended over time with reasoning that isn't visible in commit messages.
