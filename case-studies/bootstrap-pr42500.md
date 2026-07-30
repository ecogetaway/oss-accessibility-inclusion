# Case Study: Bootstrap — PR #42500

## Repository
[twbs/bootstrap](https://github.com/twbs/bootstrap)

## PR
[#42500 — Rework OTP input as a single accessible input with rendered slots](https://github.com/twbs/bootstrap/pull/42500)

## Category
Complex widget interaction

## What Happened
Bootstrap's original one-time-password (OTP) input rendered six separate `<input>` elements, one per digit, each requiring its own `aria-label` ("Digit 1", "Digit 2", ...). A community discussion (#42486) raised the concern — not from an accessibility expert, but from a maintainer of a similar component elsewhere — that reading six separately-labeled fields aloud would be tedious for screen-reader users, and that password managers and SMS autofill can't reliably target six discrete inputs. The PR replaced the six-input model with a single real `<input>` overlaid with decorative, `aria-hidden` slot elements, so assistive technology sees one field with one name, while sighted users still see individual digit boxes.

## Timeline
- Discussion #42486 opened: 2026 (raised as a question, not a bug report, by a non-expert contributor)
- PR opened: 2026-06-11
- PR merged: 2026-06-11
- Days open: 0 (same day)

## Rubric Scores

| Criterion | Score (0–2) | Justification |
| --- | --- | --- |
| User impact stated | 2 | PR body explicitly explains screen readers will now announce one field instead of one per digit, and that autofill/password managers are unblocked. |
| WCAG mapping | 2 | The PR body reasons explicitly about two success criteria — 3.3.8 Accessible Authentication (Minimum) and 1.3.5 Identify Input Purpose — and records that the rewritten docs anchor four in total (3.3.8, 1.3.5, 2.2.1, 3.3.7). The best standards work anywhere in the corpus. |
| Verification evidence | 0 | The testing section lists 1,049 passing Karma specs, clean ESLint and Stylelint, a Sass compile and a docs build — and no assistive technology at all. No screen-reader session, transcript, AT name or version appears anywhere in the thread. |
| Reviewer confidence signal | 0 | Zero reviews, zero comments. A CODEOWNERS team review was requested and never delivered. Merged 14 hours later by the same maintainer who opened it — no second party verified the accessibility claim before it shipped. |
| Direct language | 1 | The PR body itself is precise about screen readers and autofill, but the originating discussion is framed as "I'm not at all an expert on assistive technology" — the person who raised the concern explicitly disclaimed AT expertise. |
| Outcome clarity | 1 | The technical rationale is well documented, but there's no closing comment on the discussion confirming the concern was resolved from the reporter's perspective. |
| **Total** | **6/12** | |

## Review Pattern Observed
Same pattern as #42539: a maintainer with commit rights self-merges same-day with strong written justification (including WCAG citations here) but no reviewer and no recorded AT verification — the rubric-relevant gap is entirely on the testing-evidence axis, not the reasoning axis.

## Infrastructure Gap Illustrated
The originating discussion was raised by someone who explicitly said they weren't an AT expert — exactly the maintainer-capacity gap described in this repo's problem statement. The fix that resulted was well-reasoned, but nothing in the process required an actual AT test pass (as opposed to unit tests) before merge, and no one with hands-on screen-reader experience is visible anywhere in the thread.

## Verification
Re-verified 2026-07-29 against the live PR page. Score unchanged at 6/12. Findings:

- **The consequence is documented.** Seven days after this merged, the same maintainer opened [#42524](bootstrap-pr42524.md) — "OTP: fix click-to-focus and overwrite-on-retype" — whose own PR body states that this rework "improved accessibility but left two interaction gaps reported after merge." An unreviewed same-day self-merge shipped defects that a review would plausibly have caught. This is the only place in the corpus where the cost of the missing review is visible rather than hypothetical.
- **WCAG count corrected.** An earlier revision of this case study recorded two criteria; the PR names four. Two are reasoned about in the Accessibility paragraph, four are anchored in the rewritten docs.
- **Merged into `v6-dev`, not `main`** — so, as with #42539, no user of a released Bootstrap has this fix.
- **A CODEOWNERS team review was requested and never delivered.**
- **No `accessibility` label** — only `js` and `v6`.
- **The source was GitHub Discussion #42486**, not an issue.

## Source
[github.com/twbs/bootstrap/pull/42500](https://github.com/twbs/bootstrap/pull/42500)
