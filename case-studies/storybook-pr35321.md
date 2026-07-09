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

## Rubric Scores

| Criterion | Score (0–2) | Justification |
| --- | --- | --- |
| User impact stated | 1 | The PR body states the goal ("ensure the whole tree is declaring the right language for screen readers") but the originating issue (#11706) frames the problem as a testing/tooling need, not explicitly in terms of screen-reader users. |
| WCAG mapping | 0 | No WCAG success criterion (e.g. 3.1.1 Language of Page, 3.1.2 Language of Parts) is cited anywhere in the PR, issue, or reviews, despite this being a direct fit. |
| AT testing evidence | 0 | The author's own manual-testing checklist item reads "Run your favourite screenreader and observe how it handles languages" — phrased as a suggestion for the reviewer, with no evidence it, or any AT session, was actually performed and recorded by anyone. |
| Reviewer confidence signal | 1 | Two AI review bots (CodeRabbit, Copilot) left extensive comments — but exclusively about import conventions, test-file placement, and a real functional bug (docsLang not forwarded to grouped ArgRows). One human maintainer (ndelangen) approved with no comment body; no reviewer engaged with the accessibility/language-announcement claim itself. |
| Direct language | 1 | "Screen readers" appears once in the PR body, but the bulk of the discussion (both human and bot) is about code structure, not the affected users or their experience. |
| Outcome clarity | 1 | The mechanism (lang propagation through the render tree) is clearly documented in code and PR description, but whether the fix actually improves screen-reader pronunciation was never confirmed by anyone in the thread. |
| **Total** | **4/12** | |

## Review Pattern Observed
Heavy automated review activity (two different AI bots, dozens of comments) entirely focused on code-quality conventions, alongside a single no-comment human approval — a case where "the PR was reviewed a lot" and "the accessibility claim was reviewed" are two different things.

## Infrastructure Gap Illustrated
This case shows that review *volume* is not a proxy for a11y review *substance*. A PR can accumulate extensive automated scrutiny on style and correctness while the actual accessibility claim — that AT will now announce the right language — goes completely unverified. A required "AT verified: yes/no, which one, what was observed" field, distinct from general code review, would have surfaced that gap before merge.

## Source
[github.com/storybookjs/storybook/pull/35321](https://github.com/storybookjs/storybook/pull/35321)
