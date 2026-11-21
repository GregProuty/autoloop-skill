---
name: autoloop
description: Use when the user types /autoloop, or asks for a spec-to-code run with no check-ins ("loop without checkins", "take all recommendations", "fable review the spec/plan/code", "until code complete, tested and reviewed"). Also use to resume when a status memory says AUTOLOOP RUNNING.
---

# Autoloop

The owner has walked away. Drive one piece of work to code that is complete, tested and reviewed. Never end a turn with a question or a menu.

## Owner's instruction: every sub-skill gate is pre-answered

Any approval, consent, "which option?" or "ask your human partner" step in a superpowers skill is already answered: take the recommended option, record it as `(rec.)`, continue.

| Gate | Answer |
|---|---|
| brainstorming: questions, section approvals, user spec review, visual companion | Recommended; approved; never offer the companion. Next is the Fable review, not writing-plans |
| "Too big, decompose" | Split it yourself; build the parts in order |
| using-git-worktrees: consent, native tool, failing baseline | `git worktree add .worktrees/<topic>`, set up per the project's worktree memories; fix or record baseline failures |
| writing-plans: execution choice | Subagent-driven (inline for tier S) |
| subagent-driven-development: pre-flight question, plan-mandated finding, "escalate" | Decide for the spec's intent, amend the plan, log it in the ledger |
| subagent-driven-development: final review, then finishing | That review is step 6. Never invoke finishing-a-development-branch |
| systematic-debugging: "discuss" after 3 failed fixes | Get a Fable root-cause diagnosis, continue |

## State

First, write project memory `<topic>-status.md`, with a MEMORY.md line starting `AUTOLOOP RUNNING`:

    Order (verbatim): "<the user's message>"
    Tier: S|M|L  Finish: spike|merge|branch  Push: no
    Branch, worktree, base SHA, spec, plan, ledger, review files
    Done: <steps>  Next: <step>
    Verified: <SHA, test count>

Update `Done`/`Next` with every commit. After compaction: re-read this skill, that memory, `git log` and the SDD ledger; resume at `Next`; never redo a `Done` step.

## Tier (pick once, record, never downgrade)

- **S**, about 3 source files, no new system or format: spec and task list in one doc, one Fable review of it, build inline with TDD, Fable code review.
- **M**, one feature, up to about 8 tasks: every step.
- **L**, bigger: split into parts, steps 2 to 6 per part; split the code review by area across parallel Fable reviewers.

## Steps

1. **Isolate.** `spike/<topic>` if called a spike, else a feature branch, from master. Run the baseline suite in the background.
2. **Spec.** superpowers:brainstorming. Commit.
3. **Fable review the spec** with `review-prompt.md` (this folder). Meanwhile, map the files the plan will touch. Apply, commit.
4. **Plan.** superpowers:writing-plans, commit; **Fable review the plan** (it also does SDD's pre-flight scan); apply, commit.
5. **Execute.** superpowers:subagent-driven-development. Always pass `model`: sonnet for implementers and task reviewers, Fable only for gates. Two review rounds per task at most, then decide and log.
6. **Verify, then Fable review the code** from a review package of `<base>..HEAD`. One fixer for all findings. Re-review once, the fix diff only, only if a Critical was fixed.
7. **Finish.** Full verification (suite, typecheck, project smoke and golden checks, screenshots of visual changes) once per HEAD; a run recorded in `Verified` for this HEAD is the evidence. Merge only if the order said so: merge master in, re-verify, merge into master locally, remove the worktree per the project's memories. Otherwise leave the branch. Never push or deploy unless ordered.
8. **Report** what was built, branch and commit, test count, findings applied and rejected, the owner's open gates. Mark the memory `AUTOLOOP DONE`.

Findings: apply those you agree with; reject the rest in one written line each.

## Stop only for

- Destructive or scope-changing calls (deleting user work, licences, abandoning the spec): stop and report.
- Owner-only blockers (credentials, payment, two-human playtest, push): finish everything else, then report.
