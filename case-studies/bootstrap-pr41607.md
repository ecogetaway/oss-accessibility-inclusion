# Case Study: Bootstrap — PR #41607

## Repository
[twbs/bootstrap](https://github.com/twbs/bootstrap)

## PR
[#41607 — fix(modal): prevent focus on modal container with negative tabindex](https://github.com/twbs/bootstrap/pull/41607)

## Category
Complex widget interaction (stalled / closed-unmerged)

## What Happened
A keyboard user reported that Bootstrap's modal focus trap created an extra, unwanted Tab stop on the modal's own container element (which has `tabindex="-1"` and no visible content) before reaching the close button — an unnecessary and confusing stop in the tab sequence for keyboard-only users. A community contributor submitted a fix: `FocusTrap._handleFocusin` was changed to skip elements with a negative `tabIndex`, since those aren't meant to be part of the normal tab order, with a test added to cover the new behavior. The PR received no review of any kind for roughly eleven months, and was then closed — not because the fix was wrong, but because Bootstrap's v6 rewrite replaced the custom JS focus-trap with the native `<dialog>` element, which handles focus internally, making the patched code obsolete.

## Timeline
- Linked issue #41606 opened: keyboard-navigation bug report, no date recorded in the issue body
- PR opened: 2025-07-21
- PR closed (unmerged): 2026-06-27
- Days open: ~341 (~11 months)

## Rubric Scores

| Criterion | Score (0–2) | Justification |
| --- | --- | --- |
| User impact stated | 1 | The PR body explains the mechanism ("unwanted focus stop for keyboard users") but the underlying issue is described generically ("navigating using keyboard") rather than naming a specific user group or task breakdown. |
| WCAG mapping | 0 | No WCAG success criterion is cited anywhere, despite a clear fit (2.4.3 Focus Order). |
| AT testing evidence | 1 | A unit test was added to codify the new behavior, but there's no record of manual keyboard-only testing or AT verification by anyone — author or reviewer — at any point in the 11 months the PR was open. |
| Reviewer confidence signal | 0 | Zero reviews for the entire lifetime of the PR. The only comment, ever, is the maintainer's closing note eleven months later. |
| Direct language | 1 | "Keyboard users" is named directly in the PR body, but the discussion never goes deeper than that one mention. |
| Outcome clarity | 1 | The closing comment is clear about *why* it was closed (v6 rewrite obsoleted the code path), but it never engages with whether the original bug still exists in the new `<dialog>`-based implementation — an open question for a keyboard user filing a near-identical report against v6. |
| **Total** | **4/12** | |

## Review Pattern Observed
Eleven months of complete silence, then a single closing comment. This is not rejection on the merits — the maintainer never evaluated whether the fix was correct — it's a PR that outlived its own relevance while waiting for a review that never came. Distinct from the self-merge pattern seen in [Bootstrap #42539](bootstrap-pr42539.md) and [#42500](bootstrap-pr42500.md): those show a maintainer's own PRs shipping with zero external review; this shows a *contributor's* PR getting zero review of either kind, positive or negative, until unrelated architectural change made it moot.

## Infrastructure Gap Illustrated
This is the counter-example the v0.1 signals were missing: every prior case study in this repo merged within days. This one shows the failure mode the companion i18n repo documents extensively — a correct, well-scoped community contribution disappearing into review silence — can happen for accessibility PRs too, just less often in this small sample. A stale-PR triage process that periodically resurfaces old `accessibility`-labeled PRs (rather than letting them age out silently) would have caught this well before a major rewrite made the question moot, and would have given the original reporter (and the contributor) a real answer instead of an eleven-month wait for a technicality.

## Source
[github.com/twbs/bootstrap/pull/41607](https://github.com/twbs/bootstrap/pull/41607)
