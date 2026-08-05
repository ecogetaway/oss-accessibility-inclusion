# Case Study: Bootstrap — PR #42500

## Repository
[twbs/bootstrap](https://github.com/twbs/bootstrap)

## PR
[#42500 — Rework OTP input as a single accessible input with rendered slots](https://github.com/twbs/bootstrap/pull/42500)

## Category
Complex widget interaction

## What Happened
Bootstrap's original one-time-password (OTP) input rendered six separate `<input>` elements, one per digit, each requiring its own `aria-label` ("Digit 1", "Digit 2", ...). A community discussion ([#42486](https://github.com/twbs/bootstrap/discussions/42486)) raised the concern — not from an accessibility expert, but from someone who had built a similar OTP component in-house and explicitly disclaimed AT expertise "from an end-user perspective" — that reading six separately-labeled fields aloud would be tedious for screen-reader users, and that password managers and SMS autofill can't reliably target six discrete inputs. The PR replaced the six-input model with a single real `<input>` overlaid with decorative, `aria-hidden` slot elements, so assistive technology sees one field with one name, while sighted users still see individual digit boxes.

## Timeline
- Discussion #42486 opened: 2026-06-08 (miken32, "v6 Feedback" category)
- Discussion answered by coliff, pointing to this PR: 2026-06-11
- PR opened: 2026-06-11 03:21 UTC
- PR merged: 2026-06-11 16:56 UTC
- Open for: 13 hours 35 minutes
- Reporter confirmed the fix and marked the answer accepted: 2026-06-13 ("Nice! I guess it wasn't too late for a full redo of the thing")

## Rubric Scores

| Criterion | Score (0–2) | Justification |
| --- | --- | --- |
| User impact stated | 2 | PR body explicitly explains screen readers will now announce one field instead of one per digit, and that autofill/password managers are unblocked. |
| WCAG mapping | 2 | The PR body reasons explicitly about two success criteria — 3.3.8 Accessible Authentication (Minimum) and 1.3.5 Identify Input Purpose — and records that the rewritten docs anchor four in total (3.3.8, 1.3.5, 2.2.1, 3.3.7). The best standards work anywhere in the corpus. |
| Verification evidence | 0 | The testing section lists 1,049 passing Karma specs, clean ESLint and Stylelint, a Sass compile and a docs build — and no assistive technology at all. No screen-reader session, transcript, AT name or version appears anywhere in the thread. |
| Reviewer confidence signal | 0 | Zero reviews, zero comments. A CODEOWNERS team review was requested and never delivered. Merged 13 hours 35 minutes later by the same maintainer who opened it — no second party verified the accessibility claim before it merged. |
| Direct language | 1 | The PR body itself is precise about screen readers and autofill, but the originating discussion is framed by its author as coming from someone with no AT end-user experience — the person who raised the concern explicitly disclaimed that specific expertise (not implementation expertise: they had already built a comparable component). |
| Outcome clarity | 2 | The technical rationale is well documented, and the loop back to the reporter is closed: coliff answered the originating discussion pointing to this PR and the updated docs, and the reporter replied "Nice! I guess it wasn't too late for a full redo of the thing," marking the answer accepted. A future reader can see the concern raised, the fix shipped, and the reporter's confirmation, without inference. |
| **Total** | **7/12** | |

## Review Pattern Observed
Same pattern as [#42539](bootstrap-pr42539.md): a maintainer with commit rights self-merges within hours with strong written justification (including WCAG citations here) but no reviewer and no recorded AT verification — the rubric-relevant gap is entirely on the testing-evidence axis, not the reasoning axis.

## Infrastructure Gap Illustrated
The originating discussion was raised by someone who explicitly disclaimed AT expertise from an end-user perspective — exactly the maintainer-capacity gap described in this repo's problem statement, though notably not by someone inexperienced with the problem: they had already built a comparable OTP component of their own. The fix that resulted was well-reasoned, but nothing in the process required an actual AT test pass (as opposed to unit tests) before merge, and no one with hands-on screen-reader experience is visible anywhere in either thread.

## Verification
Re-verified 2026-07-29 and again 2026-08-04 against the live PR page, the GitHub API, and Discussion #42486. Score changed from 6/12 to 7/12. Findings:

- **The consequence is documented.** Seven days after this merged, the same maintainer opened [#42524](bootstrap-pr42524.md) — "OTP: fix click-to-focus and overwrite-on-retype" — whose own PR body states that this rework "improved accessibility but left two interaction gaps reported after merge." An unreviewed same-day self-merge merged with defects that a review would plausibly have caught. This is the only place in the corpus where the cost of the missing review is visible rather than hypothetical.
- **WCAG count corrected.** An earlier revision of this case study recorded two criteria; the PR names four. Two are reasoned about in the Accessibility paragraph, four are anchored in the rewritten docs.
- **Merged into `v6-dev`, not `main`** — so, as with #42539, no user of a released Bootstrap has this fix.
- **A CODEOWNERS team review was requested and never delivered.**
- **No `accessibility` label** — only `js` and `v6`.
- **The source was GitHub Discussion #42486**, not an issue.
- **API-confirmed interval: 2026-08-04.** Created 2026-06-11T03:21:43Z, merged 2026-06-11T16:56:39Z — 13 hours 34 minutes 56 seconds. `author_association: MEMBER`, `merged_by: mdo`, `comments: 0`, `review_comments: 0`, `auto_merge: null`.
- **Discussion #42486 re-read verbatim, 2026-08-04.** The reporter's actual words are "I'm not at all an expert on assistive technology from an end-user perspective" — the earlier version of this case study truncated the quote and glossed it as a general disclaimer of AT expertise. The reporter had in fact already built their own OTP implementation using a visually-hidden real input with `aria-hidden` decorative boxes — the same architecture this PR goes on to adopt — and described it as "our home-grown OTP component," not as a maintained public project. Corrected throughout: What Happened, Direct language, Infrastructure Gap.
- **Outcome clarity raised from 1 to 2.** The earlier version stated there was no closing comment confirming resolution from the reporter's perspective. There is one: coliff answered the discussion on 2026-06-12 linking this PR, and the reporter replied on 2026-06-13 confirming and marking the answer accepted. Total moves from 6/12 to 7/12 accordingly.

## Source
[github.com/twbs/bootstrap/pull/42500](https://github.com/twbs/bootstrap/pull/42500) · [discussion #42486](https://github.com/twbs/bootstrap/discussions/42486)
