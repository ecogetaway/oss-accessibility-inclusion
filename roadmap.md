# Roadmap

## v0.1 — done
- Reusable templates: `ACCESSIBILITY.md`, accessibility issue template, accessibility PR template, `CONTRIBUTING.md` section.
- `review-rubric.md`: six scored criteria (0–2 each) operationalizing the method described in the README.
- Five case studies (Bootstrap ×2, MUI, VS Code, Storybook), each scored against the rubric.
- `signals/review-patterns-v0.1.md`: first cross-case synthesis.
- Issue and PR templates updated to require a WCAG mapping and an explicit AT-verification field — the two fields the case studies showed actually predict review quality.

## v0.2 — next
- **Source a stalled or rejected a11y PR.** All five v0.1 case studies merged quickly or merged despite unresolved gaps; none stalled the way the companion i18n repo's case studies did. Need at least one counter-example to know whether that's a real pattern (a11y reviewed faster than i18n) or a small-sample artifact.
- **`a11y-signals.yml`.** A machine-readable file for projects to declare their accessibility posture (conformance target, review capacity, AT test matrix), mirroring the i18n-signals.yml concept in [oss-language-inclusion](https://github.com/ecogetaway/oss-language-inclusion).
- **Comparative note across the two companion repos** once both have enough case studies — a11y vs. i18n review patterns is the actual thesis of running two parallel studies.
- Expand the rubric's score bands with real threshold data once there are 10+ case studies to calibrate against.

## Later
- Solicit case-study candidates and maintainer feedback through the issue labels described in the README's "How to Participate" section.
- Revisit whether the rubric needs a criterion specific to security review of contributed ARIA/markup, given the injection-risk note in the README's "Accessibility Review Gap" section.
