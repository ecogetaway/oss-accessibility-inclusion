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
- PR merged: 2026-06-23
- Days open: ~1

## Rubric Scores

| Criterion | Score (0–2) | Justification |
| --- | --- | --- |
| User impact stated | 2 | PR body and linked issue both name the specific problem: screen readers announce the value before the label, citing NVDA explicitly. |
| WCAG mapping | 0 | No success criterion cited anywhere in the PR, issue, or commit — despite this being a clean fit for 1.3.1 (Info and Relationships) / 4.1.2 (Name, Role, Value). |
| AT testing evidence | 1 | The original issue reporter tested with NVDA + Chrome + Windows and described the exact reproduction. No evidence in the PR that the fix was re-verified with AT before merge. |
| Reviewer confidence signal | 0 | Zero reviews, zero comments (inline or issue-level). The PR was opened and merged by the same author, a maintainer with direct commit rights — no second party engaged with the accessibility claim at all. |
| Direct language | 2 | "Screen readers (e.g. NVDA)" and "announced ... after" are specific and person-centered, not generic "a11y fix" language. |
| Outcome clarity | 1 | The PR body explains the technical rationale clearly (browser support for `:has()`, why label-first now works), but there's no confirmation the fix was checked against the original reporter's repro, and the issue thread itself was not closed with a comment. |
| **Total** | **6/12** | |

## Review Pattern Observed
Self-merge by a maintainer with commit authority, same day the PR was opened, with no reviewer of any kind — the accessibility claim was accepted on the author's word alone.

## Infrastructure Gap Illustrated
The fix was correct and the impact was well-described, but nothing in the process required a WCAG citation or a second-party AT check before merge. A maintainer with commit rights can ship an accessibility change entirely on self-assessment; a PR template prompting for "WCAG SC" and "verified with AT: yes/no, which one" would make that assessment visible even when the author and merger are the same person.

## Source
[github.com/twbs/bootstrap/pull/42539](https://github.com/twbs/bootstrap/pull/42539)
