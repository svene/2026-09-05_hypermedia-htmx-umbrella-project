# Analysis Baseline

The commit each project was at **when the docs in this folder were written**. When
a project gains new commits later, diff from the hash recorded here to see what
the umbrella docs still need to catch up on.

- Analysis date: **2026-09-09** (baseline re-synced to each project's current
  HEAD; the 2026-09-06 Thymeleaf build-out and the 2026-09-07 per-project
  `playwright/` additions (WP-T12) are reflected — neither changes doc-relevant
  content beyond what the umbrella docs already cover)
- All projects analysed on branch `main` unless noted.
- Project name = GitHub repo name under `github.com/svene/` (see
  [Variants.md](Variants.md) for links). The throwaway spike
  `2026-05-01_springboot-hono-docs` (local-only, superseded) is not tracked here.

| Project | Branch | Commit at analysis | Date | Subject |
|---|---|---|---|---|
| `2025-08-23_ssfe-patterns-jte-htmx` | main | `9a9f2d9` | 2026-09-07 | playwright tests |
| `2025-08-23_ssfe-patterns-jte-vc-htmx` | main | `a2c3cd1` | 2026-09-07 | playwright tests |
| `2025-08-23_ssfe-patterns-thymeleaf-htmx` | main | `dc9822f` | 2026-09-09 | WP-T10b — docs-project rename swept through readme + javadocs |
| `2025-12-21_ssfe-patterns-quarkus-qute-htmx` | main | `e6bffc3` | 2026-09-07 | playwright tests |
| `2025-12-27_ssfe-patterns-hono-htmx` | main | `98a8543` | 2026-09-07 | playwright tests |
| `2025-12-31-springboot-hono-poc` | main | `4e6f9aa` | 2026-09-05 | vendored bulma |
| `2026-01-24_hda-dynapage-demo` | main | `0d3df4f` | 2026-09-05 | vendored bulma |
| `2026-03-07_springboot-graalvm-jsx-poc` | main | `3a0f19f` | 2026-09-09 | WP-T10c — back-reference updated to `…graalvm-hono-demo` (this repo keeps its name) |
| `2026-03-09_hda-springboot-graalvm-hono-demo` | main | `9ce2966` | 2026-09-09 | WP-T10c — renamed from `…-graalvm-jsx-demo` |
| `2026-03-15_hda-quarkus-graalvm-hono-demo` | main | `bb6b072` | 2026-09-09 | WP-T10c — renamed from `…-graalvm-jsx-demo` |
| `2026-05-02_hda-htmx-patterns-docs` | main | `5e10194` | 2026-09-09 | WP-T10b — renamed from `…_ssfe-patterns-jte-vc-htmx-docs` |
| `2026-09-03_hda-springboot-browser-hono` | main | `68371c1` | 2026-09-05 | vendored bulma |
| `2026-09-03_hda-quarkus-browser-hono` | main | `100cb74` | 2026-09-09 | WP-T10c — fork-parent reference updated |

## Refreshing the docs after upstream changes

For one project (from that project's working copy):

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
