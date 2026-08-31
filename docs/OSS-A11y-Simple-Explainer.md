# Open Source Accessibility Initiative
## Simple Explainer — What This Project Is (and What “Patterns” Mean)

**Audience:** You, collaborators, interns, partners  
**Tone:** Plain language  
**Hub:** https://ecogetaway.github.io/ (file: `OSS-A11y-Simple-Explainer.md`)  
**Repo copy:** [`docs/OSS-A11y-Simple-Explainer.md`](OSS-A11y-Simple-Explainer.md) in oss-accessibility-inclusion  
**Repo:** https://github.com/ecogetaway/oss-accessibility-inclusion  

Keep hub and repo copies in sync when you edit §6a (how we identify a11y PRs) or the phase table.

---

# 1. The project in one paragraph

Open source is good at reviewing **code**. It is much weaker at reviewing **accessibility** changes (fixes that help screen-reader users, keyboard users, and others).

This project does not build a new screen reader or sell audits. It **studies real accessibility pull requests** on GitHub, scores how they were reviewed, writes down what keeps going wrong, and turns those lessons into **templates and signals** other projects can reuse.

---

# 2. What is a “pattern”? (simple)

A **pattern** is a **recurring observation** that shows up across several case studies — not a one-off story about a single PR.

Think of it like this:

| Term | Simple meaning | Example |
| --- | --- | --- |
| **Case study** | One real accessibility PR, written up and scored | “Bootstrap PR #42500 scored 7/12” |
| **Score / rubric** | A fixed checklist (0–12) so cases are compared fairly | Did anyone test with a screen reader? |
| **Pattern** | “We keep seeing the same kind of thing in many cases” | “Merged a11y PRs were usually merged by their own author” |
| **Signal** | A written finding you can point to later (in docs or a schema) | Pattern text in `signals/review-patterns-v0.2.md` |

**Pattern ≠ prediction about the whole internet.**  
With seven cases, a pattern means: *in this carefully checked sample, this kept happening.* More cases test whether it still holds.

**Pattern ≠ a bug in one app.**  
The bug is “floating label breaks screen readers.”  
The pattern is “projects merge accessibility changes without a second person checking with assistive technology.”

### Everyday analogy

- **Case study** = one patient’s chart  
- **Pattern** = “in these seven charts, the same process failure repeats”  
- **Template / ACCESSIBILITY.md** = the improved checklist you hand the next hospital  

### Patterns you already published (v0.2) — in plain English

| # | Pattern (plain English) |
| --- | --- |
| **1** | Citing WCAG is not enough. What matters is whether someone **checked with real assistive technology** (or a real device) before merge. |
| **2** | In this corpus, **every merged a11y PR was merged by its own author**. Second-person review is rare. |
| **3** | Lots of **code review** (even bots catching real bugs) is still not **accessibility verification**. Nobody asked what a screen reader announces. |
| **4** | A rule written in prose (“only the a11y tester may close this”) is **not a real gate** unless the platform enforces it. |
| **5** | **Who opened the PR** matters. Maintainer a11y PRs moved fast; an outside contributor’s fix waited ~11 months and was never judged on merit. |
| **6** | Asking a **team** for review often gets silence; asking a **named person** worked once — still unreliable either way. |
| **7** | **Merged ≠ shipped.** Some fixes merge to an unreleased branch while users on released versions still have the bug. |

When the plan says “test Pattern 5 outside Bootstrap,” it means: *check another project to see if “outside contributors wait forever” happens there too — or if it was mostly a Bootstrap story.*

---

# 3. The big table — “What the project actually is” — explained simply

This is the life cycle of the initiative. You do **not** only score case studies forever. Scoring is how you earn the right to propose infrastructure.

