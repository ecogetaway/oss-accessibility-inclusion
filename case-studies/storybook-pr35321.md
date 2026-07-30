# Case Study: Storybook — PR #35321

## Repository
[storybookjs/storybook](https://github.com/storybookjs/storybook)

## PR
[#35321 — A11y: Handle lang attribute throughout preview](https://github.com/storybookjs/storybook/pull/35321)

## Category
Accessibility × i18n intersection

## What Happened
Storybook always rendered `<html lang="en">` regardless of the actual language of the story or docs content being previewed, first reported in issue #11706 by someone testing multilingual sites. For screen-reader users, an incorrect `lang` attribute means the AT selects the wrong pronunciation/voice profile for the content being read — an accessibility failure that is specifically about internationalization (wrong language announced), not just missing markup. The PR adds `htmlLang` and `docs.lang` (BCP-47) parameters and threads them through story rendering, docs blocks, and the args table so both Storybook's own UI chrome (fixed to English) and user content (configurable) get the correct `lang` attribute.

## Timeline
- Linked issue #11706: feature request, filed by a non-a11y-specialist contributor testing multilingual sites
- PR opened: 2026-06-29
- PR merged: 2026-06-30
- Days open: 1
- Authored and merged by the same person (Sidnioulz), who holds write access; shipped in the 10.5.0 release line

## Rubric Scores

| Criterion | Score (0–2) | Justification |
| --- | --- | --- |
| User impact stated | 1 | The PR body states the goal ("ensure the whole tree is declaring the right language for screen readers") but the originating issue (#11706) frames the problem as a testing/tooling need, not explicitly in terms of screen-reader users. |
| WCAG mapping | 0 | No WCAG success criterion (e.g. 3.1.1 Language of Page, 3.1.2 Language of Parts) is cited anywhere in the PR, issue, or reviews, despite this being a direct fit. |
| AT testing evidence | 0 | The author's own manual-testing checklist item reads "Run your favourite screenreader and observe how it handles languages" — phrased as a suggestion for the reviewer, with no evidence it, or any AT session, was actually performed and recorded by anyone. |
| Reviewer confidence signal | 1 | One automated reviewer (CodeRabbit) left 9 of the PR's 12 inline comments, and they were substantive: blank `docs.lang` values rendering as `lang=""` instead of inheriting the project setting; project annotations not threaded into title and subtitle resolution; an `lang="en"` override wrongly covering caller-supplied content in the same ActionBar; `docsLang` dropping on grouped ArgRows. That is real engagement with whether the mechanism works. What no comment addressed — bot or human — is whether AT announces the right language afterwards. The single human review (ndelangen) was an approval with an empty body, and the author merged their own change. |
| Direct language | 1 | "Screen readers" appears once in the PR body, but the bulk of the discussion (both human and bot) is about code structure, not the affected users or their experience. |
| Outcome clarity | 1 | The mechanism (lang propagation through the render tree) is clearly documented in code and PR description, but whether the fix actually improves screen-reader pronunciation was never confirmed by anyone in the thread. |
| **Total** | **4/12** | |

## Review Pattern Observed
Substantive automated review of the mechanism; no verification of the outcome. An AI reviewer caught four real defects in how the language value propagates. A single human approval carried no comment body. The author, who holds write access, merged their own change and then applied the `qa:success` label to it themselves. "The code was reviewed" and "the accessibility claim was verified" are two different things here, and only the first happened.

## Infrastructure Gap Illustrated
This case shows that code review is not accessibility verification. An automated reviewer can examine the mechanism carefully — and did — while the claim that actually matters, that AT will now announce the right language, goes unchecked, because verifying it requires rendering the page and listening rather than reading a diff. A required "AT verified: yes/no, which AT, which version and browser, what was observed" field, distinct from general code review, would have surfaced that gap before merge.

Note also that this is the third case in the sample where the merging maintainer was also the author — see Pattern 2 in [`signals/review-patterns-v0.2.md`](../signals/review-patterns-v0.2.md).

## Verification
Re-verified twice. Against the GitHub API on 2026-07-27: an earlier version described two AI reviewers and characterised the bot comments as concerning only import conventions and test-file placement; both were inaccurate and were corrected.

Re-verified again against the live PR page on 2026-07-29, which showed the corrected version was still not exact. Score unchanged at 4/12. Findings:

- **Comment counts.** The page's conversation counter reads 17. CodeRabbit posted three separate reviews, with seven, one and one actionable comments respectively, plus five nitpicks. The figure "9 of 12 inline comments" conflated actionable comments with a total; the defensible statement is that a single automated reviewer posted nine actionable comments across three reviews and found four genuine defects in how the language value propagates.
- **"Ahead of a feature freeze" is unsourced.** It appears nowhere on the PR page and has been removed pending a source.
- **"Maintainer" overstated.** The author's badge reads Contributor, not Member. They self-assign, apply labels, move project-board cards and merge — so they hold write access — but the page contradicts the word "maintainer" on its face.
- **Code-owner reviews were requested from two people** (jonniebigodes, kylegach) and neither reviewed. The lone approval came from a third person and carried no comment body.
- **The author self-certified QA**, flipping `qa:needed` to `qa:success` on their own merged change. This is the cleanest single illustration in the corpus of a process with no independent checkpoint.
- **It shipped.** Merged to `next`, referenced by the 10.5.0-alpha.10 prerelease and consumed downstream at storybook 10.5.0 — unlike all three Bootstrap cases.

## Source
[github.com/storybookjs/storybook/pull/35321](https://github.com/storybookjs/storybook/pull/35321)
