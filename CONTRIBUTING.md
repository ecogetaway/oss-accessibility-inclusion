# Contributing

This is a **research repository**, not a software product. There is no application to build and no test suite to run. What we produce is evidence: structured reviews of real accessibility pull requests, a scoring rubric, synthesized patterns, and reusable templates other projects can adopt.

Contributions are welcome from people who have never written a line of code, and from people who have shipped accessibility work for twenty years. The most valuable contribution here is usually **a verified observation**, not a patch.

If you are looking for the reusable accessibility section to drop into your *own* project's CONTRIBUTING.md, that lives in [`templates/CONTRIBUTING-accessibility-section.md`](templates/CONTRIBUTING-accessibility-section.md). Take it — that is what it is for.

## Ways to contribute

**Score a new case study.** Pick a real accessibility PR from any open source project, score it against the [six-criterion rubric](review-rubric.md), and write it up in the shape of the existing [case studies](case-studies/). This is how the corpus grows.

**Disagree with a score.** Every case study is a judgement call. If you think a score is wrong, open an issue explaining which criterion and why. A well-argued disagreement is more useful to us than a new case study — it tests the rubric itself.

**Tell us what happened when you used the templates.** If you tried the [accessibility PR template](.github/PULL_REQUEST_TEMPLATE/accessibility.md) or [`ACCESSIBILITY.md`](ACCESSIBILITY.md) in a real project, we want to know what worked, what maintainers pushed back on, and what you deleted. Template trials and honest failure reports reshape the rubric.

**Bring lived experience.** Some questions cannot be answered from documentation. If you use a screen reader, switch device, magnifier, voice control, or any other assistive technology daily, your reading of what "verified" should mean carries more weight here than any standards citation.

**Research and evidence work.** Sourcing candidate PRs, checking prior art, verifying claims against primary sources — much of this needs care and patience rather than accessibility expertise.

## Finding something to work on

Open issues are labelled by tier so you can self-select:

- **`tier-a`** — cold-claimable. No assistive-technology experience or lived-experience judgement required. Start here if you are new.
- **`tier-b`** — needs experience with assistive technology to answer well. Open for input; we would rather wait for the right person than guess.
- **`needs-lived-experience-review`** — we specifically want input from people who use assistive technology daily.
- **`good first issue`** — scoped small and documented enough to pick up cold.

**To claim something, comment on the issue.** That is the whole process. You do not need to ask permission, introduce yourself first, or be assigned before starting. If an issue has been quiet for a while, assume it is free and say you are picking it up.

If nothing fits but you want to help, open a new issue describing what you would like to work on.

## The evidence standard

This is the one rule that is not negotiable, and it applies to every contribution.

**Every factual claim is verified against a primary source before it lands.** A primary source is the PR, the commit, the diff, the linked issue, the standard itself, or the rendered page — not a summary, not a blog post about it, and not a model's recollection. Case studies in this repo have been re-verified multiple times, and scores have changed as a result.

Concretely, that means:

- Link the PR, commit, or issue you are describing, and quote the part you are relying on.
- If you scored something, show which rubric criterion produced each point.
- If you tested with assistive technology, say which AT, which browser, which OS, and what it actually announced. "Works with a screen reader" is not evidence.
- If you are unsure, write down the uncertainty instead of resolving it silently. Flagged uncertainty is useful; confident error is not.
- AI-assisted drafting and research are fine and openly used in this project. The verification requirement does not relax because a model produced the draft — it tightens.

## Accessibility of this project itself

Contributors with disabilities are welcome, and that includes how we work together, not only what we publish.

If an accommodation would help — communication format, review pace, timing, how evidence is shared or requested, anything — say so in any issue and we will adapt. You do not need to explain why, and you do not need a diagnosis to ask.

We use direct, person-centered language ("person with a disability", "screen-reader users") and follow individuals' own preferred terms, whether person-first or identity-first. We avoid euphemisms such as "differently abled", "special needs", or "people of all abilities". See [`ACCESSIBILITY.md`](ACCESSIBILITY.md) for the project's own conformance scope and known limitations.

## Opening a pull request

For prose, case studies, and rubric work — most of what lands here — a PR needs:

- What you are adding or changing, and why.
- Your sources, linked, for every factual claim.
- For a case study: the completed rubric scoring, criterion by criterion.
- For a rubric or template change: what evidence prompted it. Ideally a case where the current version produced the wrong answer.

Small fixes — typos, broken links, unclear sentences — need none of that. Just open the PR.

## Code of conduct

Participation is governed by the [Code of Conduct](CODE_OF_CONDUCT.md). Accessibility work attracts people who have been talked over in a lot of other rooms; this one is meant to be different.