| Phase | Simple name | What you do (simple) | What you are trying to learn or achieve | What “done” looks like |
| --- | --- | --- | --- | --- |
| **Now (and sometimes later)** | **Evidence** | Find real accessibility PRs → write case studies → score them with the rubric → notice patterns | Is there a real, repeatable review gap — with proof, not vibes? | A small, honest corpus (e.g. 7 → 10 → 12 cases) and written patterns |
| **Next** | **Infrastructure** | Turn patterns into things others can use: accessibility PR template, `ACCESSIBILITY.md`, draft `a11y-signals.yml`, clearer “how to review a11y” expectations | If the gap is real, what should a project *do differently* on Monday? | Drop-in files + docs people can copy without joining your research |
| **Then** | **Adoption** | Ask real maintainers/projects to try the templates or declare signals; listen to what breaks | Does anyone outside your repo change behaviour? | Named trials, feedback issues, maybe a merged outward PR — not star counts |
| **Later** | **Scale (optional)** | Tools (e.g. validate the signals file), metrics, policy/procurement, partnerships, funding that buys capacity | Can this become shared infrastructure, not only a research diary? | Only after evidence + some adoption — not instead of them |

**Important:** Most **Next** artifacts already exist as drafts in the repo (PR template, `ACCESSIBILITY.md`, signals schema + examples). Next work is mostly **harden from patterns, package an Adopt guide, and write a sharp “how to review” one-pager** — not invent everything from scratch.

**Draft vs lock:** You do **not** wait for a huge corpus before drafting. You **do** wait (or stay provisional) before locking schema/v1 claims. More PRs sharpen drafts; they don’t mean “no artifacts until N=20.” Sampling should mix popularity/impact with author type, outcome type, and defect category — not only famous repos. Details: `OSS-A11y-Phase-Plans` §0b.

**Detailed task plans** for Next / Then / Later (checklists, sequencing, exit criteria) live in:  
`OSS-A11y-Phase-Plans` (Markdown in the hub repo + DOCX in Downloads).

### How the phases connect (one sentence each)

1. **Evidence** — “Here’s what actually happens on real PRs.”  
2. **Infrastructure** — “Here’s a reusable way to do better.”  
3. **Adoption** — “Someone else tried it.”  
4. **Scale** — “Make it easier to adopt and sustain (tools, funding, partners).”

### What you repeat vs what you graduate from

| Keep doing (selectively) | Graduate toward |
| --- | --- |
| Add a case when you need a **new pattern**, a **calibration** point, or a **missing type** (e.g. “reviewed and rejected on merits”) | Shipping and improving templates / signals |
| Re-verify old cases if facts change | Getting maintainers to try the artifacts |
| Update pattern write-ups when evidence changes | Funding and partnerships that support the infrastructure story |

**You do not need infinite case studies.**  
You need **enough honest evidence** that the patterns are trustworthy, then you **spend more time on infrastructure and adoption**.

---

# 4. Mini glossary

| Word | Meaning here |
| --- | --- |
| **a11y** | Accessibility |
| **AT** | Assistive technology (e.g. VoiceOver, NVDA) |
| **Rubric** | The shared 6-criterion scoring sheet (0–12) |
| **Corpus** | The set of scored case studies |
| **Signals** | Synthesized findings (patterns) written so others can reuse them |
| **Template** | A ready-made PR/issue/`ACCESSIBILITY.md` file others can copy |
| **Adoption** | Another project actually using your artifact |
| **Outward PR** | You contribute a fix or template *into someone else’s repo* |

---

# 5. What this project is / is not

| It is | It is not |
| --- | --- |
| Evidence-first research on how a11y PRs are reviewed | An accessibility audit company |
| A source of reusable contribution infrastructure | A WCAG certification body |
| A companion to OSS language-inclusion research | “Just write more blog posts forever” |
| A long game: prove → package → adopt → (maybe) scale | Only “keep scoring PRs until the end of time” |

---

# 6. One picture of the loop

```text
Find a11y PRs
    → Score case studies (rubric)
        → Write patterns (what repeats)
            → Ship templates / signals (infrastructure)
                → Someone tries them (adoption)
                    → Learn + optionally add more cases
                        → Later: tools, partners, funding capacity
```

**Bottom line:**  
**Patterns** = “what keeps repeating in the evidence.”  
**The project** = use that evidence to build and spread better accessibility contribution infrastructure — not to run an endless scoring factory.

---

# 6a. How we identify "real accessibility PRs" and "accessibility changes"

