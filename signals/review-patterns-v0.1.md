# Signals v0.1 — Patterns Across the First Five Case Studies

Synthesized from the five case studies scored against [`review-rubric.md`](../review-rubric.md).

## Scores at a glance

| Case study | Category | Score |
| --- | --- | --- |
| [VS Code #324192](../case-studies/vscode-pr324192.md) | Contrast / theming | 11/12 |
| [MUI #48572](../case-studies/mui-material-ui-pr48572.md) | AT-specific behavior | 10/12 |
| [Bootstrap #42539](../case-studies/bootstrap-pr42539.md) | Semantics / reading order | 6/12 |
| [Bootstrap #42500](../case-studies/bootstrap-pr42500.md) | Complex widget interaction | 6/12 |
| [Storybook #35321](../case-studies/storybook-pr35321.md) | Accessibility × i18n intersection | 4/12 |

## Pattern 1 — AT-testing evidence is the criterion that separates high and low scores, not WCAG citation

The two highest-scoring cases (VS Code, MUI) both had a named person or process actually verify the fix against real assistive technology (VoiceOver, or a dedicated accessibility-test role) before merge. The two Bootstrap cases had strong written reasoning — one even cited four WCAG success criteria — but no recorded AT verification, and scored the same as a result. WCAG mapping alone does not predict review quality; independently confirmed AT testing does.

## Pattern 2 — Self-merge by a maintainer with commit rights is the default failure mode, not adversarial rejection

Neither Bootstrap PR received a single review comment. Both were opened and merged by the same maintainer, same day. This isn't a story about hostile or careless maintainers — the written justifications were good — it's that nothing in the process required a second party to weigh in before an accessibility change shipped. That absence is invisible unless you go looking for it, because the PR still reads as well-documented.

## Pattern 3 — Automated review volume is not a substitute for accessibility review

The Storybook PR had by far the most review activity of the five — two different AI bots left dozens of comments — none of which touched the actual accessibility claim (correct language announcement for screen readers). All of it was about import conventions and test-file placement. A PR can look heavily reviewed while the one claim that matters for this repo's scope goes completely unverified.

## Pattern 4 — Structured, tagged issue intake produces the best-reviewed PRs

The VS Code case is the outlier specifically because the issue that fed it wasn't a community bug report — it came from a named internal accessibility-testing role, tagged with the exact WCAG criterion and a rule that only a verified tester could close it. The PR review itself was almost a formality; the rigor happened at issue-filing time. This suggests the highest-leverage intervention for other projects isn't a better PR template, but a better *issue* template that captures WCAG mapping and AT evidence before a PR ever opens.

## Open question for v0.2

All five 2026 PRs in this set were either merged same-day/same-week or (in Storybook's case) merged despite an unverified core claim — none stalled or were rejected. The companion i18n repo's case studies show the opposite pattern (long stalls, silent closes). Is accessibility work actually reviewed *faster* than i18n work in these projects, or does this sample simply not yet include a stalled/rejected a11y PR? Worth deliberately sourcing a stalled or closed-unmerged a11y PR for v0.2 to test this.
