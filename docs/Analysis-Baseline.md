# Analysis Baseline

The commit each project was at **when the docs in this folder were written**. When
a project gains new commits later, diff from the hash recorded here to see what
the umbrella docs still need to catch up on.

- Analysis date: **2026-09-05**
- All projects analysed on branch `main` unless noted.
- Project name = GitHub repo name under `github.com/svene/` (see
  [Variants.md](Variants.md) for links). `springboot-hono-docs` is local-only.

| Project | Branch | Commit at analysis | Date | Subject |
|---|---|---|---|---|
| `2025-08-23_ssfe-patterns-jte-htmx` | main | `9d03e03` | 2025-08-24 | documented Template-Injection pattern and Template-Inclusion pattern |
| `2025-08-23_ssfe-patterns-jte-vc-htmx` | main | `6dc16fb` | 2026-05-10 | s05: extracted the documentation |
| `2025-08-23_ssfe-patterns-thymeleaf-htmx` | main | `07b4d91` | 2025-08-23 | springboot code: controller working |
| `2025-12-21_ssfe-patterns-quarkus-qute-htmx` | main | `afab795` | 2026-01-15 | code for M05 |
| `2025-12-27_ssfe-patterns-hono-htmx` | main | `ed939ef` | 2026-05-30 | moved tnt.md to docs project |
| `2025-12-31-springboot-hono-poc` | main | `8016781` | 2026-08-30 | upgrade alpinejs |
| `2026-01-24_hda-dynapage-demo` | main | `b63fcf9` | 2026-08-31 | implemented hx-partial variant with the help of AI. I like it better than the OOB variant … |
| `2026-03-07_springboot-graalvm-jsx-poc` | main | `273832e` | 2026-03-10 | todo |
| `2026-03-09_hda-springboot-graalvm-jsx-demo` | main | `e854c30` | 2026-09-01 | architecture.md |
| `2026-03-15_hda-quarkus-graalvm-jsx-demo` | main | `c59b3dc` | 2026-09-01 | architecture.md |
| `2026-09-03_hda-springboot-browser-hono` | main | `5ec1511` | 2026-09-05 | updates to docs |
| `2026-09-03_hda-quarkus-browser-hono` | main | `d18bf57` | 2026-09-05 | doc updates |
| `2026-05-01_springboot-hono-docs` | master | `9c6ceca` | 2026-05-02 | some examples and settings for code documentation |
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
