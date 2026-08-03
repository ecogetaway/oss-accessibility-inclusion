# The Seven PRs, Explained

A plain-language walkthrough of the seven accessibility pull requests scored in this repo. If you want the full evidence and per-criterion reasoning, each case study is linked from [`case-studies/`](case-studies/). This page is the five-minute version.

All seven were verified twice against primary sources — once via the GitHub API and once against the live pull request pages. That found two of our own characterisations inaccurate and two of our own scores wrong; every correction is recorded in the affected case study. The scores below are the corrected ones.

---


We took seven real accessibility fixes from four widely used open-source projects — Bootstrap, MUI, Storybook and Visual Studio Code — and read every comment on each one. Then we scored them against the same six questions, using only what was written in the thread as evidence.

The scoring is deliberately not about whether the fix was correct. All seven fixes were, as far as we can tell, reasonable code. We were asking something different: when an accessibility change is proposed, does anything in the process check that it actually works for the people it is meant to help?

## The six questions, in plain terms

1. Who was affected, and what could they not do? Is that written down?
2. Is it tied to a standard? Does anyone name the specific success criterion at stake?
3. Did anyone verify it against real assistive technology or a real device — named, with version, and with what was observed?
4. Did a reviewer actually engage? Or was it a rubber stamp, or nothing at all?
5. Is the language specific? "NVDA users on Windows" rather than "accessibility issue".
6. Is the outcome legible? Could a future contributor tell what happened, and why?

Each scores 0 to 2, for twelve points in total. Ten and above looks like a mature process. Five and below means no structured accessibility review happened, and the outcome depended on who happened to pick it up.

## The seven at a glance

| Pull request | Project | The problem | Score |
| --- | --- | --- | --- |
| #48572 | MUI | One Backspace deleted three items, but only for VoiceOver users | 9/12 |
| #324192 | VS Code | Warning text too faint to read in the light theme | 8/12 |
| #42524 | Bootstrap | Fixing the OTP field broke it again, then broke it on iPad | 7/12 |
| #42539 | Bootstrap | Screen readers announced a field's value before its name | 6/12 |
| #42500 | Bootstrap | Six-box one-time-password field read aloud as six separate fields | 6/12 |
| #41607 | Bootstrap | Modals had a phantom stop in the keyboard tab order | 4/12 |
| #35321 | Storybook | Pages always claimed to be in English, whatever language they were in | 4/12 |

**The most important thing about that table is its ceiling.** Nothing reaches the 10-to-12 band — not in four of the best-resourced front-end codebases in open source. The top of the range is itself a finding.

## MUI #48572 — 9 out of 12

**What broke.** In a multi-select field, pressing Backspace once deleted three items instead of one — but only if you had navigated there using VoiceOver, Apple's screen reader. VoiceOver sends an extra, invisible keystroke that ordinary keyboard use does not, and the component was not expecting it.

**What happened.** The author fixed the state handling and suppressed the duplicate keystroke. Then a reviewer did the thing almost nobody else in this sample did: they opened it with VoiceOver on Chrome and Safari, confirmed it worked, and said so before approving.

**Why it scores highest.** This is the only case where a second person independently verified the fix using the actual assistive technology. The author noted that the relevant half of the bug was impossible to cover with an automated test — the invisible keystroke does not exist in a test harness. A machine could not have caught it. Someone had to listen.

**The catch.** The verification exists as nine words in a review comment: "Looks good, tested the fix with VO+Chrome/Safari." No version, no operating system, nothing about what was actually observed. That is why the best case in the corpus scores 9 rather than 12 — the rigour was real, but unreproducible. It depended entirely on that reviewer being present.

## VS Code #324192 — 8 out of 12

**What broke.** Warning text in a menu sat at too low a contrast against its background in one light theme. Readable if your eyesight is good; not if you have low vision or reduced contrast sensitivity.

**What happened.** The issue was filed through a formal accessibility testing programme, on a structured template: tagged with the exact standard breached, stating the required contrast ratio twice, naming the affected users precisely, with reproduction steps and full environment details. The pull request that answered it cites none of that — every point this case scores well on, it inherits from the issue.

**Why it scores well anyway.** Because good intake does real work. By the time a developer saw it, the affected users, the standard, the target number and the verification requirement were already written down.

