# Open Source Accessibility Inclusion

Open source has standardized infrastructure for code contribution, but no equivalent infrastructure for accessibility contribution.

This repository investigates whether accessibility inclusion is a missing infrastructure layer in open source — and documents how accessibility pull requests are actually reviewed in practice.

**Early evidence suggests** a recurring pattern: code contribution has mature shared workflows, while accessibility contribution depends on local process, individual goodwill, and maintainer capacity that often does not include accessibility expertise.

This is a companion project to [oss-language-inclusion](https://github.com/ecogetaway/oss-language-inclusion), applying the same evidence-first method to a second under-served contribution domain.

**Provenance.** Part of the **OSS Infrastructure Initiative** (Sanjay C. and Aniruddh Raghavendra) — an evidence-first portfolio applying one method across three under-served open source contribution domains: internationalization, accessibility, and AI contribution. First published July 2026. Full portfolio under [Companion Projects](#companion-projects) below.

_Status as of 4 August 2026: seven scored case studies, a review rubric, and a draft a11y-signals.yml. All seven re-verified three times — API on 27 July, live pages on 29 July, and every diff, commit and linked issue on 4 August; five scores changed in total and several cross-case patterns were corrected or extended._

**New here?** Start with [The Seven PRs, Explained](seven-prs-explained.md) — a five-minute plain-language walkthrough of what we found and why it matters.

_Built with AI-assisted drafting and research; every factual claim is independently verified against primary sources before publication._

## The Findings, First

Seven real accessibility PRs across Bootstrap, MUI, VS Code, and Storybook, each scored 0–12 against a [six-criterion review rubric](review-rubric.md):

| Case study | Category | Score |
| --- | --- | --- |
| [MUI #48572](case-studies/mui-material-ui-pr48572.md) | AT-specific behavior | **9/12** |
| [VS Code #324192](case-studies/vscode-pr324192.md) | Contrast / theming | **8/12** |
| [Bootstrap #42500](case-studies/bootstrap-pr42500.md) | Complex widget interaction | 7/12 |
| [Bootstrap #42524](case-studies/bootstrap-pr42524.md) | Follow-up defect after an unreviewed merge | 7/12 |
| [Bootstrap #42539](case-studies/bootstrap-pr42539.md) | Semantics / reading order | 6/12 |
| [Bootstrap #41607](case-studies/bootstrap-pr41607.md) | Stalled 11 months, closed unmerged | 4/12 |
| [Storybook #35321](case-studies/storybook-pr35321.md) | Accessibility × i18n | 4/12 |

No case reaches the 10–12 band the rubric describes as normal for an accessibility-mature project. The range is 4 to 9, across four of the best-resourced front-end projects in open source.

Four findings the scores surface — full synthesis in [signals/review-patterns-v0.2.md](signals/review-patterns-v0.2.md):

1. **Verification evidence — not WCAG citation — predicts review quality.** The PR with the best standards work in the corpus, reasoning about two success criteria and anchoring four, scored 7/12 and merged with interaction defects that surfaced within a week. The PR citing no criterion at all scored 9/12, because a reviewer opened it with VoiceOver first.
2. **The most heavily reviewed PR still scored among the lowest.** Storybook #35321 drew nine actionable comments across three automated reviews, finding four genuine defects in how the fix propagated, and ships four automated test surfaces asserting the resulting attribute. Nobody established what a screen reader announces afterwards — the test environment has no assistive technology in it. Code review and automated testing are not accessibility verification.
3. **Whether a PR gets reviewed at all tracks who opened it.** Six of the six merged PRs were merged by their own author; the one outside contributor's fix was labelled `accessibility` within hours and then waited eleven months for any response, before being closed as superseded by an unrelated rewrite — never evaluated on its merits.
4. **A control written as prose is not a gate.** The best-specified issue in the corpus carried an explicit rule that only an accessibility tester could close it after verification. It was closed as completed by someone else, and the `verified` label arrived roughly three weeks later attached to a measured contrast value — real evidence, arriving too late to inform the decision it nominally confirms.

Optional share graphic for posts/talks: [`docs/images/a11y-scoreboard.svg`](docs/images/a11y-scoreboard.svg).

### Try this first

| Priority | Action |
| --- | --- |
| **1. Primary** | Steal the [accessibility PR template](.github/PULL_REQUEST_TEMPLATE/accessibility.md) for your next a11y contribution (or paste it into an existing PR description) |
| **2. Secondary** | Add [`ACCESSIBILITY.md`](ACCESSIBILITY.md) to your project so contributors know your conformance target and how to test |
| **3. Then** | [Tell us what broke or helped](https://github.com/ecogetaway/oss-accessibility-inclusion/issues/new/choose) — maintainer and contributor feedback reshapes the rubric |

The research (scoreboard + case studies) is here so you can see *why* the template asks for AT evidence. The template is the thing to use tomorrow.

Please do **not** ask people to star the repo. The useful signal is a template trial or a scored disagreement with a case study.

## Terminology used in this repo

- **a11y** = accessibility ("a", 11 letters, "y")
- **AT** = assistive technology (screen readers, switch devices, magnifiers)
- **signals** = synthesized patterns
- **case studies** = structured reviews of real pull requests
- **rubric** = the standard checklist each case study is scored against

---

## Why Now

- Accessibility is increasingly a legal requirement. In the EU, Directive (EU) 2016/2102 covers public sector websites and mobile applications, and the European Accessibility Act (Directive (EU) 2019/882, in force since 2019) has applied to a range of consumer products and services since 28 June 2025; conformance with the harmonised standard EN 301 549 (V3.2.1) creates a presumption of conformity with both. In the US, the Department of Justice's 2024 rule under Title II of the ADA requires state and local government web content to meet WCAG 2.1 Level AA, with compliance dates now falling in April 2027 and April 2028 following a one-year extension issued in April 2026; Title III rulemaking for the private sector remains paused, and obligations there continue to be shaped by litigation.
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
| Bootstrap | [#42524](https://github.com/twbs/bootstrap/pull/42524) — OTP click-to-focus and overwrite fixes after #42500 merged with defects | Complex widget interaction (follow-up) |
| MUI Material UI | [#48572](https://github.com/mui/material-ui/pull/48572) — autocomplete focus fix for VoiceOver | AT-specific behavior |
| VS Code | [#324192](https://github.com/microsoft/vscode/pull/324192) — warning icon colors, 2026 Light theme | Contrast / theming |
| Storybook | [#35321](https://github.com/storybookjs/storybook/pull/35321) — lang attribute handling in preview | Accessibility × i18n intersection |
| Bootstrap | [#41607](https://github.com/twbs/bootstrap/pull/41607) — modal focus-trap fix, closed unmerged after 11 months | Complex widget interaction (stalled) |

Full write-ups: [Bootstrap #42539](case-studies/bootstrap-pr42539.md) · [Bootstrap #42500](case-studies/bootstrap-pr42500.md) · [Bootstrap #42524](case-studies/bootstrap-pr42524.md) · [MUI #48572](case-studies/mui-material-ui-pr48572.md) · [VS Code #324192](case-studies/vscode-pr324192.md) · [Storybook #35321](case-studies/storybook-pr35321.md) · [Bootstrap #41607](case-studies/bootstrap-pr41607.md).

Case study write-ups live in [`case-studies/`](case-studies/). The scoring checklist lives in [`review-rubric.md`](review-rubric.md). Cross-case patterns are synthesized in [`signals/review-patterns-v0.2.md`](signals/review-patterns-v0.2.md).

---

## Reusable Templates

Drop-in files any project can adopt today (same links as [Try this first](#try-this-first)):

- [`ACCESSIBILITY.md`](ACCESSIBILITY.md) — project accessibility statement: scope, conformance target, testing expectations, known limitations, contact path.
- [`.github/ISSUE_TEMPLATE/accessibility.yml`](.github/ISSUE_TEMPLATE/accessibility.yml) — structured accessibility issue form.
- [`.github/PULL_REQUEST_TEMPLATE/accessibility.md`](.github/PULL_REQUEST_TEMPLATE/accessibility.md) — **primary CTA** — a11y PR template with user impact, WCAG mapping, AT verification, and a non-expert reviewer checklist.
- [`templates/CONTRIBUTING-accessibility-section.md`](templates/CONTRIBUTING-accessibility-section.md) — accessibility section to paste into your own project's `CONTRIBUTING.md`.
- [`signals/a11y-signals.schema.yml`](signals/a11y-signals.schema.yml) — draft machine-readable posture file (analogous to CODEOWNERS); examples in [`signals/examples/`](signals/examples/).

Not yet built: a validator for the signals schema (see [`roadmap.md`](roadmap.md)).

---

## How to Participate

1. **Use a template** on a real a11y issue or PR, then open feedback here.
2. Suggest a recent a11y PR worth studying: issue label `case-study-candidate`.
3. Share reviewing/contributing experience: label `community-feedback`.
4. Maintainers: tell us what would make a11y PRs reviewable for you.

Contributors with disabilities are welcome. If an accommodation would help with communication, review format, timing, or how evidence is shared, please say so in any issue.

**A note on language.** This project uses direct, person-centered language ("person with a disability," "screen-reader users") and follows individuals' own preferred terms, whether person-first or identity-first. We avoid euphemisms such as "differently abled," "special needs," or "people of all abilities," which disability-language guides identify as patronizing or obscuring. Case studies describe affected users specifically (for example, "VoiceOver users," "users navigating by keyboard") rather than generically.

---

## Repository Structure

    oss-accessibility-inclusion/
    ├── README.md
    ├── LICENSE                  (Apache 2.0)
    ├── ACCESSIBILITY.md
    ├── CONTRIBUTING.md          (how to contribute to this research)
    ├── problem-definition.md
    ├── roadmap.md
    ├── review-rubric.md
    ├── case-studies/
    ├── signals/
    ├── templates/               (drop-in files for your own project)
    └── .github/
        ├── ISSUE_TEMPLATE/accessibility.yml
        └── PULL_REQUEST_TEMPLATE/accessibility.md

---

## Companion Projects

Three repositories, one method: document how a contribution domain actually fails in real repositories, then build the smallest machine-readable piece of infrastructure the evidence says is missing. Each domain's adoption compounds the others' credibility.

| Domain | Repository | What it builds | Maturity |
| --- | --- | --- | --- |
| Internationalization | [oss-language-inclusion](https://github.com/ecogetaway/oss-language-inclusion) | Translated-string contribution evidence + `i18n-security-lint` CI tooling | Most developed; method published in CACM Blog and DevOps.com |
| Accessibility | [oss-accessibility-inclusion](https://github.com/ecogetaway/oss-accessibility-inclusion) | How accessibility PRs are reviewed; review rubric + draft `a11y-signals.yml` | Active |
| AI contribution | [oss-ai-contribution-policy](https://github.com/ecogetaway/oss-ai-contribution-policy) | Machine-readable `ai-contribution-policy.yml` standard (verification over detection) | Early evidence-gathering |

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
- Issue and PR templates updated (v0.2) to require WCAG mapping and an explicit AT-verification field, based directly on case-study evidence for what predicts review quality.
- Seven case studies completed and scored across Bootstrap, MUI, VS Code, and Storybook (all 2026 PRs, plus one 2025–2026 stalled PR); scores range 4/12 to 9/12.
- Cross-case signals synthesized in [`signals/review-patterns-v0.2.md`](signals/review-patterns-v0.2.md): verification evidence (not WCAG citation) predicts review quality; self-merge is the norm rather than the exception, at six of six merged PRs; substantive code review does not substitute for assistive-technology verification; a process control written as prose in an issue body is not enforced and gets bypassed; code-owner team review requests went unanswered in four of four cases (all in Bootstrap), while a request to two named individuals succeeded once and failed once elsewhere in the corpus; and whether a PR gets reviewed at all appears to depend more on author identity than on the accessibility domain itself.
- All seven PRs and their linked issues re-verified three times: against the GitHub API on 2026-07-27, against live GitHub pages on 2026-07-29, and against every PR's full diff, commit history and linked issues or discussions on 2026-08-04. Five scores changed across the three passes, several cross-case patterns were inverted or corrected, and criterion 3 of the rubric was rebuilt with explicit bands after the corpus showed it being applied inconsistently. Every change is recorded in the affected case study's Verification section and in [`signals/review-patterns-v0.2.md`](signals/review-patterns-v0.2.md).
- `a11y-signals.yml` schema drafted ([`signals/a11y-signals.schema.yml`](signals/a11y-signals.schema.yml)), with two worked examples — a machine-readable accessibility-posture declaration any project can place at its repo root, analogous to CODEOWNERS.
- Companion project: [oss-language-inclusion](https://github.com/ecogetaway/oss-language-inclusion) — same method, applied to internationalization.
- Licensed under Apache 2.0.
  
