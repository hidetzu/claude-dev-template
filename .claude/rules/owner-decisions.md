# Owner decisions

⚠ **`MUST` = required, `SHOULD` = default, `MAY` = optional.**

⚠ **This file is the owner of `CLAUDE.md` §7-1 and §7-2.** ⚠ **Never restate them there.**

## Grounds

⚠ **Stalling costs more than deciding.** ⚠ **But a decision the owner cannot walk back costs
more than either.** ⚠ **The line between them is the only thing this file draws.**

## Decide yourself vs. ask

⚠ **The default is: decide, and carry it through to the end.**
Ask only where **being wrong cannot be walked back**.

| Decide yourself | Ask |
|---|---|
| Implementation order, how to split it, where tests go | ⚠ **Anything a human reads** on screen or in output |
| What to measure and how | ⚠ **When the scope moves** (crossing `Non-goals`) |
| A bug with exactly one sensible fix | ⚠ **When what may be claimed changes** (`docs/SPEC.md`) |
| Adding docs, comments, tests | Two presentable options that **measurement cannot settle** |

- MUST: Ask with **`AskUserQuestion`**. ⚠ **Never bury the question in prose** (it gets missed).
  ⚠ **With `.claude/hooks/ask-slack.mjs` configured, this asks in Slack and receives the answer back.**
- MUST: ⚠ **Nothing else goes to Slack** — no progress, no completions, no failures
  (⚠ **they would bury the one thing that needs an answer**).
- MUST NOT: ⚠ **Never ask what measuring would settle.** Measure first.
- MUST: ⚠ **Asking stops the work.** Finish everything that does not depend on the answer
  **before** asking.
- MUST: ⚠ **Record what was asked.** Once decided, put the reason in `docs/adr/`.

## ⚠ An owner decision outranks your judgement

- MUST: ⚠ **Copy `Owner Decisions` out of an issue verbatim**, and never change one on your own
  judgement.
- MUST: ⚠ **A later comment overrides the issue body.** ⚠ **A decision made mid-flight often
  exists only in a comment.**
- MUST: ⚠ **When body and comment conflict and you cannot tell which is authoritative, ask.**
- MUST: ⚠ **When the issue, the spec, the ADRs and the code disagree, do not decide which is
  right.** ⚠ **Return that a human must decide.**

## ⚠ `ready-for-ai`

⚠ **This is not a priority label.** It marks "an AI can carry this to the end without a human
deciding mid-way".

- MUST: ⚠ **Only a human applies it.** The AI goes as far as producing the verdict
  (`.claude/skills/issue-ready/SKILL.md`).
- MUST NOT: ⚠ **Never apply it, and never remove it.**
- MUST: ⚠ **The label is an entry condition, not a guarantee that it can be implemented.**
  ⚠ **Bodies and comments change after a label is applied, and labels get applied by mistake** —
  ⚠ **so re-run the gate every time.**
- MUST: ⚠ **Even with the label, permission for `git push` and merge is taken every time**
  ([`git.md`](git.md)). ⚠ **The one exception is the Loop Controller's**, and it is written out
  in full there.

## ⚠ Rewriting an issue

⚠ **The AI may rewrite an issue body.** ⚠ **Closing it, and labels, stay with the human** (above).

⚠ **Rewrite only what you measured.**

| May | ⚠ May not |
|---|---|
| Add the date and the PR to a finished item | ⚠ Change `Goal` / `Scope` / `Out of Scope` / `Owner Decisions` |
| Append a correction to a statement that is no longer true | ⚠ Delete or rewrite the original words |
| Note that a reference is gone | ⚠ Fix by guesswork (⚠ if you have not measured it, leave it) |
| Tick a box (⚠ only when measured) | ⚠ Close it |

⚠ **Never delete. Append.** ⚠ **Deleting the original words loses why they were written.**

⚠ **Not because it is old — because it is no longer true.**
⚠ **Time is not a reason to touch an issue.**

⚠ **What we stepped on**: ⚠ **we first reached for a periodic review — look over the issues
every N days.** ⚠ **The practice around auto-closing stale issues argues against it:
closing on time alone throws away context, silence is not low value, and it hides the triage
problem rather than solving it.** ⚠ **Review by time, and you gain a reason to touch the
issues that are still correct.**

### ⚠ Collect the appends under `## Updates`

⚠ **The body is the record of the time it was written.**⚠ **`Updates` is the diff against now.**

```text
## Updates

### <date> — <state>        ⚠ partly solved / solved / the fact changed / the reference is gone

<what you confirmed>        ⚠ with the PR. ⚠ with the numbers when you measured

The body's "<the passage>" stays as the record of when it was written.
⚠ But as of now, <the fact>.

Unresolved:
- <what is left>
```

- MUST: ⚠ **Newest on top** (⚠ so the current fact reads first).
- MUST: ⚠ **Name the passage in the body.** ⚠ **Without it a reader trusts the body**
  (⚠ they cannot tell which part is stale).
- MUST: ⚠ **Keep the unresolved list.** ⚠ **A half-solved issue is not a solved one.**

⚠ **Without this, a long-lived issue collects corrections until the current fact is unreadable again.**

### ⚠ When to look

⚠ **Not on a clock.** ⚠ **At the seams of the work.**

```text
issue-ready     ⚠ the one issue you are about to take on (§4-2 there)
change-review   ⚠ the issue this PR touches, when a partial fix cannot carry `Closes`
```

⚠ **The other open issues are not looked at.**
⚠ **An issue nobody reads does no harm by being stale.** ⚠ **The harm is believing it while reading.**
⚠ **Looking at all of them turns a periodic review into a review pinned to a seam — the same thing.**

⚠ **This leaves a hole, and it is left open on purpose**: ⚠ **an issue that never reaches
`issue-ready` is never looked at.** ⚠ **Closing that needs a human step** (⚠ check the body
when applying the label). ⚠ **No AI-side mechanism fills it.**

