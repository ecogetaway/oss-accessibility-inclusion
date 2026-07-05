# Accessibility Statement

This project aims to be usable by people with disabilities and by people using assistive technologies, keyboard-only navigation, zoom, reflow, captions, reduced motion, or other alternate interaction modes. Accessibility is treated as a core quality requirement, not optional polish.

This file explains our scope, conformance target, testing expectations, how to report barriers, and how accessibility contributions are reviewed.

## Scope

Accessibility applies to every user-facing surface of this project:

- Repository documentation (README, guides, case studies)
- Issue and pull request templates
- Any published site, demo, or rendered output derived from this repository

## Conformance target

We target **WCAG 2.2 Level AA** as the baseline for all user-facing content, and reference **ARIA** authoring practices for any interactive components.

Where a case study or template references a standard, we cite the specific WCAG success criterion (for example, 1.1.1 Non-text Content; 2.1.1 Keyboard; 2.4.7 Focus Visible; 4.1.2 Name, Role, Value).

## Known limitations

This is an early-stage project. Current known limitations:

- Case-study write-ups are being added incrementally and may not yet cover all disability interaction modes.
- Automated accessibility checks are not yet wired into CI. This is on the roadmap.

If you find a barrier not listed here, please report it — see below.

## Reporting an accessibility barrier

Open an issue using the **Accessibility issue** template (it applies the `a11y` label automatically). Please describe:

- Who is affected (for example, screen-reader users, keyboard-only users, low-vision users)
- Where the barrier occurs (file, page, or component)
- Steps to reproduce, expected behavior, and actual behavior
- Your environment: browser, operating system, and any assistive technology with version

If you are unsure how to classify the issue, focus on the user impact and the steps to reproduce it. Imperfect reports are welcome; silence is the only wrong option.

## Testing expectations for contributions

Automated checks are useful but do not replace manual testing. Where relevant to your change, please verify:

- Keyboard-only navigation through the affected flow
- Visible focus for changed interactive elements
- Accessible name, role, value, and state for changed controls
- Screen-reader behavior where announcements, labels, landmarks, forms, or dynamic content changed
- Contrast, zoom, and reflow where visual presentation changed

Suggested test setups: NVDA with Firefox or Chrome on Windows; VoiceOver with Safari on macOS; TalkBack with Chrome on Android for mobile-impacting changes; axe DevTools, Lighthouse, or pa11y for automated passes. Document in your PR which setup you used.

## How accessibility contributions are reviewed

Accessibility PRs use the dedicated PR template, which captures user impact, WCAG mapping, reproduction steps, verification steps, and testing evidence. The template is designed so that maintainers who are not accessibility specialists can still review with confidence.

Review readiness: accessibility PRs are actively reviewed. If a change requires assistive-technology expertise the maintainers lack, we will say so openly in the PR rather than let it stall silently — and we welcome community verification.

## Accommodations

Contributors with disabilities are welcome. If an accommodation would help with communication, review format, timing, or the way evidence is shared, please say so in any issue or discussion. Preferred contact path: open an issue in this repository.

## Language

This project uses direct, person-centered language ("person with a disability," "screen-reader users") and follows individuals' own preferred terms, whether person-first or identity-first. We avoid euphemisms such as "differently abled," "special needs," or "people of all abilities."