**The catch, and it is a big one.** The issue carried an explicit instruction: only the accessibility tester may close this bug, after verification. That did not happen. A colleague asked the pull request author whether it could be closed, and then closed it as completed. The verification label arrived a week later, from a third person, attached to the comment "Looks good now" — with no measured ratio anywhere in the record. Closed first, verified after, by neither the named role nor in the stated order.

This case originally scored 11 out of 12 in our own write-up, as the corpus exemplar. Checking what actually happened to its one decisive control is what brought it down to 8 — and produced a better finding than the one it replaced.

## Bootstrap #42524 — 7 out of 12

**What broke.** This one exists because an earlier fix was merged without review. Bootstrap's one-time-password field had been rewritten to be more accessible (see #42500 below); the rewrite shipped two defects that, in the maintainer's own words, were "reported after merge" — you could not click a box to focus it, and retyping a digit shoved the others along.

**What happened next is the interesting part.** The fix for those defects introduced a third. An outside contributor tested the preview build on two iPadOS beta versions and found that tapping the field raised the on-screen keyboard and then dismissed it within a split second — making the component unusable on touch devices, in a component whose entire purpose was accessibility. The maintainer diagnosed it publicly, pushed a fix, and then wrote: *"Could you re-test on iPadOS 26/27 once the preview rebuilds? I don't have a device to confirm the keyboard now stays up."* The contributor re-tested and confirmed it the next day.

**Why it matters more than its score.** That exchange contains the whole recommendation of this project, arrived at by instinct. A maintainer hit a verification gap, said so publicly, routed it to someone who could close it, and got an answer inside a day. It also produced the strongest verification evidence in the corpus — named platform, named versions, named comparison browsers, observed behaviour, independent re-test.

**The catch.** Nothing made it happen. It depended on a maintainer thinking to ask and a contributor with the right hardware happening to read the thread. Nothing recorded the request as an outstanding obligation, and nothing stopped the parent pull request merging a week earlier without any of it.

## Bootstrap #42539 — 6 out of 12

**What broke.** In floating-label form fields, the input came before the label in the underlying markup, because a styling trick needed that order to animate. Screen readers read in markup order, so a user heard the field's value before hearing what the field was for.

**What happened.** The original reporter had tested with NVDA on Chrome and Windows and described exactly how to reproduce it. A maintainer rewrote the styling so the label could come first, and merged it about thirty-six hours later.

**Why the middle score.** The user impact is described precisely and the affected technology is named. But no standard is cited, nobody re-tested with a screen reader before it shipped, and there were zero reviews of any kind — despite a code-owner rule formally requesting one.

**The catch.** It merged into an unreleased development branch. The person who reported it was running a released version, and roughly fourteen and a half months after filing, still has the bug — while the issue is closed as "completed", with no comment written to them. The technique used in the fix had also been proposed by a community member in the issue thread over a year earlier.

## Bootstrap #42500 — 6 out of 12

**What broke.** Bootstrap's one-time-password field rendered as six separate boxes, one per digit. A screen reader announced six separate fields, and password managers could not autofill into them.

**What happened.** A maintainer rewrote it as a single real input with decorative boxes drawn over it, reasoned explicitly about two accessibility standards and anchored four in the rewritten documentation, and merged it fourteen hours later.

**Why the middle score.** The reasoning is the best in the corpus. What is missing is verification: the testing section lists 1,049 passing automated tests, clean linting and a successful build — and no assistive technology at all. Nobody opened a screen reader. Nobody reviewed it, because the author merged their own change.

**The catch.** Seven days later the same maintainer had to open #42524 to fix two interaction defects this change had shipped. This is the only place in the corpus where the cost of a missing review is visible rather than hypothetical. The concern had originally been raised by someone who said upfront that they were not an assistive-technology expert — and nobody more qualified ever appeared.

## Bootstrap #41607 — 4 out of 12

**What broke.** Bootstrap's modal dialogs put an invisible stop in the keyboard tab sequence — press Tab and you would land on nothing before reaching the close button. Trivial to ignore with a mouse; genuinely confusing if the keyboard is how you navigate. It was a regression: a user identified the exact patch release that introduced it, and the last version that worked.

**What happened.** A community contributor — not a maintainer — submitted a fix with a test. A maintainer labelled it `accessibility` within hours. It then received no review of any kind for about eleven months, and was finally closed, not because it was wrong, but because a rewrite had replaced that code entirely.

