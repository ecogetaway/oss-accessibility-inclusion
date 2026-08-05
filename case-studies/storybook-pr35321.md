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
- Two commits. The only substantive one, `520c701` ("UI: Add docs.lang and htmlLang parameters"), is attributed to mehm8128 as commit author with Sidnioulz as `Co-Authored-By`; the second, `383d590`, is a housekeeping merge of `next` into the feature branch, authored by Sidnioulz alone. Sidnioulz opened the PR from their branch (`sidnioulz/fix-html-lang-refreshed`), is co-credited on the substantive code, and merged the PR into `next` as `91b9c34`.
- Shipped in the 10.5.0 release line

## Rubric Scores

| Criterion | Score (0–2) | Justification |
| --- | --- | --- |
| User impact stated | 1 | The PR body states the goal ("ensure the whole tree is declaring the right language for screen readers") but the originating issue (#11706) frames the problem as a testing/tooling need, not explicitly in terms of screen-reader users. |
| WCAG mapping | 0 | No WCAG success criterion (e.g. 3.1.1 Language of Page, 3.1.2 Language of Parts) is cited anywhere in the PR, issue, or reviews, despite this being a direct fit. |
| AT testing evidence | 0 | The PR ships four automated test surfaces for the language mechanism: `ArgsTable.lang.test.tsx` (three assertions), `WebView.test.ts` (five assertions on `htmlLang` being applied to and removed from the story root), and play functions `InlineHtmlLang` in `Story.stories.tsx` and `ForwardsLang` in `DocsPage.stories.tsx`. Every assertion is a DOM check on the `lang` attribute's presence and value, run in happy-dom (`// @vitest-environment happy-dom`). They establish that the attribute is set correctly. They cannot establish that a screen reader selects the right voice profile as a result, because that requires rendering and listening, and the test environment contains no assistive technology. The PR body's own checklist item — "Run your favourite screenreader and observe how it handles languages" — is the only thing on the PR that would have closed that gap, and it was phrased as a suggestion for the reviewer with no record of anyone performing it. |
| Reviewer confidence signal | 1 | One automated reviewer (CodeRabbit) posted nine actionable comments across three separate reviews, and they were substantive: blank `docs.lang` values rendering as `lang=""` instead of inheriting the project setting; project annotations not threaded into title and subtitle resolution; a `lang="en"` override wrongly covering caller-supplied content in the same ActionBar; `docsLang` dropping on grouped ArgRows. That is real engagement with whether the mechanism works. What no comment addressed — bot or human — is whether AT announces the right language afterwards. The single human review (ndelangen) was an approval with an empty body; code-owner reviews requested from two others were never delivered, and one of the two co-authors merged the change. |
| Direct language | 1 | "Screen readers" appears once in the PR body, but the bulk of the discussion (both human and bot) is about code structure, not the affected users or their experience. |
| Outcome clarity | 1 | The mechanism (lang propagation through the render tree) is clearly documented in code, tests, PR description and `docs/api/parameters.mdx`, but whether the fix actually improves screen-reader pronunciation was never confirmed by anyone in the thread. |
| **Total** | **4/12** | |

## Review Pattern Observed
Substantive automated review of the mechanism, substantive automated testing of the mechanism, and no verification of the outcome. An AI reviewer caught four real defects in how the language value propagates. Four test surfaces assert the resulting attribute. A single human approval carried no comment body. The change was co-authored, and one of the two co-authors merged it and then applied the `qa:success` label themselves.

Collaboration between co-authors is not independent review: a second person was involved in writing the code, code-owner review was requested from two others and never arrived, and no independent party verified the outcome. "The code was reviewed and tested" and "the accessibility claim was verified" are two different things here, and only the first happened.

## Infrastructure Gap Illustrated
This case shows that neither code review nor automated testing is accessibility verification. Both were done, and done competently: an automated reviewer found four real defects in how the language value propagates, and four test surfaces assert that the resulting attribute carries the right string. The claim that actually matters — that AT will now announce the right language — goes unchecked by all of it, because verifying it requires rendering the page and listening rather than reading a diff or asserting on a DOM node in a headless environment.

This is the sharpest illustration in the corpus of the distinction the initiative rests on: the mechanism is testable by machine, the outcome is not. A required "AT verified: yes/no, which AT, which version and browser, what was observed" field, distinct from both general code review and unit testing, would have surfaced that gap before merge.

Note also that this is the third case in the sample where the person merging was an author of the change — here, one of two co-authors. See Pattern 2 in [`signals/review-patterns-v0.2.md`](../signals/review-patterns-v0.2.md).

## Verification
Re-verified three times.

**2026-07-27, against the GitHub API.** An earlier version described two AI reviewers and characterised the bot comments as concerning only import conventions and test-file placement; both were inaccurate and were corrected.

**2026-07-29, against the live PR page**, which showed the corrected version was still not exact. Score unchanged at 4/12. Findings:

- **Comment counts.** CodeRabbit posted three separate reviews, with seven, one and one actionable comments respectively, plus five nitpicks. The figure "9 of 12 inline comments" conflated actionable comments with a total; the defensible statement is that a single automated reviewer posted nine actionable comments across three reviews and found four genuine defects in how the language value propagates. The page's conversation counter is unreliable on this PR — bot cross-references from downstream dependency bumps inflate it, and it has moved since without a human comment being added. Cite the per-review actionable counts, not the counter.
- **"Ahead of a feature freeze" is unsourced.** It appears nowhere on the PR page and has been removed pending a source.
- **"Maintainer" overstated.** The author's badge reads Contributor, not Member. They self-assign, apply labels, move project-board cards and merge — so they hold write access — but the page contradicts the word "maintainer" on its face.
- **Code-owner reviews were requested from two people** (jonniebigodes, kylegach) and neither reviewed. The lone approval came from a third person and carried no comment body.
- **The author self-certified QA**, flipping `qa:needed` to `qa:success` on their own merged change. This is the cleanest single illustration in the corpus of a process with no independent checkpoint.
- **It shipped.** Merged to `next`, referenced by the 10.5.0-alpha.10 prerelease and consumed downstream at storybook 10.5.0 — unlike all four Bootstrap cases.

**2026-08-04, against the PR's Files-changed and Commits tabs.** Five corrections in this pass:

- **Co-authorship.** Commit `520c701` shows mehm8128 as commit author with `Co-Authored-By: Steve Dodier-Lazaro`, inverting an earlier note that recorded mehm8128 as the possible co-author. The case study described the PR as authored and merged by the same person; reframed as co-authored, merged by one of the two co-authors. Score unchanged at 4/12 — criterion 3 turns on the absence of a recorded screen-reader result, not on the number of authors.
- **The second commit resolved.** `383d590` is a housekeeping merge of `next` into the feature branch, authored by Sidnioulz alone — not a second substantive contribution. The PR's only substantive commit is `520c701`.
- **Test surfaces were not accounted for.** The criterion 3 justification cited only the PR body checklist and did not mention that the PR ships four automated test surfaces for the language mechanism. It now names them and states why DOM assertions in happy-dom cannot establish AT behaviour. The score is unchanged; the reasoning is no longer incomplete. This correction arose from reading the Files-changed tab, which had not previously been consulted for this case — a gap in method, not only in this file.
- **Stale figure.** The rubric table still carried "9 of 12 inline comments" despite that figure being retired in this section on 2026-07-29. Corrected.
- **"All three Bootstrap cases" corrected to four**, matching the Pattern 7 fix made in `review-patterns-v0.2.md` on 2026-07-31 and not previously propagated here.

**Contributor connection disclosed.** mehm8128, the commit author of `520c701`, starred this corpus repo on 2026-08-04. The connection was identified the same day and the corrections above were made on that basis. The public right-of-reply comment left on the PR on 2026-08-01 was updated the same day to record the co-authorship and to correct a separate "shipped"/"merged" error in its labelling paragraph. No contributor to any project in this corpus has write access to this repository or has edited any case study.

## Source
[github.com/storybookjs/storybook/pull/35321](https://github.com/storybookjs/storybook/pull/35321)
