# Accessibility Pull Request

## Summary
Describe the accessibility problem and the change made.

## User impact
Who benefits from this change?

- [ ] Screen-reader users
- [ ] Keyboard-only users
- [ ] Low-vision users
- [ ] Users who zoom or reflow content
- [ ] Users with cognitive or attention-related needs
- [ ] Users affected by motion, timing, or flashing behavior
- [ ] Other:

Describe the before and after experience in plain language.

## Related issue
Link the issue, discussion, audit finding, or bug report.

## WCAG mapping (required)
List the relevant WCAG success criteria. If no direct mapping applies, say so explicitly and explain why the change still improves accessibility — don't leave this section blank.

- Example: 1.1.1 Non-text Content
- Example: 2.1.1 Keyboard
- Example: 2.4.7 Focus Visible
- Example: 4.1.2 Name, Role, Value

## AT verification (required)
Was this fix checked with real assistive technology, by you or a reviewer, before this PR is merged? This is the single field most correlated with review quality in this repo's case studies — a WCAG citation without it is not sufficient.

- [ ] Yes — verified with AT below (name it, and who verified: author / reviewer / both)
- [ ] Not yet — requesting a reviewer with AT access to verify before merge
- [ ] N/A — explain why (e.g. build-tooling-only change with no rendered output)

## What changed
Check all that apply and add details.

- [ ] Semantic HTML changed
- [ ] Accessible name, label, or description changed
- [ ] ARIA role, state, or property changed
- [ ] Keyboard interaction changed
- [ ] Focus order or focus management changed
- [ ] Color contrast or visual presentation changed
- [ ] Error handling or validation changed
- [ ] Screen-reader announcement behavior changed
- [ ] Motion, animation, or timing changed
- [ ] Documentation changed
- [ ] Test coverage changed

Implementation notes:

## How to reproduce the problem
Provide exact steps for the pre-fix behavior.

## How to verify the fix
Provide exact manual verification steps.

Expected result:

## Test environment
Complete as applicable.

| Category | Details |
| --- | --- |
| OS | |
| Browser | |
| Device | |
| Assistive technology | |
| Automated tools | |

## Evidence
Attach or describe evidence where relevant.

- Screenshots
- Short video or GIF
- Screen-reader output or transcript
- axe, Lighthouse, pa11y, or test results
- Unit, integration, or end-to-end tests

## Regression check
What nearby behavior was checked to avoid introducing a new barrier?

## Risks or open questions
Document uncertainty clearly so maintainers can review with confidence.

## Reviewer checklist
- [ ] The accessibility problem is clearly described.
- [ ] Affected users or usage modes are identified.
- [ ] WCAG mapping is filled in, or the absence of a mapping is explained.
- [ ] AT verification is filled in — not left as "N/A" without justification.
- [ ] Manual verification steps are included.
- [ ] Browser, OS, and assistive technology details are included where relevant.
- [ ] The change was checked for keyboard behavior.
- [ ] The change was checked for screen-reader behavior where relevant.
- [ ] Any remaining risks or follow-ups are documented.
