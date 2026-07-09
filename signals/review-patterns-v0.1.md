# Signals v0.1 — Patterns Across the First Six Case Studies

Synthesized from six case studies scored against [`review-rubric.md`](../review-rubric.md). Five were added in v0.1 (all merged, all fast); a sixth — a stalled, closed-unmerged PR — was added in v0.2 specifically to test the open question v0.1 raised (see below).

## Scores at a glance

| Case study | Category | Score |
| --- | --- | --- |
| [VS Code #324192](../case-studies/vscode-pr324192.md) | Contrast / theming | 11/12 |
| [MUI #48572](../case-studies/mui-material-ui-pr48572.md) | AT-specific behavior | 10/12 |
| [Bootstrap #42539](../case-studies/bootstrap-pr42539.md) | Semantics / reading order | 6/12 |
| [Bootstrap #42500](../case-studies/bootstrap-pr42500.md) | Complex widget interaction | 6/12 |
| [Bootstrap #41607](../case-studies/bootstrap-pr41607.md) | Complex widget interaction (stalled) | 4/12 |
| [Storybook #35321](../case-studies/storybook-pr35321.md) | Accessibility × i18n intersection | 4/12 |

## Pattern 1 — AT-testing evidence is the criterion that separates high and low scores, not WCAG citation

The two highest-scoring cases (VS Code, MUI) both had a named person or process actually verify the fix against real assistive technology (VoiceOver, or a dedicated accessibility-test role) before merge. The two Bootstrap cases had strong written reasoning — one even cited four WCAG success criteria — but no recorded AT verification, and scored the same as a result. WCAG mapping alone does not predict review quality; independently confirmed AT testing does.

## Pattern 2 — Self-merge by a maintainer with commit rights is the default failure mode, not adversarial rejection

Neither Bootstrap PR received a single review comment. Both were opened and merged by the same maintainer, same day. This isn't a story about hostile or careless maintainers — the written justifications were good — it's that nothing in the process required a second party to weigh in before an accessibility change shipped. That absence is invisible unless you go looking for it, because the PR still reads as well-documented.

## Pattern 3 — Automated review volume is not a substitute for accessibility review

The Storybook PR had by far the most review activity of the five — two different AI bots left dozens of comments — none of which touched the actual accessibility claim (correct language announcement for screen readers). All of it was about import conventions and test-file placement. A PR can look heavily reviewed while the one claim that matters for this repo's scope goes completely unverified.

## Pattern 4 — Structured, tagged issue intake produces the best-reviewed PRs

The VS Code case is the outlier specifically because the issue that fed it wasn't a community bug report — it came from a named internal accessibility-testing role, tagged with the exact WCAG criterion and a rule that only a verified tester could close it. The PR review itself was almost a formality; the rigor happened at issue-filing time. This suggests the highest-leverage intervention for other projects isn't a better PR template, but a better *issue* template that captures WCAG mapping and AT evidence before a PR ever opens.

## Pattern 5 — the "fast review" pattern in v0.1 was a sampling artifact, not a real difference from i18n

The open question in the original v0.1 draft of this document was whether accessibility PRs are reviewed faster than the stalled, silently-closed i18n PRs documented in the companion repo — every v0.1 case study merged same-day or same-week. [Bootstrap #41607](../case-studies/bootstrap-pr41607.md), added to test this, shows the same silent-stall pattern the i18n case studies show: eleven months with zero review, then a closing comment that never evaluates the fix on its merits. The five fast-merging PRs in this sample weren't representative — they were mostly maintainer self-merges of maintainer-authored PRs (Bootstrap #42539, #42500) or PRs that happened to get a specific reviewer's attention (MUI, VS Code). A community contributor's PR, on the same category of bug, in the same repository, waited nearly a year for any response at all. **Whether a PR gets reviewed at all appears to depend more on who opened it — maintainer vs. outside contributor — than on the accessibility domain itself.**

## Open questions for v0.3

- Is the maintainer-vs-contributor gap seen here (Bootstrap #42539/#42500 vs. #41607) consistent across other projects, or specific to how Bootstrap currently triages `accessibility`-labeled PRs?
- Bootstrap #41607 was closed for architectural reasons (v6's native `<dialog>` obsoleted the code), not because anyone judged the fix wrong. Worth sourcing a case where an a11y PR was closed after actual maintainer disagreement about the fix, to separate "never reviewed" from "reviewed and rejected."
