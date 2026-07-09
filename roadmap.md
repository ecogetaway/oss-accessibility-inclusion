# Roadmap

## v0.1 — done
- Reusable templates: `ACCESSIBILITY.md`, accessibility issue template, accessibility PR template, `CONTRIBUTING.md` section.
- `review-rubric.md`: six scored criteria (0–2 each) operationalizing the method described in the README.
- Five case studies (Bootstrap ×2, MUI, VS Code, Storybook), each scored against the rubric.
- `signals/review-patterns-v0.1.md`: first cross-case synthesis.
- Issue and PR templates updated to require a WCAG mapping and an explicit AT-verification field — the two fields the case studies showed actually predict review quality.

## v0.2 — in progress
- [x] Issue and PR templates now require a WCAG mapping and an explicit AT-verification field.
- [x] **Sourced a stalled/rejected a11y PR** — [Bootstrap #41607](case-studies/bootstrap-pr41607.md), open 11 months with zero review, closed unmerged for unrelated architectural reasons. Result: the "a11y reviewed faster than i18n" pattern in v0.1 was a sampling artifact — see [Pattern 5](signals/review-patterns-v0.1.md#pattern-5--the-fast-review-pattern-in-v01-was-a-sampling-artifact-not-a-real-difference-from-i18n). The real driver looks like author identity (maintainer vs. outside contributor), not the accessibility domain.
- [ ] **`a11y-signals.yml`.** A machine-readable file for projects to declare their accessibility posture (conformance target, review capacity, AT test matrix), mirroring the i18n-signals.yml concept in [oss-language-inclusion](https://github.com/ecogetaway/oss-language-inclusion).
- [ ] **Comparative note across the two companion repos** once both have enough case studies — a11y vs. i18n review patterns is the actual thesis of running two parallel studies.
- [ ] Expand the rubric's score bands with real threshold data once there are 10+ case studies to calibrate against.

## v0.3 — next
- Test the maintainer-vs-contributor hypothesis from Pattern 5 against another project, to see if it holds outside Bootstrap.
- Source a case where an a11y PR was actively reviewed and rejected on the merits (not just closed for unrelated reasons), to separate "never reviewed" from "reviewed and rejected."

## Later
- Solicit case-study candidates and maintainer feedback through the issue labels described in the README's "How to Participate" section.
- Revisit whether the rubric needs a criterion specific to security review of contributed ARIA/markup, given the injection-risk note in the README's "Accessibility Review Gap" section.
