Open source has standardized infrastructure for code contribution, but no equivalent infrastructure for accessibility contribution.

This repository investigates whether accessibility inclusion is a missing infrastructure layer in open source — and documents how accessibility pull requests are actually reviewed in practice.

# Open Source Accessibility Inclusion

**Early evidence suggests** a recurring pattern: code contribution has mature shared workflows, while accessibility contribution depends on local process, individual goodwill, and maintainer capacity that often does not include accessibility expertise.

This is a companion project to [oss-language-inclusion](https://github.com/ecogetaway/oss-language-inclusion), applying the same evidence-first method to a second under-served contribution domain.

## Terminology used in this repo

- **a11y** = accessibility ("a", 11 letters, "y")
- **AT** = assistive technology (screen readers, switch devices, magnifiers)
- **signals** = synthesized patterns
- **case studies** = structured reviews of real pull requests
- **rubric** = the standard checklist each case study is scored against

---

## Why Now

- Accessibility is now a legal requirement in a growing share of the world: the ADA in the US, EN 301 549 in the EU, and the European Accessibility Act (in force since 2025).
- Open source components sit inside products that carry these legal obligations — the accessibility of dependencies is becoming everyone's problem.
- Roughly one in six people worldwide lives with a significant disability. For them, an inaccessible interface is not degraded; it is unusable.
- Accessibility PRs in major projects stall for the same structural reasons i18n PRs do: maintainers cannot confidently review work that requires expertise they do not have.

---

## What This Is / What This Is Not

| What this is | What this is not |
| --- | --- |
| A meta-review study of how real a11y PRs are reviewed in practice | An accessibility testing tool or audit service |
| Structured case studies scored against a standard rubric | General accessibility guidance (see the excellent A11Y Project for that) |
| Reusable repo templates: ACCESSIBILITY.md, issue and PR templates | A conformance certification body |
| A maintainer and contributor input channel | A final standards proposal |

---

## The Accessibility Review Gap

Code contributions pass through linters, static analysis, tests, and review. Accessibility contributions typically pass through none of that in any structured way. The gap has five parts:

1. **Essential to real users.** Screen-reader users cannot use a button with no accessible name. This is not polish; it is function.
2. **Systematically under-contributed.** A11y fixes rarely add visible features and require testing with assistive technology most contributors do not use.
3. **Hard for maintainers to review.** A maintainer who has never used a screen reader cannot judge whether an ARIA change is correct — so the PR stalls.
4. **No standardized contributor pathway.** There is no canonical way to structure an a11y PR: which WCAG criteria it addresses, how it was tested, with which AT, and what the expected behavior is.
5. **No maintainer signal.** Contributors have no way to know whether a project can review a11y work, what conformance target it holds, or which AT it tests against — before investing effort.

There is also a security dimension: ARIA attributes are injected into the DOM, and an attribute sourced from an unreviewed contribution can carry the same injection risks as any untrusted string. Unreviewed contributions as an attack surface is not only an i18n story.

---

## Method

We select recent (2026), merged or active accessibility pull requests in popular open source projects and analyze each against a standard review rubric:

- Was **user impact** stated in terms of affected users and tasks?
- Was the change **mapped to WCAG success criteria**?
- Was **assistive technology testing evidence** provided (which AT, which version, what steps)?
- Did reviewers show **confidence signals** (substantive a11y review vs. rubber-stamp)?
- What **stalled, what worked**, and what did maintainers and contributors say about the process?
- Was user impact described in **direct, specific language** (e.g., "VoiceOver users") rather than euphemism or generality?

Each case study records the contribution, the review pattern observed, and the infrastructure gap it illustrates.

## Current Case Studies

| Project | PR | Category |
| --- | --- | --- |
| Bootstrap | [#42539](https://github.com/twbs/bootstrap/pull/42539) — floating labels before control for screen readers | Semantics / reading order |
| Bootstrap | [#42500](https://github.com/twbs/bootstrap/pull/42500) — accessible OTP input rework | Complex widget interaction |
| MUI Material UI | [#48572](https://github.com/mui/material-ui/pull/48572) — autocomplete focus fix for VoiceOver | AT-specific behavior |
| VS Code | [#324192](https://github.com/microsoft/vscode/pull/324192) — warning icon colors, 2026 Light theme | Contrast / theming |
| Storybook | [#35321](https://github.com/storybookjs/storybook/pull/35321) — lang attribute handling in preview | Accessibility × i18n intersection |

Full write-ups: [Bootstrap #42539](case-studies/bootstrap-pr42539.md) · [Bootstrap #42500](case-studies/bootstrap-pr42500.md) · [MUI #48572](case-studies/mui-material-ui-pr48572.md) · [VS Code #324192](case-studies/vscode-pr324192.md) · [Storybook #35321](case-studies/storybook-pr35321.md).

Case study write-ups live in [`case-studies/`](case-studies/). The scoring checklist lives in [`review-rubric.md`](review-rubric.md). Cross-case patterns are synthesized in [`signals/review-patterns-v0.1.md`](signals/review-patterns-v0.1.md).

---

## Reusable Templates

This repository also provides drop-in files any project can adopt today:

- [`ACCESSIBILITY.md`](ACCESSIBILITY.md) — a project accessibility statement: scope, conformance target, testing expectations, known limitations, and contact path.
- [`.github/ISSUE_TEMPLATE/accessibility.yml`](.github/ISSUE_TEMPLATE/accessibility.yml) — a structured accessibility issue form capturing user impact, reproduction steps, environment, and WCAG mapping.
- [`.github/PULL_REQUEST_TEMPLATE/accessibility.md`](.github/PULL_REQUEST_TEMPLATE/accessibility.md) — an a11y PR template with user impact, WCAG mapping, verification steps, and a reviewer checklist designed so non-expert maintainers can review with more confidence.
- A CONTRIBUTING.md accessibility section (see [`CONTRIBUTING.md`](CONTRIBUTING.md)).

Planned: `a11y-signals.yml` — a machine-readable file for projects to declare their accessibility posture (conformance target, review capacity, AT test matrix), analogous to the i18n-signals.yml concept in the companion repository.

---

## How to Participate

- Suggest a recent a11y PR worth studying: open an issue with the `case-study-candidate` label.
- Share your experience contributing or reviewing accessibility work: open an issue with the `community-feedback` label.
- Maintainers: tell us what would make a11y PRs reviewable for you — that input directly shapes the rubric and templates.

Contributors with disabilities are welcome. If an accommodation would help with communication, review format, timing, or how evidence is shared, please say so in any issue.

**A note on language.** This project uses direct, person-centered language ("person with a disability," "screen-reader users") and follows individuals' own preferred terms, whether person-first or identity-first. We avoid euphemisms such as "differently abled," "special needs," or "people of all abilities," which disability-language guides identify as patronizing or obscuring. Case studies describe affected users specifically (for example, "VoiceOver users," "users navigating by keyboard") rather than generically.

---

## Repository Structure

    oss-accessibility-inclusion/
    ├── README.md
    ├── LICENSE                  (Apache 2.0)
    ├── ACCESSIBILITY.md
    ├── CONTRIBUTING.md
    ├── problem-definition.md
    ├── roadmap.md
    ├── review-rubric.md
    ├── case-studies/
    ├── signals/
    └── .github/
        ├── ISSUE_TEMPLATE/accessibility.yml
        └── PULL_REQUEST_TEMPLATE/accessibility.md

---

## Related Work

This project sits deliberately between guidance repos and evidence repos:

- [intel/AccessibilityPlaybook](https://github.com/intel/AccessibilityPlaybook) — guidance for making open source accessible (playbook; not PR-review research)
- [a11yproject/a11yproject.com](https://github.com/a11yproject/a11yproject.com) — broad community education
- [accessibilitysupported/a11ysupport.io](https://github.com/accessibilitysupported/a11ysupport.io) — structured, verified AT support data (a model for evidence discipline)
- [dequelabs/axe-core](https://github.com/dequelabs/axe-core) — automated testing engine (tooling anchor)

None of these centers what this repository centers: structured case studies of how accessibility contributions are actually reviewed, and the contributor/maintainer infrastructure that evidence points to.

---

## Current Status

- Repository established with reusable templates: ACCESSIBILITY.md, issue template, PR template, CONTRIBUTING section.
- Review rubric v0.1 finalized ([`review-rubric.md`](review-rubric.md)): six criteria, 0–2 points each.
- Five case studies completed and scored across Bootstrap, MUI, VS Code, and Storybook (all 2026 PRs); scores range 4/12 to 11/12.
- First cross-case signals synthesized in [`signals/review-patterns-v0.1.md`](signals/review-patterns-v0.1.md): AT-testing evidence (not WCAG citation) predicts review quality; self-merge by a rights-holding maintainer is the default failure mode; automated review volume does not substitute for accessibility review.
- Companion project: [oss-language-inclusion](https://github.com/ecogetaway/oss-language-inclusion) — same method, applied to internationalization.
- Licensed under Apache 2.0.
