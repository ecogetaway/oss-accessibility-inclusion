# Case Study: Bootstrap — PR #42524

## Repository
[twbs/bootstrap](https://github.com/twbs/bootstrap)

## PR
[#42524 — OTP: fix click-to-focus and overwrite-on-retype](https://github.com/twbs/bootstrap/pull/42524)

## Category
Complex widget interaction

## What Happened
This is the direct sequel to [#42500](bootstrap-pr42500.md), and it exists because that PR was merged unreviewed. The single-input OTP rewrite merged with two interaction defects that, in the author's own words, were "reported after merge": clicking a slot did not focus it (the slots carried `pointer-events: none` and focus always jumped to the end of the value), and retyping a digit shifted the remaining digits along, because a native `<input>` inserts rather than overwrites. This PR reworked the interaction model to map the active slot to a selection range and intercept single-character input, while keeping the single accessible `<input>` that #42500 introduced. Both interaction fixes are covered by new unit tests added in the PR's final commit.

The fix then introduced a defect of its own. An outside contributor (coliff) tested the deploy preview on iPadOS 26 and iPadOS 27 Developer Beta and found that tapping the field raised the on-screen keyboard and dismissed it within a split second — a functional lockout on touch devices, in a component whose stated purpose was accessibility. The cause, as the author explained in the thread, was that the decorative slots overlaid the real input with `pointer-events: none`, so the component called `input.focus()` programmatically after calling `preventDefault()` on the tap; iOS will only raise the on-screen keyboard in response to a genuine, un-prevented gesture on the input itself. The author pushed a fix restoring `pointer-events: auto`, asked the reporter to re-test because he had no iPadOS device, and the reporter confirmed the following day that it worked.

## Timeline
- Parent PR #42500 merged (unreviewed, in 13h 35m): 2026-06-11
- PR opened: 2026-06-18
- Regression on iPadOS 26/27 reported by an outside contributor: 2026-06-24
- Author pushed a fix and requested re-testing on hardware he lacked: 2026-06-28
- Reporter confirmed the fix on both iPadOS versions: 2026-06-29
- PR merged: 2026-07-04
- Days open: 16

## Rubric Scores

| Criterion | Score (0–2) | Justification |
| --- | --- | --- |
| User impact stated | 1 | Both original defects are described precisely at the level of task ("you couldn't click a slot to focus it", "retyping a digit shifted the others along"), and the iPadOS regression is described in terms of observable behaviour. No affected population is ever named — not touch users, not keyboard users, not screen-reader users. Tasks are stated; users are left implicit. |
| WCAG mapping | 0 | No success criterion is cited anywhere in the PR body or the thread. Notable given that the parent PR #42500 anchored four (3.3.8, 1.3.5, 2.2.1, 3.3.7) — the follow-up fixing that PR's defects cites none. |
| Verification evidence | 2 | The strongest verification evidence in the corpus. An outside contributor names the platform and versions (iPadOS 26 and 27 Developer Beta), names comparison platforms where behaviour was correct (Edge and Firefox on Windows 11), describes precisely what was observed, and re-verifies after the fix — all before merge. It is device rather than assistive-technology verification; see the scoring note. |
| Reviewer confidence signal | 1 | Substantive pre-merge engagement did occur and it changed the code — an outside contributor found a release-blocking regression, the author diagnosed it publicly and pushed a fix, and the reporter re-verified. But no formal review was submitted; the requested code-owner team review never arrived; and the author merged his own change. |
| Direct language | 1 | Highly specific about platforms, versions and mechanisms (`pointer-events`, `preventDefault()`, `beforeinput`, caret ranges). Never specific about people — no affected user group is named at any point. |
| Outcome clarity | 2 | The record is fully legible. A future contributor can reconstruct what broke, why, who found it, how it was diagnosed, what changed and who confirmed the fix, without inference. One blemish: a second reported defect (`placeholder` not applying to slots) was still under discussion when the PR merged, and the decision to leave placeholder support out was stated after the merge, after which the reporter supplied counter-evidence from Laravel's starter kit and CoreUI. |
| **Total** | **7/12** | |

## Review Pattern Observed
The only case in the corpus where substantive pre-merge review actually happened and caught a defect before release — but it came from a non-code-owner community contributor in the comment thread rather than from the code-owner team whose review was formally requested and never delivered, and the author still self-merged. Substantively reviewed; procedurally identical to the unreviewed cases.

## Infrastructure Gap Illustrated
This case contains, spontaneously, the intervention this repository recommends. Faced with a defect he could not verify, the author wrote in the thread: *"Could you re-test on iPadOS 26/27 (Developer Beta) once the preview rebuilds? I don't have a device to confirm the keyboard now stays up."* That is precisely the "not yet — requesting a reviewer with device or AT access to verify before merge" state that the accessibility PR template makes an explicit, required field. It worked: the request was answered within a day and the regression was confirmed fixed before merge.

The gap is that nothing made it happen. It depended on a maintainer thinking to ask, and on a contributor with the right hardware happening to be reading the thread. Nothing recorded the request as an outstanding verification obligation, nothing would have flagged its absence, and nothing prevents the next such PR merging without it — as the parent PR #42500 did, one week earlier, which is why this PR exists at all.

## Scoring Note — this case changed the rubric
As first drafted, this PR scored 6/12, the same total as #42500 and #42539, despite containing the best verification behaviour anywhere in the corpus. Criterion 3 was written around assistive technology specifically — which technology, which version, what was announced — and the verification here was device verification: real hardware, named OS versions, named comparison platforms, observed behaviour, independent re-test after the fix. Every structural property the criterion was trying to reward was present; the word "assistive" was not.

Scoring the behaviour we advocate identically to the behaviour we criticise is a defect in the rubric, not a finding about the project. Criterion 3 was therefore renamed *Verification evidence* and given explicit bands on 2026-07-29, with platform verification scored on the same scale. This case moves to 2 and a total of 7/12; [MUI #48572](mui-material-ui-pr48572.md) moves down from 2 to 1 under the same bands, because nine words naming an AT with no version and no observed result is weaker evidence than what an outside contributor supplied here. Feeds issue #11 (validate the review rubric) and the AT test matrix work in #13.

## Verification
Re-verified 2026-08-04 against the GitHub API. Merged commit `b6a3341` into `v6-dev` on **2026-07-04**, sixteen days after opening — the earlier "2026-06-29 or later, archived view shows relative dating only" is superseded by this exact figure. The verbatim quote in Infrastructure Gap Illustrated is confirmed word for word against the live page. The Laravel-starter-kit and CoreUI counter-evidence in the placeholder discussion is confirmed as written.

## Source
[github.com/twbs/bootstrap/pull/42524](https://github.com/twbs/bootstrap/pull/42524)
