# Candidate screening for case studies 8–11

Screened 23 October 2026 for [issue #9](https://github.com/ecogetaway/oss-accessibility-inclusion/issues/9). This is a candidate pipeline, not a set of completed scores. I checked each pull request's description and available discussion/review timeline. The commit links below pin the examined snapshot. Review discussions can continue after that snapshot, so recheck before writing a case study.

## Shortlist

| Rank | Candidate | Why it is a good case | Evidence read |
| --- | --- | --- | --- |
| 1 | [Microsoft Bot Framework Web Chat #5923](https://github.com/microsoft/BotFramework-WebChat/commit/f23e3c3c8f1f665e0fd4120c031517d0ba8a7225) | Clear reviewed-and-rejected-on-merits example. A maintainer questioned whether the reported issue was real, compared announcement strategies in a Web Chat test page, then closed the PR after reporting that Narrator with Edge did not distinguish the proposed strings. Useful counterexample to treating a requested accessibility change as automatically beneficial. | **Strong.** Detailed author and maintainer discussion, a changes-requested review, explicit AT/browser and observed outcome, plus a clear closure rationale. The reviewer notes a possible `doc-noteref` path, but this PR does not establish that as a confirmed fix. |
| 2 | [Microsoft Fluent UI #36643](https://github.com/microsoft/fluentui/commit/5dd8258484567ae8bb8ba21ac7256a61024b080f) | Strong review-process case about carousel announcements and focus. A reviewer cited the WAI-ARIA APG, challenged moving focus, and the author revised the approach; subsequent feedback found a stale-announcement edge case that was also addressed before merge. | **Strong.** Multiple human comments, reviewer guidance, a review decision, implementation revisions and regression-test discussion are visible in the PR thread. AT observation is less explicit than in #5923. |
| 3 | [OVH Design System #1143](https://github.com/ovh/design-system/commit/b36404e62938886052373769b41b8067f9ca4ea8) | Practical component-library case spanning form names, tree selection semantics, translated controls, popovers and sortable table headers. A change request and approval are recorded before merge. | **Good.** The PR describes scope and tests; review state changes are visible. The thread is brief, so the reason behind each decision may need checking in inline comments and linked audit context. |
| 4 | [WordPress #13671](https://github.com/WordPress/wordpress-develop/commit/4221e09bd0ac9ec68a13b02271dad7e7a5ead40c) | A high-discussion case for how an accessibility proposal evolves through review. It received an approval, later a changes-requested review about invalid ID handling, and was ultimately closed unmerged. | **Good, with an outcome caveat.** The thread has substantial reviewer comments and a recorded review request, but the closure should not be described as rejection on the accessibility merits without further evidence. |
| 5 | [django-filer #1653](https://github.com/django-cms/django-filer/commit/71c4c4d7595e1b82afba0ce38b6d7bf6bcca515f) | Broad admin workflow case covering keyboard interaction, announcements, errors and focus management. Useful to contrast a maintainer approval with automated review signals. | **Good.** The PR includes concrete changes and test claims; a maintainer approval and bot review history are visible. Verify the underlying diff and distinguish human review from automated comments when scoring. |

## Other candidates screened

| Candidate | One-line reason it is instructive | Enough recorded evidence to score? |
| --- | --- | --- |
| [Gephi #3337](https://github.com/gephi/gephi/commit/49fe8e6b85c7e2d9a1b91d5ef6348c70281ce179) | Large desktop UI sweep names keyboard, accessible-name and label changes, while explicitly listing gaps and saying it was not tested with a screen reader. | **Partial.** Strong author account and clear outcome, but no reviewer discussion; a low review-confidence score would be evidence-based. |
| [OpenCloud Web #3820](https://github.com/opencloud-eu/web/commit/0243f725e8d2966385edb65c49b1b0842f1a35bf) | Component-level WCAG fixes include select relationships, table sorting names and result-count announcements, with named build and test checks. | **Partial.** Detailed PR description and one approval are present, but the recorded conversation is sparse. |
| [East Coast Enduro Association UI #421](https://github.com/east-coast-enduro-association/ecea-ui/commit/52aa087d8519db0196832dcbc4b471417bc03882) | Small association site's carousel pause behavior, reduced motion, duplicate content and skip link make a focused UX case. | **Partial.** Detailed description and verification claims, but no formal reviews; little evidence of how reviewers evaluated the claims. |
| [DMP Registry Frontend #14](https://github.com/dylan-mccormick/dmp-registry-frontend/commit/a507d4d8670f87ec82f9a0b095d98328dc8c7ccc) | A broad registry workflow audit reports keyboard, contrast, modal and axe coverage, while naming real screen-reader and zoom checks that remain outstanding. | **Partial.** Useful testing-scope transparency, but the PR has no recorded human review or discussion and was merged very quickly. |
| [Slint Tree View #3](https://github.com/stdex/slint-tree-view/commit/d174c14cf48112ca24cc99d447cce617e8f5e75d) | The author openly identifies an unresolved, untranslated expanded/collapsed announcement limitation in a screen-reader support change. | **Weak.** The limitation and linked issue are clear, but the thread is very short and has no recorded reviewer engagement. |

## Scope and cautions

- None of these repositories or pull requests duplicates the seven existing case studies listed in `case-studies/README.md`.
- The shortlist spans a major technology vendor, a foundation-led project, a commercial design-system project, and community-maintained projects. These are practical context labels, not a formal governance audit.
- Only Microsoft Bot Framework Web Chat #5923 currently meets the requested rejected-on-merits pattern from the evidence checked. The conclusion is grounded in the PR author's closing comment and should be re-verified against the thread when the case study is written.
- A candidate's PR description is evidence of what its author claimed, not independent proof that a fix works. The case-study author should inspect the diff, linked issue and every human review before scoring.
- AI-generated summaries or bot reviews should not be counted as human reviewer engagement.

## Sources

Each candidate's pinned commit link opens the examined pull-request snapshot. The surrounding PR page contains the discussion, reviews, timeline, and linked issue where present. No claim here relies on a third-party summary.
