# autoloop

A Claude Code skill for the "I'm leaving this running" loop: write the spec, take every recommendation, Fable review the spec, write the plan, Fable review the plan, execute it, Fable review the code, and finish, with no check-ins until the code is complete, tested and reviewed.

It builds on the [superpowers](https://github.com/obra/superpowers) skills (brainstorming, writing-plans, subagent-driven-development, using-git-worktrees) and pre-answers every approval gate in them so the run never stalls.

## Features

- Size tiers (S / M / L) so small changes take a short path
- State in a project memory (`AUTOLOOP RUNNING`, `Done` / `Next`) so a long run resumes after context compaction
- A bounded Fable review prompt (`review-prompt.md`): at most 10 findings, concrete scenario plus exact fix
- Sonnet for implementers and per-task reviews, Fable only for the gates
- Never pushes or deploys unless the order says so

## Requirements

- Claude Code with the superpowers plugin
- Access to the Fable model (or edit the skill to name another reviewer model)

## Install

```bash
git clone https://github.com/GregProuty/autoloop-skill ~/.claude/skills/autoloop
```

## Use

```
/autoloop build the extinguisher spike, merge when done
```

or say you're leaving it running and want the full spec-plan-build loop without check-ins.

MIT license; see [LICENSE](LICENSE).
