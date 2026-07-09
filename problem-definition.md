# Problem Definition

Open source has standardized infrastructure for code contribution — linters, CI, tests, review checklists. It has no equivalent infrastructure for accessibility contribution. This repository investigates whether that gap is structural rather than incidental, and documents how accessibility pull requests are actually reviewed in practice, not how they're supposed to be reviewed.

## The core claim

Code contribution depends on shared, repeatable process. Accessibility contribution depends on local process, individual goodwill, and whichever maintainer happens to have assistive-technology (AT) experience — which most don't. That dependency produces the same failure shape repeatedly: correct fixes that ship on the author's word alone, or well-reviewed PRs where the review never touches the accessibility claim itself. See [`signals/review-patterns-v0.1.md`](signals/review-patterns-v0.1.md) for evidence.

## The five-part gap

1. **Essential to real users, not polish.** A button with no accessible name is unusable, not degraded, for a screen-reader user.
2. **Systematically under-contributed.** A11y fixes rarely add visible features and require AT most contributors don't have.
3. **Hard for maintainers to review.** A maintainer who has never used a screen reader can't judge whether an ARIA change is correct.
4. **No standardized contributor pathway.** There's no canonical way to structure an a11y PR: which WCAG criteria it addresses, how it was tested, with which AT.
5. **No maintainer signal.** Contributors can't tell in advance whether a project can actually review a11y work, or what it holds itself to.

Full context, legal drivers, and related work are in the [README](README.md#the-accessibility-review-gap).

## What "solved" would look like

Not a certification body or a testing tool — a repeatable pattern any project can adopt: an issue/PR template that makes WCAG mapping and AT verification structural rather than optional, and a way for a project to declare its accessibility review capacity before a contributor invests effort. The case studies in this repo are evidence for which parts of that pattern actually correlate with better review outcomes (see the rubric and signals), not a guess.

## Scope boundary

This repo studies *review process*, not code correctness. A case study can score low on the rubric even when the underlying fix was technically right — the rubric measures whether the review was repeatable and verifiable, not whether the author happened to get it correct.
