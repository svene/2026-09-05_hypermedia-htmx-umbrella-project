# Analysis Baseline

AI-facing tracking file (see `docs/ai/` — kept separate from the user-facing
docs in `docs/`, moved here 2026-09-12). The commit each project was at **when
the `docs/*.md` files were last written**. When a project gains new commits
later, diff from the hash recorded here to see what the umbrella docs still
need to catch up on.

- Analysis date: **2026-09-12** (baseline re-synced to each project's current
  HEAD; the 2026-09-06 Thymeleaf build-out and the 2026-09-07 per-project
  `playwright/` additions (WP-T12) are reflected — neither changes doc-relevant
  content beyond what the umbrella docs already cover. The full WP22 rename —
  all 11 `ssfe-*`/`hda-*` repos, WP-T13 through WP-T23, plus every follow-up
  fix found during the post-WP22 review (missed `SSFE-Patterns` subtitles,
  stale copy-pasted README titles, a leftover `HDA` acronym, a stale
  `JSX`→`Hono` wording fix) — is reflected. Re-ran this `update-docs` sweep
  2026-09-12 and found 9 of the 13 rows had a stale hash left over from a
  follow-up commit that landed after that row was last bumped; all pure
  renames/internal-path/wording fixes, already covered by the doc updates
  made in the same turns — no new doc-relevant content, just caught-up hashes.
  Also reflects the plain-JTE variant's build-out (2026-09-12, with Claude):
  the last remaining `docs/ai/wip.md` TODO, bringing `hypermedia-patterns-jte-htmx`
  from a 2-page WIP demo up to the full `s01/s03/s04/s05` course — `docs/Variants.md`,
  `docs/Variant-Comparison.md`, `docs/History.md` and `docs/Learnings.md` updated
  accordingly)
- All projects analysed on branch `main` unless noted.
- Project name = GitHub repo name under `github.com/svene/` (see
  [../Variants.md](../Variants.md) for links). The throwaway spike
  `2026-05-01_springboot-hono-docs` (local-only, superseded) is not tracked here.

| Project | Branch | Commit at analysis | Date | Subject |
|---|---|---|---|---|
| `2025-08-23_hypermedia-patterns-jte-htmx` | main | `e8d3999` | 2026-09-12 | Built out the full `s01/s03/s04/s05` course (with Claude), replacing the 2-page WIP demo |
| `2025-08-23_hypermedia-patterns-jte-vc-htmx` | main | `edbc335` | 2026-09-12 | WP-T14 — renamed from `…_ssfe-patterns-jte-vc-htmx` |
| `2025-08-23_hypermedia-patterns-thymeleaf-htmx` | main | `bb43829` | 2026-09-12 | WP-T21 follow-up — fixed 5 back-references to the renamed docs project (readme + 4 javadocs) |
| `2025-12-21_hypermedia-patterns-quarkus-qute-htmx` | main | `6169029` | 2026-09-12 | Follow-up sweep — fixed a missed `SSFE-Patterns` display subtitle in `s03d04mpalayout.html` |
| `2025-12-27_hypermedia-patterns-hono-htmx` | main | `3393f62` | 2026-09-12 | WP-T17 — renamed from `…_ssfe-patterns-hono-htmx` |
| `2025-12-31-springboot-hono-poc` | main | `4e6f9aa` | 2026-09-05 | vendored bulma |
| `2026-01-24_hypermedia-dynapage-demo` | main | `dc1d5e9` | 2026-09-12 | Follow-up — retitled `hono/README.md` (was recycled from the `springboot-hono-poc` fork-parent) |
| `2026-03-07_springboot-graalvm-jsx-poc` | main | `fa71d84` | 2026-09-12 | WP-T19 follow-up — relative link to the renamed `…-graalvm-hono-demo` fixed; own title deliberately left (historical PoC) |
| `2026-03-09_hypermedia-springboot-graalvm-hono-demo` | main | `0e6c0b3` | 2026-09-12 | WP-T19 rename + follow-up JSX→Hono title/wording fix in `readme.md` |
| `2026-03-15_hypermedia-quarkus-graalvm-hono-demo` | main | `f23d547` | 2026-09-12 | WP-T20 rename + follow-up fix of a stale copy-pasted `README.md` title |
| `2026-05-02_hypermedia-htmx-patterns-docs` | main | `9e50ff6` | 2026-09-12 | WP-T21 rename + follow-up `astro.config.mjs` site-title and `README.md` title/coverage fixes |
| `2026-09-03_hypermedia-springboot-browser-hono` | main | `0a483c3` | 2026-09-12 | WP-T22 — renamed from `…_hda-springboot-browser-hono` |
| `2026-09-03_hypermedia-quarkus-browser-hono` | main | `5b8da7f` | 2026-09-12 | WP-T23 — renamed from `…_hda-quarkus-browser-hono` (WP22 complete) |

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
