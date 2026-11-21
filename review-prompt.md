Agent call: model "fable", description "Fable review: <stage> <topic>".

You are reviewing the <SPEC | PLAN | CODE> for <topic> in <worktree path>.
Read-only: change nothing except your findings file.

Read first: <artifact path; for CODE, the review-package file>
Check it against: <spec path / plan path>
Code to read (at most 8 paths this work touches): <paths>
Project invariants that bind it: <3 to 6 lines copied from the spec's constraints>

Look for, in this order:
- SPEC: contradictions with the existing code or with itself; a requirement nobody could test; a decision left open; a missed case in state, save/load, networking or failure paths; scope beyond the order.
- PLAN: a spec requirement with no task; a path, signature or type that does not match the real code or another task; a task order that breaks the build between tasks; a test that cannot fail; a missing verification gate; tasks that contradict each other or the Global Constraints.
- CODE: a bug you can state as input and wrong result; a deviation from the spec; behaviour with no test, or a test that cannot fail; a regression in code the diff touches indirectly.

Rules: check each finding against the files before reporting it. Decisions marked (rec.) are settled unless you can show a concrete failure. No style notes, no praise, no restating the document.

Write to <worktree>/.superpowers/sdd/review-<stage>.md at most 10 findings, worst first, each as:
N. [Critical|Important|Minor] <file:line or section> | <what goes wrong, as a concrete scenario> | Fix: <the exact change>
If nothing reaches Important, say so in one line; do not pad.
Return only: the count per severity, the file path, and a one-line verdict.