**Why it scores lowest.** Nobody ever evaluated it. There is exactly one comment on the pull request: the closing note, eleven months later, which never addresses whether the original defect still exists in the new implementation.

**The catch.** Four separate people engaged with this defect — the reporter, someone who independently confirmed it and identified the regression, the contributor who fixed it, and a fourth who added analysis six months later. The only maintainer actions in eleven months were a label and a closure. And compare the outcome to the two maintainer-authored fixes above, in the same project, in the same period, both merged inside a day and a half.

## Storybook #35321 — 4 out of 12

**What broke.** Storybook always declared its pages as English, no matter what language the content was actually in. Screen readers use that declaration to pick a pronunciation, so French content was being read aloud in an English voice.

**What happened.** A maintainer threaded a language setting through the whole rendering tree. An automated reviewer left nine substantive comments across three separate review passes, and they were genuinely good — it caught four real defects in how the language value propagated. The one human review was an approval with an empty comment body. The author then merged their own change and applied the "QA passed" label to it themselves.

**Why it scores low despite all that review.** Because code review and accessibility verification are different things, and only the first happened. The automated reviewer examined whether the mechanism worked. Nobody checked the thing that actually matters: does a screen reader now pronounce the content correctly? You cannot answer that by reading a diff. You have to render the page and listen. The author's own checklist even said "run your favourite screenreader" — phrased as a suggestion to the reviewer, with no sign anyone did.

**The catch, and the useful comparison.** Automated review also ran on the MUI case above — and there a human separately verified with VoiceOver. Same tooling, opposite outcome. The variable was never whether a bot reviewed; it is whether anybody rendered the thing and checked.

---

## What the seven suggest together


Seven cases can suggest mechanisms, not rates. These are claims that these failure modes exist and how they arise, not how often they occur.

**Nothing reached the mature band.** Scores run 9 down to 4, across four well-resourced projects. That ceiling is the headline finding, and it is harder to dismiss than a mixed scoreboard would be.

**Verification separates the corpus; standards citation does not.** The case with the best standards reasoning scored 6 and shipped defects within a week. The case citing no standard at all scored 9, because someone opened it with a screen reader first.

**Self-merge is the norm, not the exception.** Six of the six merged pull requests were merged by their own author. Two went further and self-certified — one applying its own "QA passed" label, the other enabling automatic merge before any review existed. The only case not self-merged is the one that was never merged at all.

**Code review is not accessibility verification.** Automated review is expanding and is genuinely useful on mechanism. It cannot establish what a screen reader announces, because that evidence lives in rendered output rather than in source. Where a human also verified, the outcome was the best in the corpus; where nobody did, it was among the worst.

**A control written as prose is not a gate.** The best-specified issue in the corpus carried an explicit rule about who could close it and when. Nothing in the platform enforced that rule, and it was bypassed within weeks by people acting in good faith and probably clearing a milestone.

**Who opened the pull request predicted whether it was reviewed.** Maintainer-authored fixes merged within a day and a half, unreviewed. The single outside contributor's fix was labelled correctly within hours and then waited eleven months for any response.

**Code-owner review requests went unanswered.** Five requests routed to a team via CODEOWNERS produced nothing at all. The one request sent to two named individuals got a response — including the only assistive-technology verification in the corpus. One instance, so a hypothesis rather than a finding, but a cheap one to test: naming a person may work where pinging a team does not.

**Merging is not shipping.** All three Bootstrap cases leave users of every released version with nothing: two fixes exist only in an unreleased branch, and the third was refused because that branch supersedes it. A rubric that stops at the merge event overstates how many of these defects were actually fixed for anybody.

### Honest limits

Seven pull requests is a documented method, not a statistical claim. They are recent, they are all in the JavaScript ecosystem, and they were selected because they were findable and readable — not at random. A different seven could tell a different story.

That is rather the point of publishing the rubric and the scores together. Anyone can disagree with a specific score — two of ours have already moved, and the criterion behind them was rebuilt because the corpus showed we were applying it inconsistently. Anyone can apply the same six questions to their own project's history and see what comes back. If you do, we would like to see it.

---

**Full case studies:** [`case-studies/`](case-studies/) · **Rubric:** [`review-rubric.md`](review-rubric.md) · **Cross-case patterns:** [`signals/review-patterns-v0.2.md`](signals/review-patterns-v0.2.md)
