# Case Study: MUI Material UI — PR #48572

## Repository
[mui/material-ui](https://github.com/mui/material-ui)

## PR
[#48572 — [autocomplete] Fix item removal when it receives focus from VoiceOver before using Backspace](https://github.com/mui/material-ui/pull/48572)

## Category
AT-specific behavior

## What Happened
In a multi-select Autocomplete, when focus on a selected chip arrived via VoiceOver navigation (rather than a native keyboard `focus` event), internal component state wasn't updated to track which chip was focused. VoiceOver also dispatches a second, synthetic `Backspace` event to the underlying `<input>` immediately after sending one to the focused chip. Together these two AT-specific behaviors caused pressing Backspace once to delete three chips instead of one: the intended chip, plus two more from the end of the list. The fix syncs focus state on `onFocus` and uses a ref to detect and suppress the duplicate synthetic Backspace.

## Timeline
- Linked issue #44936: filed the original bug report
- PR opened: 2026-05-26
- PR merged: 2026-06-01
- Days open: 6

## Rubric Scores

| Criterion | Score (0–2) | Justification |
| --- | --- | --- |
| User impact stated | 2 | PR body names VoiceOver explicitly and explains the exact mechanism (extra synthetic Backspace event) causing the wrong chips to be deleted. |
| WCAG mapping | 0 | No WCAG success criterion is cited anywhere in the PR or reviews — the bug is framed purely in terms of the AT-specific behavior, not a conformance criterion. |
| Verification evidence | 1 | The approving reviewer (mj12albert, a Member) wrote, in full: "Looks good, tested the fix with VO+Chrome/Safari". That names the AT and two browsers, but no version, no OS, and no description of what was observed — so it meets band 1, not band 2, under the criterion-3 bands. It remains the only case in the corpus where a second person re-tested with the named AT before approving. |
| Reviewer confidence signal | 2 | A human reviewer (mj12albert) engaged substantively — approved only after independently re-verifying the fix with the actual assistive technology involved, beyond the author's automated-test coverage. |
| Direct language | 2 | "VoiceOver," "VO+Chrome/Safari" — specific AT and browser combinations named throughout, not generic "accessibility" language. |
| Outcome clarity | 2 | The PR body explains precisely which half of the bug could not be unit-tested (the VoiceOver-dispatched second Backspace) and adds tests for the half that could; the reviewer's re-test comment closes the remaining gap. A future reader can see exactly what was and wasn't automatable. |
| **Total** | **9/12** | |

## Review Pattern Observed
A human reviewer independently re-tested the fix with the named assistive technology before approving — the only case in the corpus with a recorded AT verification step performed by someone other than the author. Note that the author still merged their own change: this is a self-merge like five of the other six, but the only one carrying a substantive approval from a second party first.

## Infrastructure Gap Illustrated
This is the closest thing in the corpus to a mature review process, and it still tops out at 9/12 — which is the finding. The verification that makes this case work exists as nine words in a free-text review comment. Nothing recorded the VoiceOver version or the OS, nothing captured what was actually observed, nothing required the check, and nothing would have noticed had it been skipped. Reproducing it depends entirely on the same reviewer being present next time.

A structured field — which AT, which version and OS, what was observed — would have turned the same reviewer's same work into evidence a third party could act on. It also has no WCAG citation at all, showing that AT-testing rigour and WCAG-mapping rigour are independent of each other: this case has the best verification and no standards mapping, while [VS Code #324192](vscode-pr324192.md) has the best standards mapping and thin verification.

## Verification
Re-verified 2026-07-29 against the live PR page. Changes:

- **Score reduced from 10/12 to 9/12.** Verification evidence dropped from 2 to 1 under the criterion-3 bands added to the rubric the same day: the review comment names an AT and two browsers but gives no version, no OS and no observed result. The previous 2 was inconsistent with the 1 awarded to weaker-but-comparable evidence elsewhere in the corpus.
- **Corrected an overstatement.** The author did not say the bug was impossible to cover with automated tests; he said the second half was — VoiceOver's synthetic Backspace — and did add tests for the focused-item sync.
- **Self-merge confirmed.** silviuaavram merged their own PR into `mui:master`, making this the sixth of six merged PRs in the corpus to be self-merged.
- **Review requests noted.** Reviews were requested from two named individuals plus Copilot, rather than from a code-owner team. One of the two named humans delivered. Across the rest of the corpus, five code-owner *team* requests produced nothing. Copilot reviewed three separate times, generating two, four and one comments — so automated review here examined the mechanism while a human verified the outcome, the opposite of [Storybook #35321](storybook-pr35321.md).

## Source
[github.com/mui/material-ui/pull/48572](https://github.com/mui/material-ui/pull/48572)
