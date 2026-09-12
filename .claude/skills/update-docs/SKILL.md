---
name: update-docs
description: Refresh this umbrella project's docs/*.md files against upstream changes in the sibling projects, using docs/ai/Analysis-Baseline.md as the record of what was last analysed. Use when the user asks to "update the docs", "refresh the docs", or check whether the docs are current.
---

# Update docs

Sweeps every sibling project listed in `docs/ai/Analysis-Baseline.md`, finds
what changed since it was last analysed, updates the affected `docs/*.md`
files, and bumps the baseline. This is the umbrella project's own maintenance
cycle — see `docs/ai/wip.md` ("Approach") and `README_details.md` ("Keeping
the docs current") for the surrounding rules.

## Scope for this run

- If the user named specific project(s) in their request, only sweep those
  rows of the baseline table.
- Otherwise sweep every row.
- Never touch the throwaway spike `2026-05-01_springboot-hono-docs` — it is
  intentionally not tracked in the baseline.

## Steps

1. **Read `docs/ai/Analysis-Baseline.md`** for the project ↔ recorded-hash
   table.

2. **For each project in scope**, find its local checkout. Siblings live one
   level above this repo, split into `2025/` and `2026/` by the year in the
   project's own name — e.g. `2025-08-23_hypermedia-patterns-jte-htmx` is at
   `../../2025/2025-08-23_hypermedia-patterns-jte-htmx` relative to this repo, and
   `2026-01-24_hypermedia-dynapage-demo` is at
   `../../2026/2026-01-24_hypermedia-dynapage-demo`.

3. **Diff against the recorded hash**, from this repo (no need to `cd`):

   ```sh
   git -C <path-to-project> log --oneline <recorded-hash>..HEAD
   ```

   - Empty output → nothing changed for this project. Skip it (don't touch its
     baseline row).
   - Non-empty → look closer: `git -C <path> log -p <recorded-hash>..HEAD` or
     `git -C <path> diff <recorded-hash>..HEAD --stat` to see what actually
     changed, not just the commit subjects (a commit message like "cleanup"
     can hide a real behavioural or structural change, and conversely a
     verbose message can turn out to be internal-only).

4. **Decide if it's doc-relevant.** This project's whole discipline is: the
   umbrella documents **high-level concepts and cross-variant differences
   only** — never variant internals (see `docs/ai/wip.md` → Conventions, and
   `README.md` → "It stays at a high level…"). Most commits (dependency bumps,
   refactors, test additions, typo fixes) are *not* doc-relevant. Only update
   the docs for things that change:
   - the project's role, stack, or its one distinguishing idea (→
     `docs/Variants.md`)
   - a concept adopted, dropped, or changed compared to a sibling (→
     `docs/History.md`, `docs/Variant-Comparison.md`)
   - a fact recorded in `docs/Learnings.md`'s audit tables

   If nothing doc-relevant turns up, say so and still bump the baseline row
   (the project has been reviewed, even if nothing needed to change).

5. **Update the affected `docs/*.md` files.** Follow the existing conventions:
   short catalog entries (see `docs/ai/wip.md` → "Catalog entry shape"), no
   Claude-addressing or "the user decided" phrasing (those stay out of
   `docs/*`, `README.md`, `README_details.md` — see project memory), no
   project-copy lineage in public docs.

6. **Bump `docs/ai/Analysis-Baseline.md`**: that project's row (new hash,
   commit date, one-line subject) and the top-level "Analysis date" note
   (mention which projects moved and why, briefly — see existing entries in
   that file for the tone).

7. **Report and stop.** This repo's rule: Claude edits files, the user reviews
   and commits — don't commit or push. Summarize, per project: no change /
   what changed in the docs and why / baseline bumped. If a project's own repo
   needs a corresponding edit (rare — this project only reads siblings, it
   never modifies them), say so instead of doing it.
