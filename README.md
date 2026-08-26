# claude-dev-template

⚠ **A workflow for handing work to an AI and being able to say afterwards what was actually shown.**

⚠ **This repository holds only the part that reproduced in two unrelated domains.**
⚠ **Everything that only ever worked in one of them was left behind, on purpose** (§3).

```
issue-ready  ->  owner decision gate  ->  ready-for-ai  ->  loop-controller
                                                                |
              inner verify  ->  final verify  ->  mutation / negative check
                                                                |
                                       change-review  ->  PR  ->  CI  ->  owner merge
                                                                |
                                          debt outside scope leaves as its own issue
```

---

## 1. Why now, and not earlier

⚠ **With one project, a shared template is a guess.** ⚠ **The same shape running in two
projects that share no domain is evidence.**

The two are `hidetzu/konjaku` (web / UX / product, where the right answer is arguable) and
`hidetzu/tcpip-stack` (a user-space TCP/IP stack, where the right answer is pinned down by an
RFC and by what appears on the wire). ⚠ **A rule that holds at both ends is a rule about the
workflow, not about the domain.**

### ⚠ What was measured, and how

⚠ **Compared on 2026-08-26**, working trees of both repositories, file by file.
⚠ **This is a comparison of two repositories, not a claim about any third one.**

| What was compared | Result |
|---|---|
| `.claude/settings.json` | ⚠ **Byte-identical** |
| `.claude/hooks/*.mjs`, `telemetry-dir.mjs`, `tools/telemetry-eval.mjs` | ⚠ **Identical once comments are stripped**, except user-facing strings and one env var name. `telemetry.mjs`: 1 differing line of code. `ask-slack.mjs`: 17 |
| `issue-ready`, `issue-work`, `loop-controller`, `change-review`, `context-maintainer` | ⚠ **Same sections, same order, same verdict vocabulary.** The prose is one language in each (`konjaku` Japanese, `tcpip-stack` English), so a line-diff shows near-total difference and says nothing |
| `verify` — the `PASS` / `FAIL` / `NOT-VERIFIED` block, `Regression guard`, `Mutation check` | ⚠ **Same shape, clause for clause** |
| `verify` — the entry points, their costs, their partial-run flags | ⚠ **Nothing in common.** `npm run check` / `render` on one side, `make check-static` / `-real` / `-foreign` on the other |
| `CLAUDE.md` | ⚠ **Same §1–§9 numbering and the same subject per section.** ⚠ The examples inside are the domain's, every time |

⚠ **That last pair is the whole design of this repository.** ⚠ **The contract reproduced; the
commands did not.** ⚠ **So the contract is here and the commands are not** (§3).

---

## 2. What is here

```
CLAUDE.md                        skeleton. ⚠ every FILL IN is a claim only the project can make
.envrc.example                   the Slack credentials ask-slack needs. ⚠ copy to .envrc, never fill this one in
.claude/
  rules/
    README.md                    the index, and ⚠ constraint vs. learned pitfall
    evidence.md                  ⚠ what may be said to have been observed. the one file that never bends
    verification.md              the three tiers, partial runs, PASS / FAIL / NOT-VERIFIED
    owner-decisions.md           decide yourself vs. ask, ready-for-ai
    git.md                       commits, permission, forbidden operations, what never goes public
  skills/
    issue-ready/                 can this issue be handed over at all
    issue-work/                  issue -> plan -> implement -> verify -> review -> PR
    loop-controller/             one issue, one owner approval, ⚠ merge only on fully green CI
    change-review/               is the change inside scope and inside the rules
  hooks/                         ask-slack (AskUserQuestion -> Slack -> the answer back), telemetry
  tools/docs-check.mjs           holds the documents to what they say about themselves.
                                 ⚠ --list names the cases, --only= runs one
  tools/telemetry-eval.mjs       reads the telemetry. ⚠ observation only, it scores nothing
  settings.json                  wires the hooks up
docs/
  SPEC.md                        skeleton. what may be claimed
  adr/README.md                  what belongs in an ADR and what does not
```

⚠ **`.claude/telemetry/` never enters git** — see `.gitignore` and `.claude/telemetry-dir.mjs`.
⚠ **The `.gitignore` line and the code that builds the path are two copies of one string**, and
⚠ **only a static check can hold them together.** That check is
[`.claude/tools/docs-check.mjs`](.claude/tools/docs-check.mjs), case `telemetry-ignore-line`;
⚠ **it reads the name out of the code and requires `.gitignore` to carry that exact line**,
⚠ **so renaming the directory in one place alone fails.**