Someone will ask: *How do you know a PR is a real accessibility pull request? How do you tell an accessibility change from ordinary code?*

Short answer: **we do not trust the word “a11y” alone.** We use a two-stage process — **find candidates**, then **screen them** — before anything becomes a scored case study.

## Stage 1 — Find candidates (discovery)

We look in public GitHub threads for PRs that *claim or look like* accessibility work, using several overlapping signals:

| Signal | Examples |
| --- | --- |
| **Labels** | `accessibility`, `a11y`, project-specific a11y tags |
| **Title / body language** | screen reader, VoiceOver, NVDA, JAWS, keyboard, focus trap, ARIA, WCAG, contrast, accessible name, `lang` attribute |
| **Linked issues** | Bug reports that name who is blocked (e.g. “VoiceOver users cannot…”) |
| **Known projects** | Popular UI / tooling repos where a11y PRs are findable (Bootstrap, MUI, VS Code, Storybook, …) — and deliberately beyond them over time |
| **Community tips** | Suggestions filed under `case-study-candidate` in our repo |

**GitHub-style searches we actually use (adapt per repo):**

```text
is:pr label:accessibility
is:pr label:a11y
is:pr "screen reader" OR VoiceOver OR NVDA OR WCAG OR ARIA in:title,body
```

Discovery produces a **candidate list**, not a corpus. Many candidates will be rejected at Stage 2.

## Stage 2 — Screen: is this really an accessibility change?

A PR enters the corpus only if it passes a **substance check**. We ask:

1. **User barrier?** Does the change address something that blocks or harms people using assistive technology or alternative interaction (screen readers, keyboard-only, magnification/contrast, etc.) — not merely a visual polish or refactor that happens to touch markup?
2. **Accessibility surface?** Does the diff actually touch accessibility-relevant surfaces — e.g. semantics/reading order, focus management, ARIA, names/roles, contrast/theming, AT-specific behavior, or a11y × i18n (`lang`, etc.)?
3. **Public, scorable thread?** Is there a public PR (and usually a linked issue) with enough recorded discussion that we can score the *review process* honestly against our rubric — without inventing what happened offline?
4. **Not a duplicate?** Does it add a new dimension (project, author type, outcome, defect category) rather than repeating an existing case?

If the title says “a11y” but the change is only a drive-by lint rename with **no user impact**, it fails.  
If there is **no “a11y” label** but the PR clearly fixes a VoiceOver focus bug, it can still pass.

**We study the review process, not whether the fix was “correct.”** So “real accessibility PR” means: *a real proposed change about an accessibility barrier, with a public review trail* — not “we independently audited that the code is perfect.”

## Stage 3 — Score only after screening (case study)

Only screened-in PRs get a full write-up (`case-studies/TEMPLATE.md`) and scores on the six-criterion rubric (`review-rubric.md`):

1. User impact stated  
2. WCAG mapping  
3. AT testing evidence  
4. Reviewer confidence signal  
5. Direct language  
6. Outcome clarity  

Evidence for scoring = **what is written in the PR thread and linked issues** — we do not infer unrecorded VoiceOver tests.

## Screening card (what we fill before saying “yes, this is a case”)

```text
PR URL:
Project:
Category (semantics / AT / contrast / widget / a11y×i18n / stalled / other):
Author type (maintainer / external / bot):
Outcome (merged / closed / open) + date:
AT evidence in thread? (none / claimed / linked artifact):
WCAG mapping present? (y/n):
Why include / exclude:
Sampling note (what new dimension does this add?):
```

## Sampling rules (so “real” does not mean “only famous repos”)

We deliberately mix:

- Popular **and** mid-size projects  
- Maintainer-authored **and** outside-contributor PRs  
- Merged, stalled, closed, and (when we can find one) **reviewed and rejected on merits**  
- Different defect categories (not five more of the same Bootstrap widget story)

Full checklist: `OSS-A11y-Phase-Plans` §0b · candidate pipeline: GitHub issue #9.

## One sentence you can say out loud

