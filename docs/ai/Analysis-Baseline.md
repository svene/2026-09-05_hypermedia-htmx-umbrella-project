# Analysis Baseline

AI-facing tracking file (see `docs/ai/` — kept separate from the user-facing
docs in `docs/`, moved here 2026-09-12). The commit each project was at **when
the `docs/*.md` files were last written**. When a project gains new commits
later, diff from the hash recorded here to see what the umbrella docs still
need to catch up on.

- Analysis date: **2026-09-12** (baseline re-synced to each project's current
  HEAD; the 2026-09-06 Thymeleaf build-out and the 2026-09-07 per-project
  `playwright/` additions (WP-T12) are reflected — neither changes doc-relevant
  content beyond what the umbrella docs already cover. The 2026-09-12 WP22
  rename commits for the 5 `ssfe-patterns-*` repos — WP-T13 through WP-T17 —
  are also reflected; those commits are pure renames plus internal path fixes,
  not doc-relevant content changes)
- All projects analysed on branch `main` unless noted.
- Project name = GitHub repo name under `github.com/svene/` (see
  [../Variants.md](../Variants.md) for links). The throwaway spike
  `2026-05-01_springboot-hono-docs` (local-only, superseded) is not tracked here.

| Project | Branch | Commit at analysis | Date | Subject |
|---|---|---|---|---|
| `2025-08-23_hypermedia-patterns-jte-htmx` | main | `839fa18` | 2026-09-12 | WP-T13 — renamed from `…_ssfe-patterns-jte-htmx` |
| `2025-08-23_hypermedia-patterns-jte-vc-htmx` | main | `edbc335` | 2026-09-12 | WP-T14 — renamed from `…_ssfe-patterns-jte-vc-htmx` |
| `2025-08-23_hypermedia-patterns-thymeleaf-htmx` | main | `9ffa73f` | 2026-09-12 | WP-T15 — renamed from `…_ssfe-patterns-thymeleaf-htmx` (incl. `ssfepatterns`→`hypermediapatterns` Java package) |
| `2025-12-21_hypermedia-patterns-quarkus-qute-htmx` | main | `470f172` | 2026-09-12 | WP-T16 — renamed from `…_ssfe-patterns-quarkus-qute-htmx` (incl. Java package + mirrored Qute templates dir) |
| `2025-12-27_hypermedia-patterns-hono-htmx` | main | `3393f62` | 2026-09-12 | WP-T17 — renamed from `…_ssfe-patterns-hono-htmx` |
| `2025-12-31-springboot-hono-poc` | main | `4e6f9aa` | 2026-09-05 | vendored bulma |
| `2026-01-24_hypermedia-dynapage-demo` | main | `db3c697` | 2026-09-12 | WP-T18 — renamed from `…_hda-dynapage-demo` (pom.xml artifactIds + user's manual `hono/package.json` fix) |
| `2026-03-07_springboot-graalvm-jsx-poc` | main | `3a0f19f` | 2026-09-09 | WP-T10c — back-reference updated to `…graalvm-hono-demo` (this repo keeps its name) |
| `2026-03-09_hypermedia-springboot-graalvm-hono-demo` | main | `9ce2966` | 2026-09-09 | WP-T10c — renamed from `…-graalvm-jsx-demo` |
| `2026-03-15_hypermedia-quarkus-graalvm-hono-demo` | main | `bb6b072` | 2026-09-09 | WP-T10c — renamed from `…-graalvm-jsx-demo` |
| `2026-05-02_hda-htmx-patterns-docs` | main | `d37ad37` | 2026-09-12 | WP22 (T14–T17) — extractor `srcRoot`/package paths fixed for the jte-vc, thymeleaf, qute and hono renames |
| `2026-09-03_hda-springboot-browser-hono` | main | `68371c1` | 2026-09-05 | vendored bulma |
| `2026-09-03_hda-quarkus-browser-hono` | main | `100cb74` | 2026-09-09 | WP-T10c — fork-parent reference updated |

## Refreshing the docs after upstream changes

This whole procedure is automated by the `update-docs` skill
(`.claude/skills/update-docs/SKILL.md`) — invoke it to sweep every project in
this table. The manual steps it follows, for one project (from that project's
working copy):

```sh
git log --oneline <recorded-hash>..HEAD
```

Anything listed is new since the analysis. Update `Variants.md` /
`History.md` / `Variant-Comparison.md` / `Learnings.md` as needed, then bump the
row above (hash, date, subject) and the analysis date.

To re-capture every hash at once, from a directory holding all the checkouts:

```sh
for d in */; do
  printf '%s\t' "${d%/}"
  git -C "$d" log -1 --format='%h%x09%cs%x09%s'
done
```
