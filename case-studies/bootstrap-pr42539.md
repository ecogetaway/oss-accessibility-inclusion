# Case Study: Bootstrap — PR #42539

## Repository
[twbs/bootstrap](https://github.com/twbs/bootstrap)

## PR
[#42539 — Floating labels: place label before control for screen readers](https://github.com/twbs/bootstrap/pull/42539)

## Category
Semantics / reading order

## What Happened
Bootstrap's floating-label form control required the `<input>` to precede the `<label>` in the DOM so a CSS sibling selector (`~`) could animate the label. That source order meant screen readers (reported specifically with NVDA on Chrome/Windows in the linked issue) announced the field's value before its label — the user hears a value with no name attached to it yet. The fix rewrote the SCSS to use `:has()` so the label could move first in the DOM while keeping the same visual animation, and reordered the label/input markup across the docs and example pages to match.

## Timeline
- Linked issue (#41362) opened: 2025-04-10 (reporter: HalHaynes, against Bootstrap v5.3.3)
- PR opened: 2026-06-22 05:51 UTC
- PR merged into `v6-dev` (not `main`): 2026-06-23 17:27 UTC
- Open for: 35 hours 36 minutes
- Linked issue #41362 auto-closed by GitHub's `Fixes #41362` keyword eleven seconds after the merge, attributed to the merging author

## Rubric Scores

| Criterion | Score (0–2) | Justification |
| --- | --- | --- |
| User impact stated | 2 | PR body and linked issue both name the specific problem: screen readers announce the value before the label, citing NVDA explicitly. |
| WCAG mapping | 0 | No success criterion cited anywhere in the PR, issue, or commit — despite this being a clean fit for 1.3.1 (Info and Relationships) / 4.1.2 (Name, Role, Value). |
| Verification evidence | 1 | The original issue reporter (HalHaynes) tested with NVDA on Chrome under Windows against v5.3.3 and described the exact reproduction. The PR's own stated testing for the merged code is narrower still — "SCSS compiles clean and passes stylelint" — and no automated tests exist for this change; the only test-adjacent file touched is a visual fixture whose markup was mechanically reordered to match, not a new assertion. Band 1 rather than 2 because the AT evidence predates the fix and was never repeated: nobody re-verified with a screen reader before merge, and what verification the merged code actually received is a compiler and a linter. |
| Reviewer confidence signal | 0 | Zero reviews, zero comments, one participant. A CODEOWNERS rule *did* request a team review — and the change merged without one. The PR was opened and merged by the same maintainer; no second party engaged with the accessibility claim at all. |
| Direct language | 2 | "Screen readers (e.g. NVDA)" and "announce ... after" are specific and person-centered, not generic "a11y fix" language. |
| Outcome clarity | 1 | The chain is traceable — issue, cross-referenced PR, merge commits, auto-closure — so a future contributor can follow it without guessing. But the issue closed the instant the PR merged, by automation rather than a person, while the fix exists only in the unreleased `v6-dev` branch, with no comment ever written to the reporter — who filed against v5.3.3 fourteen and a half months earlier and still has the bug in every released version. |
| **Total** | **6/12** | |

## Review Pattern Observed
Self-merge by a maintainer with commit authority, within thirty-six hours of opening, with no reviewer of any kind — the accessibility claim was accepted on the author's word alone.

## Verification
Re-verified 2026-07-29 and again 2026-08-04 (against the GitHub API for both this PR and issue #41362) against the live PR and issue pages. Score unchanged at 6/12. Findings:

- **Merged into `v6-dev`, not `main`.** Bootstrap 6 is unreleased, so roughly fourteen and a half months after HalHaynes filed the report (10 April 2025, confirmed via API; 439 days to merge), the defect is still present in every released version as of August 2026. The earlier write-up said only "merged."
- **A CODEOWNERS team review was requested and never delivered** — one of four such requests confirmed across the corpus, all in Bootstrap. The earliest was on [#41607](bootstrap-pr41607.md), roughly eleven months before this one; this is not the first chronologically, an earlier version of this note said so in error.
- **Issue #41362 was not closed by a decision.** `closed_at` is eleven seconds after `merged_at` — GitHub's `Fixes #41362` keyword closed it automatically and attributed the action to the merging author. Nobody chose to close it without replying to HalHaynes; automation closed it, and nobody appears to have noticed that the reporter, who had waited fourteen months, was never directly answered. An earlier version of this case study described the closure as a deliberate act by the PR author; it was not.
- **The `:has()` technique was not the author's.** It was proposed with worked selectors by a community commenter (RichardD2) in the issue thread in April 2025, and a maintainer replied at the time that it would become viable in v6. The PR body presents the approach without pointing back to that thread, though "Fixes #41362" keeps it reachable.
- **The PR carries no `accessibility` label** — only `css`, `js`, `v6`. None of this maintainer's three accessibility PRs is labelled accessibility, while an outside contributor's accessibility PR in the same repository was labelled within hours. Anyone auditing this project by label would not find this PR. The originating issue #41362 itself does carry the `accessibility` label (plus `v6` and `revisit-browserslist`) — the same pattern as [#42500](bootstrap-pr42500.md), where the discussion behind the fix is labelled and the fix is not.
- **API-confirmed interval, 2026-08-04.** Created 2026-06-22T05:51:47Z, merged 2026-06-23T17:27:23Z — 35 hours 35 minutes 36 seconds. `author_association: MEMBER`, `comments: 0`, `review_comments: 0`, `auto_merge: null`, 9 files changed, +126/−121, 1 commit.

## Infrastructure Gap Illustrated
The fix was correct and the impact was well-described, but nothing in the process required a WCAG citation or a second-party AT check before merge. A maintainer with commit rights can ship an accessibility change entirely on self-assessment; a PR template prompting for "WCAG SC" and "verified with AT: yes/no, which one" would make that assessment visible even when the author and merger are the same person.

## Source
[github.com/twbs/bootstrap/pull/42539](https://github.com/twbs/bootstrap/pull/42539) · [issue #41362](https://github.com/twbs/bootstrap/issues/41362)
