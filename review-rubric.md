# Review Rubric

Each case study is scored against six criteria, 0–2 points each (12 points total). The rubric measures how the *review process* handled the PR — not whether the underlying accessibility fix was technically correct.

| Score | Meaning |
| --- | --- |
| 0 | Absent |
| 1 | Partial / implicit |
| 2 | Explicit and complete |

## Criteria

### 1. User impact stated
Does the PR description or discussion name the affected users and the task they couldn't complete? ("Screen-reader users can't tell which field a value belongs to" vs. "fixes a11y issue.")

### 2. WCAG mapping
Is the change tied to a specific WCAG success criterion (e.g. 1.3.1 Info and Relationships, 4.1.2 Name Role Value) by the author, a reviewer, or the linked issue — anywhere in the thread?

### 3. AT testing evidence
Is there a record of testing with actual assistive technology — which AT, which version/OS, and what was observed — either before or after the fix?

### 4. Reviewer confidence signal
Did a reviewer engage substantively with the accessibility claim (e.g. verified the fix, asked a probing question, cited a spec) as opposed to a rubber-stamp approval or a self-merge with no review at all?

### 5. Direct language
Does the discussion name affected users specifically (e.g. "NVDA users," "keyboard-only users") rather than a generic reference to "accessibility" or "a11y issues"?

### 6. Outcome clarity
Is it clear from the record why the PR landed, stalled, or was rejected — i.e. would a future contributor understand what happened and why, without guessing?

## Score bands

- **10–12** — Review process an a11y-mature project would recognize as normal.
- **6–9** — Partial infrastructure: some signals present, but relies on individual expertise rather than repeatable process.
- **0–5** — No structured a11y review occurred; outcome depended on who happened to touch the PR.

## How to apply

For each case study:
1. Read the PR description, all comments, and linked issues.
2. Score each criterion using the PR thread as the only evidence source — do not infer intent that isn't recorded.
3. Record the score in the case study's Rubric Scores table with a one-line justification per row.
4. Total the score and place it in the score band.
