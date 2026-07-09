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
| AT testing evidence | 2 | The approving reviewer wrote "Looks good, tested the fix with VO+Chrome/Safari" — a specific AT (VoiceOver), specific browsers, and confirmation the reviewer personally re-tested it, not just read the code. |
| Reviewer confidence signal | 2 | A human reviewer (mj12albert) engaged substantively — approved only after independently re-verifying the fix with the actual assistive technology involved, beyond the author's automated-test coverage. |
| Direct language | 2 | "VoiceOver," "VO+Chrome/Safari" — specific AT and browser combinations named throughout, not generic "accessibility" language. |
| Outcome clarity | 2 | The PR body explains why unit tests can't cover the synthetic-event case ("impossible to unit test"), and the reviewer's AT re-test comment closes that gap — a future reader can see exactly what was and wasn't automatable. |
| **Total** | **10/12** | |

## Review Pattern Observed
A human reviewer independently re-tested the fix with the named assistive technology before approving — the one case among these five with a recorded, named AT verification step performed by someone other than the author.

## Infrastructure Gap Illustrated
This is close to what "an a11y-mature review process" looks like by this rubric — the remaining gap is that the AT verification lives in a one-line, unstructured review comment rather than a structured field (which AT, which OS/browser, what was checked) that could be queried or required by a template. It also has no WCAG citation, showing that AT-testing rigor and WCAG-mapping rigor can be present independently of each other.

## Source
[github.com/mui/material-ui/pull/48572](https://github.com/mui/material-ui/pull/48572)