> “We find public PRs that look accessibility-related via labels and keywords, then screen each one for a real user barrier and a scorable review thread. Only then do we write a case study and score the *review process* — not the beauty of the code.”

---

# 7. Helpful resources (to understand this project better)

Use these when a term or skill in the project feels fuzzy. You do **not** need to finish everything before contributing. Skim by section.

**Your own finds (keep building this list)**

| Resource | Why it helps this project |
| --- | --- |
| [AAArdvark Accessibility on YouTube](https://www.youtube.com/@AAArdvark-Accessibility) | Plain-language walkthroughs of accessibility topics (including WCAG 3 discussions). Good when official specs feel dense. |
| [Accessibility Weekly — Issue #512](https://a11yweekly.com/issue/512/) | Curated a11y news/links each week. Useful for staying current while you research. *(You have submitted a link for possible inclusion — nice channel for the initiative later.)* |
| [Accessibility Weekly (subscribe / home)](https://a11yweekly.com/) | Ongoing periodical; reply or write `hello@a11yweekly.com` for suggestions. |

---

## 7.1 Start here — big picture accessibility

| Resource | What you’ll understand |
| --- | --- |
| [The A11Y Project](https://www.a11yproject.com/) | Practical accessibility checklist and community baseline. Our repo is **not** a replacement for this — we study *review process*, not general how-to. |
| [W3C WAI — Accessibility fundamentals](https://www.w3.org/WAI/fundamentals/) | Official plain intro: who disability/a11y is for, and why web a11y matters. |
| [WAI — Tips for getting started](https://www.w3.org/WAI/tips/) | Short tips for designing, writing, and developing accessibly. |
| [WebAIM — Introduction to web accessibility](https://webaim.org/intro/) | Clear beginner path from a long-running a11y org. |

## 7.2 WCAG and “success criteria” (what case studies map to)

| Resource | What you’ll understand |
| --- | --- |
| [WCAG 2.2 (W3C Recommendation)](https://www.w3.org/TR/WCAG22/) | The standard people mean by “WCAG.” Case studies often map fixes to success criteria (e.g. 1.4.3 Contrast). |
| [How to meet WCAG (quick reference)](https://www.w3.org/WAI/WCAG22/quickref/) | Filterable checklist — easier than reading the full TR. |
| [Understanding WCAG 2.2](https://www.w3.org/WAI/WCAG22/Understanding/) | “Why this criterion exists” essays — useful when scoring *user impact* vs citation-only PRs. |
| [WCAG 3 Working Draft (exploratory)](https://www.w3.org/TR/wcag-3.0/) | Future direction; **not** what most OSS PRs cite today. Treat confidently blog posts about Bronze/Silver/Gold carefully — check the draft. AAArdvark’s WCAG 3 streams are a friendly companion. |

**Link to our work:** Pattern 1 says WCAG citation alone does not predict review quality — verification evidence does. Learn WCAG so you can *recognize* mappings; do not treat citation as a gold star.

## 7.3 Assistive technology (AT) — what “verification evidence” means

| Resource | What you’ll understand |
| --- | --- |
| [WebAIM — Screen reader user survey](https://webaim.org/projects/screenreadersurvey/) | Which screen readers people actually use (context for “tested with VoiceOver/NVDA”). |
| [NVDA (free, Windows)](https://www.nvaccess.org/download/) | Common AT for Windows testing. |
| [VoiceOver (macOS/iOS) — Apple guide](https://support.apple.com/guide/voiceover/welcome/mac) | Common AT on Apple platforms. |
| [Accessibility Insights](https://accessibilityinsights.io/) | Guided automated + manual checks (still not a full substitute for AT). |
| [axe DevTools](https://www.deque.com/axe/devtools/) | Popular automated checker — great *supplement*, not proof a screen reader works. |

**Link to our work:** Pattern 3 — code review and automated tests ≠ AT verification. If a PR never says which AT was used, that is a scoring signal.

## 7.4 How accessibility shows up in pull requests (closest to our method)

| Resource | What you’ll understand |
| --- | --- |
| [Our repo — Seven PRs, Explained](https://github.com/ecogetaway/oss-accessibility-inclusion/blob/main/seven-prs-explained.md) | Fastest path into *this* project’s findings. |
| [Our review rubric](https://github.com/ecogetaway/oss-accessibility-inclusion/blob/main/review-rubric.md) | Exact criteria you will score against. |
| [Our patterns v0.2](https://github.com/ecogetaway/oss-accessibility-inclusion/blob/main/signals/review-patterns-v0.2.md) | Full pattern write-ups with links to cases. |
| [Accessibility PR template (ours)](https://github.com/ecogetaway/oss-accessibility-inclusion/blob/main/.github/PULL_REQUEST_TEMPLATE/accessibility.md) | What “good infrastructure” looks like as a file people can steal. |
| [GitHub — Reviewing changes in pull requests](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests) | How reviews, approvals, and merges work on the forge (needed for Patterns 2, 6). |
| [GitHub CODEOWNERS](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners) | Why “team review requested” appears in Pattern 6. |

## 7.5 Disability, language, and ethics (so write-ups stay respectful)

| Resource | What you’ll understand |
| --- | --- |
| [WAI — How to refer to people with disabilities](https://www.w3.org/WAI/EO/Drafts/PWD-Use-People/) | Language guidance (prefer clear, specific, respectful wording). |
| [Inclusive Design Principles](https://inclusivedesignprinciples.org/) | Mindset beyond compliance checklists. |
| [Disability Debrief](https://www.disabilitydebrief.org/) | Lived-experience / disability journalism context (appears in a11y press rounds). |

## 7.6 Open source process (the “infrastructure” half of the thesis)

| Resource | What you’ll understand |
| --- | --- |
| [Producing Open Source Software (Fogel) — free book](https://producingoss.com/) | How OSS projects actually run (review, maintainers, contributors). |
| [Open Source Guides — Finding users → Building community](https://opensource.guide/) | Maintainer/contributor norms. |
| [CHAOSS — Community health metrics](https://chaoss.community/) | How communities measure process (longer-term adjacency for “signals”). |
| Companion repo: [oss-language-inclusion](https://github.com/ecogetaway/oss-language-inclusion) | Same *evidence → infrastructure* method applied to i18n / translated-string security. |

## 7.7 Newsletters & ongoing learning (low effort, high signal)

| Resource | Notes |
| --- | --- |
| [Accessibility Weekly](https://a11yweekly.com/) | David A. Kennedy’s roundup — you already use this; good place for initiative visibility once a solid public link exists. |
| [WebAIM newsletter / blog](https://webaim.org/blog/) | Practical testing and standards updates. |
| [TPGi blog](https://www.tpgi.com/blog/) | Deep technical a11y articles. |
| [Deque blog](https://www.deque.com/blog/) | Tools + WCAG practice. |
| [tink.uk (Léonie Watson)](https://tink.uk/) | Screen-reader / standards perspective from a leading expert. |

## 7.8 Suggested learning path (2–3 hours total to start)

1. **30 min** — [Seven PRs, Explained](https://github.com/ecogetaway/oss-accessibility-inclusion/blob/main/seven-prs-explained.md) + skim this explainer (§1–3).  
2. **30 min** — [WCAG quickref](https://www.w3.org/WAI/WCAG22/quickref/) (browse, don’t memorize).  
3. **30 min** — One AAArdvark video on a topic you don’t know + skim [A11Y Project checklist](https://www.a11yproject.com/checklist/).  
4. **30 min** — Read **one** full case study in our repo end-to-end, then the matching pattern in v0.2.  
5. **Ongoing** — Skim [A11y Weekly](https://a11yweekly.com/) when it arrives; star links that touch *review process*, AT testing, or OSS contribution — not only UI tips.

## 7.9 How to add to this list

When you find something useful (like AAArdvark or a Weekly issue), add a row under **Your own finds** with: name, URL, and one sentence on *why it helps this project* (process, AT, WCAG, OSS, or disability context). Prefer primary sources (W3C, project docs, public PRs) when making claims in case studies.

---

*Explainer for collaborators and interns. Details and scored evidence live in the GitHub repo; this document translates the ideas and points to learning resources.*