```
node .claude/tools/docs-check.mjs            every case
node .claude/tools/docs-check.mjs --list     name them without running (⚠ loads nothing)
node .claude/tools/docs-check.mjs --only=links
```

⚠ **It announces its own count, and the count is never written down** (`rules/evidence.md`).
The other two cases hold documents to rules that would otherwise be promises: every relative
link in the markdown resolves, and ⚠ **no count is written into `docs/SPEC.md`.**

⚠ **This is not this project's verification.** ⚠ **That is `.claude/skills/verify/SKILL.md`, and
every project still writes its own** (§3). ⚠ **These three cases assert only what this template
can claim about any copy of itself.**

---

## 3. What is deliberately not here

⚠ **A gap named here is a decision.** ⚠ **An unnamed gap is just something not done yet.**

| Not here | Deliberate? | Why |
|---|---|---|
| ⚠ **`.claude/skills/verify/SKILL.md`** | ⚠ **yes** | ⚠ **The contract reproduced, the commands did not** (§1). The contract is `rules/verification.md`; ⚠ **every project writes the skill that names its own entry points** |
| A CI workflow | yes | ⚠ **Which tiers CI can run is a property of the machine**, and it differed between the two. A shipped workflow would be a claim about a runner nobody measured |
| Issue and PR templates | yes | ⚠ **`issue-ready` §6 says not to push its nine sections onto outside reporters.** A shipped template would do exactly that |
| `context-maintainer` | ⚠ **no** | ⚠ **Not a rejection.** It exists in both repositories with the same four sections, ⚠ **so it has the same grounds as the four that are here** — it was simply outside what v0.1 was scoped to. A candidate for v0.2 |
| konjaku's `css.md`, `components.md`, `domain.md`, `ui-ux-review`, `product-discovery` | yes | One domain only |
| tcpip-stack's `c.md`, `layers.md` | yes | One domain only |
| A `LICENSE` | ⚠ **no** | ⚠ **Not chosen yet.** ⚠ **Until it is, nobody outside can rely on being allowed to copy this** |

⚠ **Nothing in this repository claims to have been proven anywhere except in those two projects.**
⚠ **A third project adopting it is a third data point, not a confirmation.**

---

## 4. Using it

1. Copy `CLAUDE.md`, `.claude/` and `docs/` into the project.
2. Fill in every `FILL IN`. ⚠ **They are not optional** — each is something only this project
   knows, and a skeleton left unfilled reads as though it were answered.
3. Write `.claude/skills/verify/SKILL.md` against
   [`rules/verification.md`](.claude/rules/verification.md): ⚠ **name the three tiers, the entry
   points, how to run one case, and how to count without running.**
4. Add the rule files this domain needs, and list them in
   [`rules/README.md`](.claude/rules/README.md). ⚠ **Each states its grounds.**
5. ⚠ **Leave `CLAUDE.md` §9 empty.** ⚠ **It fills up with what this project pays for, and
   nothing else** — ⚠ **never with a row carried over from here.**

⚠ **The hooks need `node`.** `ask-slack.mjs` reads its Slack credentials from the environment and
⚠ **falls back to asking in the terminal when they are absent** — ⚠ it never blocks the work.
[`.envrc.example`](.envrc.example) names the three variables; copy it to `.envrc` (or `.env`) and
fill them in there — ⚠ **`.envrc` and `.env` are gitignored and `.envrc.example` is not.**
`.claude/hooks/slack-doctor.mjs` says which part of the setup is missing.

---

## 5. ⚠ What sending it back looks like

⚠ **This repository is downstream of two working projects, and it stays downstream.**

- ⚠ **A rule earns its place here by holding in both**, ⚠ **never by sounding general.**
- ⚠ **A pitfall belongs to the repository that paid for it** (`CLAUDE.md` §9).
  ⚠ **It reaches here only as a constraint with its grounds named**, ⚠ **and the row stays where
  it happened.**
- ⚠ **When a project has to fight the template to do the right thing, the template is wrong.**
  ⚠ Fix it here, and say which project it broke in.
