# Signals v0.2 — Patterns Across Seven Case Studies

Synthesized from seven case studies scored against [`review-rubric.md`](../review-rubric.md). Supersedes v0.1, which covered six. Every case was re-verified against its live GitHub page on 2026-07-29 (four scores changed and one pattern was inverted outright), and again on 2026-08-04 against the GitHub API and every diff, which changed one further score and corrected two patterns. What changed and why is recorded in each case study's Verification section.

## Scores at a glance

| Case study | Category | Score |
| --- | --- | --- |
| [MUI #48572](../case-studies/mui-material-ui-pr48572.md) | AT-specific behavior | 9/12 |
| [VS Code #324192](../case-studies/vscode-pr324192.md) | Contrast / theming | 8/12 |
| [Bootstrap #42500](../case-studies/bootstrap-pr42500.md) | Complex widget interaction | 7/12 |
| [Bootstrap #42524](../case-studies/bootstrap-pr42524.md) | Complex widget interaction (follow-up defect) | 7/12 |
| [Bootstrap #42539](../case-studies/bootstrap-pr42539.md) | Semantics / reading order | 6/12 |
| [Bootstrap #41607](../case-studies/bootstrap-pr41607.md) | Complex widget interaction (stalled) | 4/12 |
| [Storybook #35321](../case-studies/storybook-pr35321.md) | Accessibility × i18n intersection | 4/12 |

The most important thing about this table is its ceiling. After re-verification, **no case in the corpus reaches the 10–12 band** the rubric describes as normal for an accessibility-mature project. The range is 4 to 9, across four of the best-resourced front-end projects in open source.

## Pattern 1 — Verification evidence separates the corpus; WCAG citation does not

The two cases with the most thorough standards work score 7 and 8. The case with no WCAG citation anywhere scores 9. What separates them is whether a second person confirmed the outcome against real assistive technology or a real device before merge.

The inversion is worth stating precisely, because it cuts against the standard advice to cite success criteria in accessibility PRs. Citing them is good practice — [Bootstrap #42500](../case-studies/bootstrap-pr42500.md) reasons about two criteria and anchors four in its docs, which is the best standards work in the corpus — but it tells you nothing about whether anyone checked the result. #42500 has zero verification evidence and merged with defects that surfaced within the week.

The corollary is bleaker than v0.1 recorded. Only one case in seven reaches the top band on this criterion, and it is [Bootstrap #42524](../case-studies/bootstrap-pr42524.md) — device verification, supplied by an outside contributor, on a PR nobody had scored at all until this revision. The single best piece of verification evidence in the corpus came from someone with no formal role in the review.

## Pattern 2 — Self-merge is not a tendency; it is the norm

**Six of the six merged PRs in this corpus were merged by their own author.** Bootstrap #42500, #42539 and #42524 by the same maintainer; MUI #48572 and VS Code #324192 by their sole authors; Storybook #35321 by one of its two co-authors.

Only one of those six carried a substantive approval from a second party first ([MUI #48572](../case-studies/mui-material-ui-pr48572.md)). Two carried an approval with an empty comment body. The remaining three — Bootstrap #42500, #42539 and #42524 — carried no formal review of any kind; the third of those drew substantive comment-thread engagement from an outside contributor who caught a release-blocking regression, but that engagement never took the form of a submitted review (see Pattern 1).

Two cases go further than self-merge into self-certification. Storybook's merging author applied the `qa:success` label to the change they'd just merged. VS Code's author enabled auto-merge before any review had happened, so the merge was authorised in advance of the approval it waited for.

This is not a story about careless maintainers — the written justifications are generally good. It is that nothing in any of these projects requires a second party before an accessibility change ships, and the absence is invisible because the PRs read as well-documented.

## Pattern 3 — Code review is not accessibility verification

[Storybook #35321](../case-studies/storybook-pr35321.md) drew the most review activity in the corpus. A single automated reviewer posted nine actionable comments across three separate reviews, plus five nitpicks. Those comments were not filler: they caught blank `docs.lang` values rendering as `lang=""` instead of inheriting the project setting, project annotations not threaded into title and subtitle resolution, an English override wrongly covering caller-supplied content, and `docsLang` dropping on grouped ArgRows. That is substantive review of whether the mechanism works.

What no comment did — bot or human — was establish what a screen reader announces afterwards. The single human review was an approval with an empty body, and the author's own testing checklist asked the reviewer to run a screen reader, with no evidence anyone did. Nor is the PR untested: it ships four automated test surfaces asserting the resulting `lang` attribute, all of them DOM checks in a headless environment with no assistive technology in it.

[MUI #48572](../case-studies/mui-material-ui-pr48572.md) is the control case that makes this legible. Automated review ran there too — three separate passes, this time from GitHub Copilot rather than CodeRabbit — and a human separately verified with VoiceOver. A different vendor's bot, the same shape of process, the opposite outcome. The variable is not whether a bot reviewed; it is whether anybody rendered the thing and checked.

## Pattern 4 — A control written as prose is not a gate

This pattern replaces v0.1's "structured intake produces the best-reviewed PRs," which re-verification falsified.

[VS Code #324192](../case-studies/vscode-pr324192.md) is fed by the best-specified issue in the corpus: filed by an accessibility testing programme on a structured template, tagged `#WCAG1.4.3`, stating the 4.5:1 requirement twice with a measured pre-fix ratio attached, naming the affected population, carrying full environment details and an `accessibility-sla` label. v0.1 credited it with the corpus's decisive process control — a rule, written in the issue body, that only the accessibility tester may close the bug after verification.

The rule is real. It was also broken. A collaborator asked the PR author "should this be closed?" and then closed it as completed the same day the PR merged. The `verified` label arrived roughly three weeks later, from a third person, attached to the comment "Looks good now" and a screenshot measuring 4.76 against the required 4.5 — the only measured verification value anywhere in the corpus, and one that arrived after the decision it nominally confirms. The process ran backwards: closed, then verified, by neither the named role nor in the stated order, with the eventual evidence too late to matter either way.

Structured intake still does real work — every criterion this case scores well on is inherited from the issue, and the PR itself cites nothing. But the lesson is narrower and harder than v0.1 claimed. **A rule expressed as text in an issue body is still a value, and values lose to milestone pressure. Only a control the platform enforces is a gate.** Nothing surfaced the rule at the moment of closure; nothing flagged that verification had not happened; nothing prevented the wrong person from acting; and nothing made the eventual verification arrive in time to count.

## Pattern 5 — Whether a PR is reviewed tracks who opened it

Six maintainer-authored PRs merged, five of them within 36 hours, none with more than one substantive external review between them. The one outside contributor's PR — [#41607](../case-studies/bootstrap-pr41607.md), a correct and tested fix for a keyboard focus-trap defect — waited about 341 days for any response, then was closed because an unreleased rewrite had made the code path obsolete. It was never evaluated on its merits.

Re-verification strengthened this in two ways. First, it was triaged correctly within hours: a maintainer applied both `js` and `accessibility` labels the day it opened, which rules out the defence that nobody noticed. Triage worked; review never happened. Second, four separate people engaged with the underlying defect — the reporter, an independent confirmer who bisected the regression to 5.3.7, the contributor who fixed it, and a fourth who added analysis six months later — while the only maintainer actions in eleven months were a label and a closure.

A labelling asymmetry runs alongside it. In the same repository, in the same period, the outside contributor's PR was labelled `accessibility` within hours, while none of the maintainer's own three accessibility PRs carries that label at all. Any audit of this project's accessibility work by label would find the contributor's rejected fix and miss all three that merged — none of which has itself reached a released version.

The asymmetry recurs beyond this one contributor, and in the opposite direction: the community discussion behind #42500 and the issue behind #42539 both carry the `accessibility` label, and neither resolving PR does. Taken together, the label tracks who is asking rather than what the change does — a report gets labelled correctly and its fix does not, in three out of three instances checked.

## Pattern 6 — Naming a person beats naming a team, but neither is reliable

Five of the six merged PRs formally requested a review; VS Code did not; its only review came from Copilot's automatic trigger.

Four of those five requests went to a **team** via CODEOWNERS, and all four were in Bootstrap — #42500, #42539, #42524, and the never-merged #41607. None produced a response. The fifth went to two **named individuals**, on Storybook — and neither of them responded either.

MUI is the one case that requested named individuals and got an answer: two people plus Copilot were asked, and one of the two humans delivered, including the only AT verification in the corpus.

Team requests are 0 for 4. Named-individual requests are 1 for 2 successful projects (MUI) and 0 for 2 in the other (Storybook) — a low hit rate either way, but the one success anywhere in the corpus came from naming a person rather than a team alias. That is not enough to call it a fix. It is enough to say a team alias has never once worked here, and asking a specific person has, at least once.

## Pattern 7 — Merging is not shipping

All four Bootstrap cases leave users of every released version with nothing. #42500, #42539 and #42524 merged only into the unreleased `v6-dev` branch; #41607 targeted `main` and was closed precisely because `v6-dev` supersedes it. The reporter of the floating-label defect filed against v5.3.3 and, roughly fourteen and a half months later (439 days, confirmed via the GitHub API), still has the bug — while the issue is closed as *completed*.

Storybook, MUI and VS Code all shipped. So the pattern is project-specific rather than universal, which is why it belongs here rather than in the headline findings. But it changes what "merged" means as an outcome measure, and it means a rubric that stops at the merge event overstates how many of these defects were actually fixed for anybody.

## Open questions for v0.3

- Is the maintainer-vs-contributor gap consistent across other projects, or specific to how Bootstrap currently triages accessibility PRs? Testing Pattern 5 against a non-Bootstrap project remains the highest-value next case.
- Pattern 6 now rests on four failed team requests and a three-instance split on named requests (1 success, 2 failures). Does requesting review from named individuals rather than a code-owner team measurably change response rates at larger sample sizes?
- Every case here was either never reviewed or reviewed without verification. Sourcing a case where an accessibility PR was reviewed and **rejected on the merits** would separate "never reviewed" from "reviewed and disagreed with," which the corpus currently cannot do.
- Should the rubric score whether a fix reached a released version, or is that outside the scope of review process? Pattern 7 suggests the merge event is a weaker outcome signal than assumed.

## Verification

All seven PRs and their linked issues re-verified against live GitHub pages on 2026-07-29, following an earlier API-based re-verification on 2026-07-27, and re-verified a third time on 2026-08-04 against the GitHub API and every PR's Files-changed and Commits tabs, plus every linked issue and discussion.

Score changes, 2026-07-29: VS Code #324192 from 11/12 to 8/12; MUI #48572 from 10/12 to 9/12; Bootstrap #42524 added at 7/12. Rubric change: criterion 3 was renamed *Verification evidence* and given explicit bands, after #42524 exposed that it scored device verification below weaker AT evidence.

Score changes, 2026-08-04: Bootstrap #42500 from 6/12 to 7/12, after the originating discussion was found to have been answered and the reporter's confirmation credited under Outcome clarity.

Pattern changes, 2026-07-29: Pattern 4 was inverted — the closure rule it credited turned out to have been bypassed. Pattern 2 was extended from three self-merges to six of six. Pattern 3's comment counts were restated (nine actionable comments across three automated reviews, not "9 of 12 inline"), and an unsourced claim that the Storybook PR merged ahead of a feature freeze was removed. Patterns 6 and 7 are new.

Pattern changes, 2026-08-04: Pattern 6 corrected — the CODEOWNERS team-request count was five including Storybook; it is four, all in Bootstrap, with Storybook's request going to two named individuals who did not respond. The pattern's conclusion is rewritten accordingly. Pattern 3's MUI comparison corrected from "same tooling" to two different vendors' bots (CodeRabbit on Storybook, Copilot on MUI). Pattern 5's labelling claim extended from one instance to three, and its maintainer-PR count corrected from two to three. Pattern 4's verification-evidence claim corrected: a measured contrast value does exist in the VS Code record, arriving roughly three weeks after merge — too late to inform the decision, not absent from it. Six instances of "shipped" describing a merge to an unreleased branch were corrected to "merged" throughout.

Corrected 2026-07-31: Pattern 7 said three Bootstrap cases; #42524 also merged into `v6-dev`, making it four. Confirmed via the GitHub API.
