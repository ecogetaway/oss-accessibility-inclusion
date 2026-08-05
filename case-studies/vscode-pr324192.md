# Case Study: VS Code — PR #324192

## Repository
[microsoft/vscode](https://github.com/microsoft/vscode)

## PR
[#324192 — a11y: Update warning icon colors in 2026 Light theme](https://github.com/microsoft/vscode/pull/324192)

## Category
Contrast / theming

## What Happened
The "Autopilot (Preview)" label and other warning/info text in the Copilot permission-picker combo box failed the WCAG 1.4.3 minimum contrast ratio (4.5:1) against its background in the 2026 Light theme, making it hard to read for users with low vision or reduced contrast sensitivity. The issue was filed through a formal accessibility testing programme — tagged `#A11yTCS`, `#A11ySev3`, `#WCAG1.4.3`, on a structured template with repro steps, actual/expected results, full environment details, and a colour-contrast-analyzer screenshot measuring the failure at 2.991:1 — rather than as a community bug report. The fix darkened the warning icon's foreground colour to roughly 6:1 and removed a CSS opacity reduction that had been lowering effective contrast further.

The interesting part of this case is not the fix. It is what happened to the process control the issue carried.

## Timeline
- Issue #321431 filed by an accessibility tester (kapilvaishna): 2026-06-15
- Triaged, assigned and labelled `accessibility-sla` the same day
- PR opened, auto-merge enabled by the author before review, and self-merged: 2026-07-03 (opened and merged the same day; PR carries milestone 1.128.0)
- Issue closed as completed by a collaborator (meganrogge), asking the PR author "should this be closed?": 2026-07-03
- `verified` label applied by a different contributor (jruales) with the comment "Looks good now" and a contrast-measurement screenshot: ~2026-07-24, roughly three weeks *after* closure

## Rubric Scores

| Criterion | Score (0–2) | Justification |
| --- | --- | --- |
| User impact stated | 2 | The issue states plainly: "Users with low vision or impaired contrast sensitivity cannot read the text," with repro steps, expected/actual results, and a measured pre-fix ratio of 2.991:1 attached as a screenshot — the most quantified intake report in the corpus. |
| WCAG mapping | 2 | Filed with an explicit `#WCAG1.4.3` tag and the 4.5:1 target ratio stated twice, in the filer's own words. The PR body itself cites neither; the mapping is entirely upstream. |
| Verification evidence | 1 | A measured contrast ratio does exist in this record — the comment carrying the `verified` label includes a screenshot reading 4.76 against the required 4.5. It is the only measured verification value anywhere in the corpus. It does not reach band 2 because it was posted roughly three weeks after the merge-linked closure: real evidence that arrived too late to inform the decision it nominally verifies. Nobody recorded a measurement before or at merge. |
| Reviewer confidence signal | 0 | The author self-assigned, enabled auto-merge (squash) *before* any review, and merged their own PR. The automated Copilot review generated no inline comments — only a plain-language summary of the diff, which does state the new value's approximate contrast ratio, but that is a calculation from the changed hex codes, not a human or AT verification. The single human approval (aeschli) has an empty body. |
| Direct language | 2 | The issue names the affected group precisely: "Users with low vision or impaired contrast sensitivity." |
| Outcome clarity | 1 | The chain from issue to fix is traceable, but the outcome is muddled: the issue carried an explicit instruction that only the accessibility tester could close it after verification, and it was closed as completed by someone else, on the same day as the merge, before any human verification existed on the record. |
| **Total** | **8/12** | |

## Review Pattern Observed
Rigour at intake, none at review, and a documented process control that was bypassed. The issue is the best-specified artifact in the corpus — tagged criterion, stated and measured ratio, named affected population, structured environment data, SLA label. The PR that answers it was self-assigned, auto-merged before review, approved with an empty body, and merged by its own author. Verification arrived roughly three weeks after closure, from a third party, as a one-line comment and a screenshot.

## Infrastructure Gap Illustrated
This case originally read as the corpus exemplar, and re-verification inverted it. The issue body carries an explicit closure rule:

> Please do not close this bug. This bug should only be closed by TCS, C+AI Accessibility tester after bug verification.

That rule was not followed. A collaborator who had triaged the issue asked the PR author whether it should be closed, then closed it as completed the same day the PR merged. The `verified` label came roughly three weeks later from someone else, this time with a measured contrast ratio attached — but by then the decision it verified had already been made and shipped.

The gap this illustrates is precise and generalisable: **a rule written as prose in an issue body is still a value, not a gate.** Nothing in the platform prevented the wrong person from closing it, nothing surfaced the rule at the moment of closure, and nothing flagged that verification had not yet happened. The best-instrumented accessibility process in this corpus had its one decisive control bypassed within weeks, by people acting in good faith who were probably clearing a milestone.

The transferable lesson is not "adopt a closure rule." It is that a control has to be enforced by the system rather than stated in the text, or it will be honoured only when nobody is busy — and even when verification does eventually happen, evidence that arrives after the decision cannot make the decision safer.

## Verification
Re-verified 2026-07-29 and again 2026-08-04 against the live PR and issue pages. Findings:

- **Score reduced from 11/12 to 8/12 on 2026-07-29.** The original scoring credited the upstream process for criteria it did not actually evidence in the record.
- **Verification evidence reduced from 2 to 1 on 2026-07-29**, applying the criterion-3 bands added that day. Re-examined 2026-08-04: the earlier text stated no measured ratio was ever recorded by any human. That was wrong — jruales's comment does include a measured value (4.76). The justification is corrected here; the score is unchanged, because that measurement postdates the merge and the closure by roughly three weeks and could not have informed either.
- **Reviewer confidence reduced from 1 to 0 on 2026-07-29.** An empty-bodied approval was scored 0 for Storybook #35321; the identical evidence here was scored 1. The inconsistency was ours.
- **Outcome clarity reduced from 2 to 1** on discovery that the closure rule was violated.
- **Timeline date corrected, 2026-08-04.** An earlier revision recorded the PR as opened "late June 2026 (exact date not pinned)" and separately noted that a prior "2026-07-03" figure "was wrong and is now recorded as approximate pending an API check." That 2026-07-03 figure was in fact correct: the PR page shows it opened, reviewed, approved, merged and branch-deleted, all on 3 July 2026. Restored throughout.
- **Both image attachments opened, 2026-08-04**, closing the last unexamined source in the corpus. Kapilvaishna's original report carries an Accessibility Insights for Windows screenshot measuring `#BF8803` on `#FAFAFD` at 2.991:1, Fail. Jruales's "Looks good now" comment carries a second screenshot, a contrast overlay on `span.agent-host-chat-input-picker-label` reading 4.76 with a pass indicator. Reflected in criteria 1 and 3 above.
- Also corrected: the earlier write-up described "Microsoft's internal accessibility QA function." The tags identify a TCS accessibility testing programme — a vendor arrangement — which is a meaningfully different thing for other projects to reason about.

## Source
[github.com/microsoft/vscode/pull/324192](https://github.com/microsoft/vscode/pull/324192) · [issue #321431](https://github.com/microsoft/vscode/issues/321431)
