Accessibility section for CONTRIBUTING.md
Accessibility contributions
Accessibility contributions are welcome and valued.
This project aims to be usable by people with disabilities and by people using assistive technologies, keyboard-only navigation, zoom, reflow, captions, reduced motion, or other alternate interaction modes. Accessibility work is treated as a core quality requirement for the Vue frontend, Python backend behavior that affects user-facing flows, and project documentation.
Contributors with disabilities are welcome. If an accommodation would help with communication, review format, timing, or the way evidence is shared, please open an issue or use the project's preferred contact path listed in ACCESSIBILITY.md.
What counts as an accessibility contribution
Accessibility work in this project includes, but is not limited to:
•	Fixing semantic HTML, labels, headings, landmarks, alt text, and link purpose in Vue components and docs.
•	Improving keyboard navigation, focus order, focus visibility, dialogs, menus, tables, and form validation behavior.
•	Correcting accessible names, descriptions, announcements, and ARIA usage.
•	Improving contrast, text scaling, reflow, reduced-motion handling, or error messaging.
•	Updating Python-generated content, templates, form responses, API-backed UI states, or rendered output that affects accessibility.
•	Adding tests, documentation, issue templates, or CI checks that improve accessibility review confidence.
Before opening an accessibility PR
Please do the following where relevant:
1.	Review ACCESSIBILITY.md for project scope, target conformance level, and known limitations.
2.	Check existing issues labeled a11y to avoid duplicating work.
3.	Describe the user impact clearly, for example: screen-reader users, keyboard-only users, low-vision users, or users affected by motion or cognitive load.
4.	Map the issue to WCAG success criteria if you can.
5.	Test the change manually, not only with automated tooling.
Recommended checks
For frontend or docs changes, the minimum expected checks are:
•	Keyboard-only navigation through the affected flow.
•	Visible focus for changed interactive elements.
•	Accessible name, role, value, and state checks for changed controls.
•	Screen-reader verification where the change affects announcements, labels, landmarks, forms, tables, dialogs, or dynamic content.
•	Contrast, zoom, and reflow checks where layout or visual styling changed.
For backend or API work that affects the UI, please verify that:
•	Error states return clear and actionable messages.
•	Validation messages can be associated with the relevant form fields.
•	Async loading, success, and failure states are exposed clearly in the UI.
•	Structured data sent to the frontend does not force inaccessible rendering patterns.
Preferred test setup
Use the best setup available to you and document it in the PR.
Suggested combinations:
•	NVDA with Firefox or Chrome on Windows.
•	VoiceOver with Safari on macOS.
•	TalkBack with Chrome on Android for mobile-impacting changes.
•	axe DevTools, Lighthouse, eslint accessibility rules, pa11y, Playwright, or equivalent automated checks.
Automated checks are useful, but they do not replace manual testing.
Opening the PR
Use the accessibility PR template for accessibility-related changes.
A strong accessibility PR should include:
•	The problem being solved.
•	The affected users or usage mode.
•	Relevant WCAG mapping, if known.
•	Exact reproduction and verification steps.
•	Browser, OS, device, and assistive-technology details.
•	Evidence such as screenshots, short recordings, copied screen-reader output, or automated scan results.
•	Any risks, trade-offs, or follow-up issues.
Coding expectations for the Vue frontend
When contributing to the Vue application, prefer:
•	Native HTML elements before custom ARIA patterns.
•	Real button elements for button behavior and real a elements for navigation.
•	Programmatic labels connected to inputs.
•	Predictable heading structure and landmarks.
•	Focus management for dialogs, drawers, route changes, and other stateful UI.
•	Error messaging that is visible, understandable, and associated with the control.
•	Accessible loading and status messages for async operations.
•	Motion and animation that respects reduced-motion preferences.
Avoid adding ARIA where native semantics already solve the problem.
Coding expectations for Python-backed behavior
For Python services, templates, or server-rendered output that affect user experience:
•	Return clear validation and error messages.
•	Preserve enough structure for the frontend to present accessible names, descriptions, states, and relationships.
•	Avoid response formats that force color-only, icon-only, or position-only meaning.
•	Keep generated content concise and understandable where possible.
•	Document any accessibility implications when changing APIs that drive forms, tables, navigation, or notifications.
Review expectations
Maintainers may not be specialists in accessibility testing, so contributors should make changes easy to review.
Please assume the reviewer needs:
•	A plain-language explanation of the barrier.
•	Reproducible test steps.
•	Clear expected behavior.
•	Evidence from the tools or assistive technologies you used.
If a reviewer asks for clarification, treat that as part of making the change reviewable, not as a rejection of the work.
Labels and triage
Use or request the project's accessibility labels where available, for example:
•	a11y
•	a11y: bug
•	a11y: enhancement
•	a11y: needs triage
•	a11y: ready for review
•	a11y: needs manual test
Documentation expectations
Changes to docs should also be accessible.
Please use:
•	Descriptive headings.
•	Meaningful link text.
•	Alt text for informative images.
•	Tables only when they improve comprehension.
•	Captions or transcripts for essential media.
•	Clear instructions that do not depend only on color, position, or visual cues.
Good first accessibility fixes
If you are looking for a place to start, useful contributions include:
•	Missing form labels.
•	Incorrect heading hierarchy.
•	Poor focus visibility.
•	Keyboard traps.
•	Missing dialog titles or descriptions.
•	Icon-only controls without accessible names.
•	Low-contrast text or controls.
•	Inaccessible error summaries or validation messages.
•	Missing alt text or unclear link text in docs.
When in doubt
Prefer a smaller, well-tested accessibility improvement over a large speculative refactor. If you are unsure whether an issue is accessibility-related, open an issue with the a11y label and describe the user impact.
<img width="476" height="648" alt="image" src="https://github.com/user-attachments/assets/e597cc6a-2a54-4096-8d6c-6651ca6e5bc9" />
