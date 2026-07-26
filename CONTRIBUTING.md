# Contributing

Thanks for looking. This document explains what this project is, what you can pick
up, and — just as importantly — what is deliberately not open for anyone to decide.

## What this project is

We are investigating how accessibility contributions to open source are reviewed in
practice. Not whether projects are accessible — whether the infrastructure for
accepting accessibility work exists at all.

The work has three strands:

- **Evidence.** Case studies of real projects, and analysis of real accessibility pull
  requests, showing where contributions stall and why.
- **`a11y-signals.yml`.** A machine-readable file, in the spirit of `CODEOWNERS` or
  `SECURITY.md`, letting a project declare its accessibility conformance target, its
  review capacity, and its assistive-technology test matrix.
- **A review rubric**, so a maintainer with no accessibility background can make a
  defensible decision about an accessibility contribution.

## The two tiers

Issues here fall into one of two groups, and the labels tell you which.

### Tier A — `tier-a`, `good first issue`

Claimable by anyone, cold. No prior involvement needed, no accessibility expertise
needed, no permission needed. Comment on the issue saying you're taking it.

These are tasks where correctness is checkable against a source: surveys, citation
checks, documentation, data collection. Every Tier A issue states its acceptance
criteria in a form someone else can verify. If you can't tell whether you've
finished, the issue is badly written — tell us and we'll fix it.

### Tier B — `tier-b`, `needs-council-review`

**Not claimable.** These are open so the structure of the work is visible, not so
that they get done quickly.

These issues turn on judgements that require lived experience of assistive
technology — what counts as a meaningful test floor, where the line falls between a
decision a non-expert can make and one they can't, what a project is actually
promising when it declares review capacity. Getting those wrong doesn't just produce
a worse artifact; it produces one that gives cover to projects that shouldn't have
it.

Those decisions belong to the Disability Advisory Council: daily assistive-technology
users, compensated for their time, holding approval authority over
accessibility-substantive questions. Nothing about us, without us.

The Council is not yet seated. Until it is, Tier B issues stay parked. You are
welcome to draft and discuss in the comments — that's useful, and it's not the same
thing as deciding.

**If you use assistive technology daily**, we would much rather talk with you about
joining the Council than have you do this work unpaid. Open an issue or reach out
directly.

## What "nothing about us, without us" means here operationally

It is easy to state as a value and harder to encode as a control. In this repo it
means specifically:

- A maintainer may not merge a resolution to a `needs-council-review` issue on their
  own judgement, regardless of how confident they are.
- The `needs-council-review` label is not a formality to be cleared. It is removed
  only after Council review.
- If you think an issue is mislabelled — that a Tier A issue actually requires lived
  experience — say so. Reclassifying upward is always welcome and never a
  complaint we'll take badly.

## Claiming and finishing work

1. Comment on the issue to claim it. One person at a time, unless the issue says it
   can be split.
2. If you go quiet for two weeks, we'll unassign so someone else can pick it up. No
   hard feelings — life happens, and a stale claim blocks others.
3. Open a pull request referencing the issue number.
4. Work against the acceptance criteria in the issue. Partial work is fine and
   welcome; say what you did and didn't do.

## Evidence standards

Most of the Tier A work produces evidence files, and those have to hold up under a
reviewer who is looking for reasons to doubt us.

- **Pin your links.** GitHub permalinks to a commit SHA, never a branch URL. Branch
  URLs rot, and a rotted citation is worse than no citation.
- **Primary sources only** for legal and regulatory claims. The official text or the
  issuing body's own page. Not a summary article, not a vendor blog, not an AI
  answer.
- **Record the date you checked.**
- **No opinions in data files.** If a row asserts something the linked source doesn't
  say, it's wrong even if it's true. Judgement belongs in prose, clearly marked as
  such.
- **Uncertainty is a valid finding.** `unclear` with a one-line explanation is more
  useful than a confident guess.

We would rather have twenty rows we can defend than sixty we can't.

## The contribution process itself should be accessible

It would be embarrassing to run an accessibility project with an inaccessible
contribution process, so:

- No required tooling. If GitHub's interface doesn't work for you, send us the work
  however suits — plain text, email, a comment — and we'll handle the mechanics.
- Ask for what you need. Format, timing, a different way of reviewing. It isn't an
  imposition and you don't need to explain why.
- **We will never ask you to disclose a disability**, and you should never feel you
  need to in order to justify a request or establish your standing to contribute.
  Council membership is the one place where daily assistive-technology use is
  relevant, and that is a conversation you opt into, not a disclosure we collect.

If any part of this process is a barrier, that's a bug in the process. Tell us.

## What this project does not do

- We do not certify or rate projects as accessible.
- `a11y-signals.yml` describes a project's *process*, not its *product*. A project
  declaring review capacity is not claiming its software is accessible, and the file
  must never be usable as evidence that it is.
- We do not file accessibility complaints, and we are not a legal service.

## Credit

Contributors are credited by name in the repository and in any published output that
draws on their work, unless they ask not to be. If you'd prefer a different name, a
handle, or no attribution, say so and that's the end of it.

> **Maintainers:** the exact attribution convention is still being settled across
> this repo and the language-infrastructure repo. Replace this note with the agreed
> wording before the first external contribution is merged, so no one contributes
> under unclear terms.

## Conduct

Be decent. Assume good faith. If someone tells you a request or a phrasing is a
problem, take it seriously rather than debating it.

> **Maintainers:** add a `CODE_OF_CONDUCT.md` (the Contributor Covenant is the usual
> starting point) and link it from here. A project asking disabled people to
> participate should have a stated conduct policy and a named person to report to
> before it starts recruiting.

## Questions

Open an issue with the `question` label. There is no such thing as a question too
basic for this repo — if something is unclear to you, it's unclear, and that's worth
knowing.
