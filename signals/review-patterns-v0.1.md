# Signals v0.1 — superseded

This document has been superseded by [`review-patterns-v0.2.md`](review-patterns-v0.2.md), which covers seven case studies instead of six and reflects the full re-verification carried out on 2026-07-29.

Three things changed materially, and are recorded here so the revision history stays legible rather than silently rewritten:

- **Pattern 4 was inverted.** v0.1 credited VS Code #324192 with a decisive process control — a rule that only an accessibility tester could close the issue after verification. The rule exists, and it was bypassed: the issue was closed as completed by a different person, and verification arrived a week later with no measured result. The replacement pattern is that a control written as prose is not a gate.
- **Pattern 2 was much larger than v0.1 recorded.** Three self-merges became six of six merged PRs.
- **Two scores fell.** VS Code #324192 from 11/12 to 8/12 and MUI #48572 from 10/12 to 9/12, after criterion 3 was given explicit bands. A seventh case, Bootstrap #42524, was added at 7/12.

The superseded text is preserved in this file's git history.
