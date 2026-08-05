# Case Study: Bootstrap — PR #41607

## Repository
[twbs/bootstrap](https://github.com/twbs/bootstrap)

## PR
[#41607 — fix(modal): prevent focus on modal container with negative tabindex](https://github.com/twbs/bootstrap/pull/41607)

## Category
Complex widget interaction (stalled / closed-unmerged)

## What Happened
A keyboard user reported that Bootstrap's modal focus trap created an extra, unwanted Tab stop on the modal's own container element (which has `tabindex="-1"` and no visible content) before reaching the close button — an unnecessary and confusing stop in the tab sequence for keyboard-only users. A community contributor submitted a fix: `FocusTrap._handleFocusin` was changed to skip elements with a negative `tabIndex`, since those aren't meant to be part of the normal tab order, with the existing test updated — its assertion inverted — to match the new behavior. The PR received no review of any kind for roughly eleven months, and was then closed — not because the fix was wrong, but because Bootstrap's v6 rewrite replaced the custom JS focus-trap with the native `<dialog>` element, which handles focus internally, making the patched code obsolete.

## Timeline
- Linked issue #41606 opened by Saisailaja-ux (Windows, Edge): 2025-07-21
- Independently confirmed the same day by DerLukas15 (Linux/Firefox), who bisected the regression to 5.3.7 with 5.3.5 as the last working version
- PR opened by killerdevildog: 2025-07-21 (2025-07-22 in the web UI's local time)
- `js` and `accessibility` labels applied by a maintainer within hours of the PR opening
- Further analysis contributed by Jacky040124 in a fork: 2026-01
- Issue #41606 closed as completed: 2026-06-24
- PR closed (unmerged): 2026-06-27 (2026-06-28 in the web UI's local time)
- Days open: ~341 (~11 months)

## Rubric Scores

| Criterion | Score (0–2) | Justification |
| --- | --- | --- |
| User impact stated | 1 | The PR body explains the mechanism ("unwanted focus stop for keyboard users") but the underlying issue is described generically ("navigating using keyboard") rather than naming a specific user group or task breakdown. |
| WCAG mapping | 0 | No WCAG success criterion is cited anywhere, despite a clear fit (2.4.3 Focus Order). |
| Verification evidence | 1 | Two independent reporters described the defect on named platforms — Windows/Edge and Linux/Firefox — and one bisected it to a specific release. The existing test was updated, its assertion inverted to expect the new behaviour, but no new test case was added. All of this evidence is pre-fix and from reporters: no one, author or reviewer, verified the patched behaviour by keyboard at any point in the eleven months the PR was open. |
| Reviewer confidence signal | 0 | Zero reviews for the entire lifetime of the PR. A CODEOWNERS team review was requested on day one and never delivered. The only comment, ever, is the maintainer's closing note eleven months later. |
| Direct language | 1 | "Keyboard users" is named directly in the PR body, but the discussion never goes deeper than that one mention. |
| Outcome clarity | 1 | The closing comment is clear about *why* it was closed (v6 rewrite obsoleted the code path), but it never engages with whether the original bug still exists in the new `<dialog>`-based implementation — an open question for a keyboard user filing a near-identical report against v6. |
| **Total** | **4/12** | |

## Review Pattern Observed
Eleven months of complete silence, then a single closing comment. This is not rejection on the merits — the maintainer never evaluated whether the fix was correct — it's a PR that outlived its own relevance while waiting for a review that never came. Distinct from the self-merge pattern seen in [Bootstrap #42539](bootstrap-pr42539.md) and [#42500](bootstrap-pr42500.md): those show a maintainer's own PRs merging with zero external review while still unreleased; this shows a *contributor's* PR getting zero review of either kind, positive or negative, until unrelated architectural change made it moot.

## Verification
Re-verified 2026-07-29 and again 2026-08-04 against the live PR and issue pages, and against the Commits and Files-changed tabs. Score unchanged at 4/12. Findings:

- **It was triaged correctly within hours, and then ignored.** A maintainer applied both `js` and `accessibility` labels the same day the PR opened. This removes the most natural defence — that nobody noticed it — and is a sharper framing than "waited eleven months without a review comment."
- **A CODEOWNERS team review was requested and never delivered.** This is the earliest of the four such requests confirmed across the corpus.
- **Four people engaged; no maintainer reviewed.** The reporter, an independent confirmer who bisected the regression, the contributor who fixed it, and a fourth who added analysis in January. The only maintainer actions in eleven months were a label and a closure.
- **It was a shipped regression, not an ancient defect.** DerLukas15 identified 5.3.7 as the first broken release and 5.3.5 as the last working one, within a day of the original report — the easiest possible case for a review process to act on.
- **The linked issue was closed on an expectation, not a verification.** The closing note says the stray focus stop "shouldn't occur" under v6's native `<dialog>` handling and invites the reporters to open a new issue if they still see it — asking people running 5.3.7 to verify against a branch they cannot run.
- **No test was added, contrary to an earlier version of this case study.** The changed spec file is +2/−2: the existing test was renamed from "should force focus on itself if there is no focusable content" to "should not force focus on element with negative tabindex if there is no focusable content," and its assertion inverted from `toHaveBeenCalled()` to `not.toHaveBeenCalled()`. The author's own PR body says "Updated test to expect the new behavior" — accurately; the case study's earlier "a test was added" did not.
- **Never merged, so never released to a Bootstrap user.** Two commits into `main` were requested; none landed.
- **Note on dates.** The web UI shows 22 Jul 2025 to 28 Jun 2026 in local time; the API reports 21 Jul and 27 Jun in UTC. Both are correct; the interval is 341 days either way.
- **Page shows three participants.** Two of the three interactions were a label action and a closing note, not review — worth stating pre-emptively, since the participant count reads against a claim of silence.

## Infrastructure Gap Illustrated
This is the counter-example the v0.1 signals were missing: every prior case study in this repo merged within days. This one shows the failure mode the companion i18n repo documents extensively — a correct, well-scoped community contribution disappearing into review silence — can happen for accessibility PRs too, just less often in this small sample. A stale-PR triage process that periodically resurfaces old `accessibility`-labeled PRs (rather than letting them age out silently) would have caught this well before a major rewrite made the question moot, and would have given the original reporter (and the contributor) a real answer instead of an eleven-month wait for a technicality.

## Source
[github.com/twbs/bootstrap/pull/41607](https://github.com/twbs/bootstrap/pull/41607)
