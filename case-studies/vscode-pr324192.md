# Case Study: VS Code — PR #324192

## Repository
[microsoft/vscode](https://github.com/microsoft/vscode)

## PR
[#324192 — a11y: Update warning icon colors in 2026 Light theme](https://github.com/microsoft/vscode/pull/324192)

## Category
Contrast / theming

## What Happened
The "Autopilot (Preview)" label and other warning/info text in the Copilot permission-picker combo box failed the WCAG 1.4.3 minimum contrast ratio (4.5:1) against its background in the 2026 Light theme, making it hard to read for users with low vision or reduced contrast sensitivity. The issue was filed through a formal accessibility testing programme — tagged `#A11yTCS`, `#A11ySev3`, `#WCAG1.4.3`, on a structured template with repro steps, actual/expected results and full environment details — rather than as a community bug report. The fix darkened the warning icon's foreground colour to roughly 6:1 and removed a CSS opacity reduction that had been lowering effective contrast further.

The interesting part of this case is not the fix. It is what happened to the process control the issue carried.

## Timeline
- Issue #321431 filed by an accessibility tester (kapilvaishna): 2026-06-15
- Triaged, assigned and labelled `accessibility-sla` the same day
- PR opened, auto-merge enabled by the author before review, and self-merged: late June 2026 (exact date not pinned; PR carries milestone 1.128.0)
- Issue closed as completed by a collaborator (meganrogge), asking the PR author "should this be closed?": ~2026-07-08
- `verified` label applied by a different contributor (jruales) with the comment "Looks good now": ~2026-07-15, one week *after* closure

## Rubric Scores

| Criterion | Score (0–2) | Justification |
| --- | --- | --- |
| User impact stated | 2 | The issue states plainly: "Users with low vision or impaired contrast sensitivity cannot read the text," with repro steps and expected/actual results. |
| WCAG mapping | 2 | Filed with an explicit `#WCAG1.4.3` tag and the 4.5:1 target ratio stated twice, in the filer's own words. The PR body itself cites neither; the mapping is entirely upstream. |
| Verification evidence | 1 | The issue recommends a contrast checker and gives precise environment details, but no measured ratio is ever recorded by a verifier. The only verification in the record is the comment "Looks good now," applied with the `verified` label a week after the issue was already closed. |
| Reviewer confidence signal | 0 | The author self-assigned, enabled auto-merge (squash) *before* any review, and merged their own PR. The automated Copilot review generated no comments. The single human approval (aeschli) has an empty body. Nothing in the thread engages with the contrast claim. |
| Direct language | 2 | The issue names the affected group precisely: "Users with low vision or impaired contrast sensitivity." |
| Outcome clarity | 1 | The chain from issue to fix is traceable, but the outcome is muddled: the issue carried an explicit instruction that only the accessibility tester could close it after verification, and it was closed as completed by someone else, before verification, on the basis of a question rather than a check. |
| **Total** | **8/12** | |

## Review Pattern Observed
Rigour at intake, none at review, and a documented process control that was bypassed. The issue is the best-specified artifact in the corpus — tagged criterion, stated ratio, named affected population, structured environment data, SLA label. The PR that answers it was self-assigned, auto-merged before review, approved with an empty body, and merged by its own author. Verification arrived a week after closure, from a third party, as three words.

## Infrastructure Gap Illustrated
This case originally read as the corpus exemplar, and re-verification inverted it. The issue body carries an explicit closure rule:

> Please do not close this bug. This bug should only be closed by TCS, C+AI Accessibility tester after bug verification.

That rule was not followed. A collaborator who had triaged the issue asked the PR author whether it should be closed, then closed it as completed. The `verified` label came a week later from someone else, with no measured ratio attached.

The gap this illustrates is precise and generalisable: **a rule written as prose in an issue body is still a value, not a gate.** Nothing in the platform prevented the wrong person from closing it, nothing surfaced the rule at the moment of closure, and nothing flagged that verification had not yet happened. The best-instrumented accessibility process in this corpus had its one decisive control bypassed within weeks, by people acting in good faith who were probably clearing a milestone.

The transferable lesson is not "adopt a closure rule." It is that a control has to be enforced by the system rather than stated in the text, or it will be honoured only when nobody is busy.

## Verification
Re-verified 2026-07-29 against the live PR and issue pages. Three findings changed:

- **Score reduced from 11/12 to 8/12.** The original scoring credited the upstream process for criteria it did not actually evidence in the record.
- **Verification evidence reduced from 2 to 1**, applying the criterion-3 bands added to the rubric on 2026-07-29. The original justification treated the *existence* of a testing programme as verification evidence; the rubric asks for a recorded observation, and "Looks good now" with no measured ratio does not meet the top band.
- **Reviewer confidence reduced from 1 to 0.** An empty-bodied approval was scored 0 for Storybook #35321; the identical evidence here was scored 1. The inconsistency was ours.
- **Outcome clarity reduced from 2 to 1** on discovery that the closure rule was violated.

Also corrected: the earlier write-up described "Microsoft's internal accessibility QA function." The tags identify a TCS accessibility testing programme — a vendor arrangement — which is a meaningfully different thing for other projects to reason about. PR open/merge dates in the earlier version (2026-07-03) were wrong and are now recorded as approximate pending an API check.

## Source
[github.com/microsoft/vscode/pull/324192](https://github.com/microsoft/vscode/pull/324192) · [issue #321431](https://github.com/microsoft/vscode/issues/321431)
