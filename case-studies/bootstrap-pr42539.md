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
- Linked issue (#41362) opened: 2025 (reporter: HalHaynes, against Bootstrap v5.3.3)
- PR opened: 2026-06-22
- PR merged into `v6-dev` (not `main`): 2026-06-23
- Days open: ~1 (about 36 hours)
- Linked issue #41362 closed as completed by the PR author, same day as the merge, with no closing comment

## Rubric Scores

| Criterion | Score (0–2) | Justification |
| --- | --- | --- |
| User impact stated | 2 | PR body and linked issue both name the specific problem: screen readers announce the value before the label, citing NVDA explicitly. |
| WCAG mapping | 0 | No success criterion cited anywhere in the PR, issue, or commit — despite this being a clean fit for 1.3.1 (Info and Relationships) / 4.1.2 (Name, Role, Value). |
| Verification evidence | 1 | The original issue reporter (HalHaynes) tested with NVDA on Chrome under Windows against v5.3.3 and described the exact reproduction. Band 1 rather than 2 because the evidence predates the fix and was never repeated: nobody re-verified with a screen reader before merge. |
| Reviewer confidence signal | 0 | Zero reviews, zero comments, one participant. A CODEOWNERS rule *did* request a team review — and the change merged without one. The PR was opened and merged by the same maintainer; no second party engaged with the accessibility claim at all. |
| Direct language | 2 | "Screen readers (e.g. NVDA)" and "announced ... after" are specific and person-centered, not generic "a11y fix" language. |
| Outcome clarity | 1 | The chain is traceable — issue, cross-referenced PR, merge commits, closure as completed — so a future contributor can follow it without guessing. But the issue was closed as *completed* while the fix exists only in the unreleased `v6-dev` branch, with no comment to the reporter, who filed against v5.3.3 and still has the bug in every released version. |
| **Total** | **6/12** | |

## Review Pattern Observed
Self-merge by a maintainer with commit authority, same day the PR was opened, with no reviewer of any kind — the accessibility claim was accepted on the author's word alone.

## Verification
Re-verified 2026-07-29 against the live PR and issue pages. Score unchanged at 6/12. Findings:

- **Merged into `v6-dev`, not `main`.** Bootstrap 6 is unreleased, so roughly fourteen and a half months after HalHaynes filed the report, the defect is still present in every shipped version. The earlier write-up said only "merged."
- **A CODEOWNERS team review was requested and never delivered** — the first of five such instances across the corpus.
- **Issue #41362 was closed as completed** by the PR author on the day of the merge, with the PR cross-referenced but no comment written.
- **The `:has()` technique was not the author's.** It was proposed with worked selectors by a community commenter (RichardD2) in the issue thread in April 2025, and a maintainer replied at the time that it would become viable in v6. The PR body presents the approach without pointing back to that thread, though "Fixes #41362" keeps it reachable.
- **The PR carries no `accessibility` label** — only `css`, `js`, `v6`. Neither of this maintainer's two accessibility PRs is labelled accessibility, while an outside contributor's accessibility PR in the same repository was labelled within hours. Anyone auditing this project by label would not find this PR.

## Infrastructure Gap Illustrated
The fix was correct and the impact was well-described, but nothing in the process required a WCAG citation or a second-party AT check before merge. A maintainer with commit rights can ship an accessibility change entirely on self-assessment; a PR template prompting for "WCAG SC" and "verified with AT: yes/no, which one" would make that assessment visible even when the author and merger are the same person.

## Source
[github.com/twbs/bootstrap/pull/42539](https://github.com/twbs/bootstrap/pull/42539)
