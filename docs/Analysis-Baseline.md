# Analysis Baseline

The commit each project was at **when the docs in this folder were written**. When
a project gains new commits later, diff from the hash recorded here to see what
the umbrella docs still need to catch up on.

- Analysis date: **2026-09-05**
- All projects analysed on branch `main` unless noted.
- Project name = GitHub repo name under `github.com/svene/` (see
  [Variants.md](Variants.md) for links). The throwaway spike
  `2026-05-01_springboot-hono-docs` (local-only, superseded) is not tracked here.

| Project | Branch | Commit at analysis | Date | Subject |
|---|---|---|---|---|
| `2025-08-23_ssfe-patterns-jte-htmx` | main | `e2cba81` | 2026-09-05 | htmx4 upgrade |
| `2025-08-23_ssfe-patterns-jte-vc-htmx` | main | `5089f49` | 2026-09-05 | bulma vendored |
| `2025-08-23_ssfe-patterns-thymeleaf-htmx` | main | `07b4d91` | 2025-08-23 | springboot code: controller working |
| `2025-12-21_ssfe-patterns-quarkus-qute-htmx` | main | `6049e32` | 2026-09-05 | vendored bulma |
| `2025-12-27_ssfe-patterns-hono-htmx` | main | `7400027` | 2026-09-05 | vendored bulma |
| `2025-12-31-springboot-hono-poc` | main | `4e6f9aa` | 2026-09-05 | vendored bulma |
| `2026-01-24_hda-dynapage-demo` | main | `0d3df4f` | 2026-09-05 | vendored bulma |
| `2026-03-07_springboot-graalvm-jsx-poc` | main | `273832e` | 2026-03-10 | todo |
| `2026-03-09_hda-springboot-graalvm-jsx-demo` | main | `515fd94` | 2026-09-05 | vendored bulma |
| `2026-03-15_hda-quarkus-graalvm-jsx-demo` | main | `74384ac` | 2026-09-05 | vendored bulma |
| `2026-09-03_hda-springboot-browser-hono` | main | `68371c1` | 2026-09-05 | vendored bulma |
| `2026-09-03_hda-quarkus-browser-hono` | main | `8c50787` | 2026-09-05 | vendored bulma |
| `2026-05-02_ssfe-patterns-jte-vc-htmx-docs` | main | `fd414ca` | 2026-05-30 | added intellij idea section to .gitignore |

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
