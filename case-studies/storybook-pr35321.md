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
- Authored and merged by the same maintainer (Sidnioulz), ahead of a stated feature freeze

## Rubric Scores

| Criterion | Score (0–2) | Justification |
| --- | --- | --- |
| User impact stated | 1 | The PR body states the goal ("ensure the whole tree is declaring the right language for screen readers") but the originating issue (#11706) frames the problem as a testing/tooling need, not explicitly in terms of screen-reader users. |
| WCAG mapping | 0 | No WCAG success criterion (e.g. 3.1.1 Language of Page, 3.1.2 Language of Parts) is cited anywhere in the PR, issue, or reviews, despite this being a direct fit. |
| AT testing evidence | 0 | The author's own manual-testing checklist item reads "Run your favourite screenreader and observe how it handles languages" — phrased as a suggestion for the reviewer, with no evidence it, or any AT session, was actually performed and recorded by anyone. |
| Reviewer confidence signal | 1 | One automated reviewer (CodeRabbit) left 9 of the PR's 12 inline comments, and they were substantive: blank `docs.lang` values rendering as `lang=""` instead of inheriting the project setting; project annotations not threaded into title and subtitle resolution; an `lang="en"` override wrongly covering caller-supplied content in the same ActionBar; `docsLang` dropping on grouped ArgRows. That is real engagement with whether the mechanism works. What no comment addressed — bot or human — is whether AT announces the right language afterwards. The single human review (ndelangen) was an approval with an empty body, and the author merged his own change. |
| Direct language | 1 | "Screen readers" appears once in the PR body, but the bulk of the discussion (both human and bot) is about code structure, not the affected users or their experience. |
| Outcome clarity | 1 | The mechanism (lang propagation through the render tree) is clearly documented in code and PR description, but whether the fix actually improves screen-reader pronunciation was never confirmed by anyone in the thread. |
| **Total** | **4/12** | |

## Review Pattern Observed
Substantive automated review of the mechanism; no verification of the outcome. An AI reviewer caught four real defects in how the language value propagates. A single human approval carried no comment body. The author, a maintainer, merged his own change ahead of a feature freeze. "The code was reviewed" and "the accessibility claim was verified" are two different things here, and only the first happened.

## Infrastructure Gap Illustrated
This case shows that code review is not accessibility verification. An automated reviewer can examine the mechanism carefully — and did — while the claim that actually matters, that AT will now announce the right language, goes unchecked, because verifying it requires rendering the page and listening rather than reading a diff. A required "AT verified: yes/no, which AT, which version and browser, what was observed" field, distinct from general code review, would have surfaced that gap before merge.

Note also that this is the third case in the sample where the merging maintainer was also the author — see Pattern 2 in [`signals/review-patterns-v0.1.md`](../signals/review-patterns-v0.1.md).

## Verification
Comment counts, reviewer identities and merge details re-verified against the GitHub API on 2026-07-27. An earlier version of this case study described two AI reviewers and characterised the bot comments as concerning only import conventions and test-file placement; both were inaccurate and have been corrected. The score is unchanged.

## Source
[github.com/storybookjs/storybook/pull/35321](https://github.com/storybookjs/storybook/pull/35321)
