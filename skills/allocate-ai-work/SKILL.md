---
name: allocate-ai-work
description: Builds an allocation ledger for one concrete workflow before you hand it to AI, or when you review one already handed over. Splits each step into four stages (gather, analyse, decide, act), sets an automation level for each stage from two questions (can an error here be undone? does it travel on before anyone notices?), names the work the person still has after handover, a concrete check, and who takes over when it goes wrong. Each row cites its basis in the human-automation research literature with a verification status and link. Use when asked how far to automate a workflow, what an AI agent may do on its own, where human approval belongs, or whether an existing automated workflow is set too high. Not for rating people, not for choosing tools, and not a safety case for regulated work.
---

# Allocate AI Work

Decide, stage by stage, how far a workflow is handed to AI, and write the decision down so it can be checked and revisited.

"Should we automate this?" treats automation as one switch. It is not: the same workflow gathers information, analyses it, decides, and acts, and each of those stages can sit at a different level. A higher level is a trade, not an upgrade. And the useful question is not "is the AI better at this step" but "once this step is handed over, what is left for the person, and can they still take over when it fails".

The ledger this skill produces is a proposal. The workflow's owner adopts or changes it. The skill never changes the settings of a running system.

## When to use

- Before handing a workflow, or part of one, to an AI agent or an automated pipeline.
- Reviewing a workflow that already runs with AI, to see where it is set higher or lower than the reasons support.
- Deciding where a human approval step belongs.

## When not to use

- Rating how well a person uses AI. The ledger is about a workflow, not a person.
- Choosing between tools or vendors.
- Safety-critical or regulated work. Follow your domain's standards; this ledger can sit beside them, not replace them.
- A vague brief ("use AI more"). Ask for one concrete workflow first.

## Inputs

1. **Workflow**: a name and its steps, 3 to 12 of them. More than 12: split it into two workflows.
2. **Who carries the result** of each step: whose problem it is if the step is wrong.
3. **What an error actually costs** at each step: money, time, or credibility with people outside the workflow.
4. **Current practice** for each step, if the workflow already runs: a person does it, AI does it, or both.

If the steps or the costs are unclear, ask one question to pin them down before Step 1.

## The level scale

| Level | Name | The automation | The person |
|---|---|---|---|
| 0 | Manual | does nothing | does the stage |
| 1 | Suggest | alerts or recommends | does the stage |
| 2 | Prepare | does the stage's work, but a person reviews the result before it is used or takes effect | reviews, then uses or discards the result |
| 3 | Act, undoable | does the stage and its result takes effect without a person reviewing it first; only results that can be undone; leaves a receipt for each | checks receipts by sample; undoes what is wrong |
| 4 | Act unattended | as level 3, and no one is present when its result takes effect: it starts itself on a schedule or an event, or another program or an AI agent starts it and leaves it running | reads its reports; checks by sample |

Two things decide the level: whether a person reviews the result before it takes effect (2 versus 3), and whether anyone is present when it does (3 versus 4). A job that only prepares work for a person stays at level 2 even when it starts itself on a schedule.

What starts a job does not decide 3 versus 4; presence does. A background process that an AI agent launches and leaves running (a waiter, a watcher, a retry loop) is at level 4 when its results take effect while the person is away, even with no schedule anywhere. A job the person starts by hand and stays with until its result has taken effect is at level 3. Presence means the person who answers for the stage; an AI agent that is still running does not count.

**Who is "the person".** The person is the human who answers for the stage. If an AI agent performs a stage on that person's behalf (reviews a result, decides, sends a reply), that is automation of the stage, rated like any other, even when the person is nearby.

This five-level scale is a simplification of the ten-level scale of Sheridan and Verplank (1978), applied per stage as in Parasuraman, Sheridan and Wickens (2000). The folding into five levels is this skill's, not theirs.

## Rules

1. **Decide stages, and actions that cannot be undone, never go above level 1.** The automation may recommend; a person decides and acts.
2. **Every level has a reason**: the answers to the two questions in Step 2. A level without a reason drifts.
3. **A level is changed by a person, on a date.** Never let the automation raise or lower its own level. A system that switches itself has taken the decision away from the person who answers for it.
4. **Every ledger has a review date.** Workflows, tools and error costs change; levels set once go stale.

Rule 1 and the two questions are a working rule from the studio that wrote this skill, based on one documented case. They are not part of the published level-of-automation models, and the ledger header says so.

## Workflow

### Step 1: Split each step into stages

| Stage | What happens |
|---|---|
| Gather | finding and collecting the information the step needs |
| Analyse | filtering, comparing, computing, drafting |
| Decide | choosing what to do among the options |
| Act | carrying out the choice: sending, publishing, paying, changing a record |

Not every step has all four. List only the stages that exist; if a step has none of a stage, leave it out.

Sorting or filtering by fixed rules that a person wrote (a threshold, a pattern list) is Analyse. Choosing among options in a way that someone must answer for is Decide.

### Step 2: Two questions set a ceiling

For each stage ask:

- **Q1. If this stage gets it wrong, can the error be undone?** Say by whom, how, and up to what point.
- **Q2. Does an error here travel on** to the next step, or out to people outside the workflow, before anyone would notice?

| Situation | Ceiling |
|---|---|
| Decide stage | 1 |
| A stage that speaks or commits for a person: sends, publishes, pays, signs | 1 |
| Error cannot be undone | 1 |
| Error can be undone, but travels on before anyone would notice | 2 |
| Error can be undone and does not travel | 3 |
| As above, and a missed or wrong run would be reported by something that runs without a person (an alert, a watchdog, a failure report) before the next run adds to it, or, for a one-off run, before its result is relied on | 4 |

Judge Q2 with the following stages at the levels you are recommending: if the next stage puts the result in front of a person before it is used, an error stops there and does not travel unnoticed.

**Mixed error classes.** Sometimes most errors at a stage can be undone and one class cannot: a step that files incoming documents, say, where a secret that slips through is copied into a history that cannot be cleaned. Do not give the whole stage one answer. Set a ceiling for each class and write both in the Level column, for example `4 (ordinary files) · 1 (files containing secrets)`. This holds only if something sorts each item into its class before the stage acts on it (a filter, a rule, a person); name it in the Reason. If nothing does, the lowest ceiling applies to the whole stage.

Items of the lower class that the sorting misses still run at the higher level. That is a residual risk, not a level: Rule 1 still holds for the class. Either lower the whole stage, or list the residual risk under Findings for the owner to accept or refuse by name.

The ceiling is the highest level the reasons allow, not a target. Recommend the ceiling unless Step 3 lowers it or the owner prefers lower; when you recommend below the ceiling, say why. Write the answers to Q1 and Q2 in the Reason column.

### Step 3: The residual work question

For every stage at level 2 or above, write what the person still does after handover, then ask:

- Will the person still see enough of the work to notice a failure and understand it?
- Will they still have the practice to do this stage by hand when the automation stops?

The work left behind is a different job from the work handed over: checking data someone else cleaned is not cleaning data. If either answer is no, lower the level by one, or add a takeover path that keeps the person in practice (for example, running the stage by hand on a fixed schedule).

### Step 4: Checks and takeover

- **Check.** For every stage at level 2 or above, write how it is checked and how often: what is looked at, how much of it, on what schedule, by whom. "Keep an eye on it" and "remember to check" are not checks: research on automation bias reports that telling people to verify does not reliably prevent it (a contested point). If `calibrate-ai-checks` is available to you, use it to set the rate; otherwise write a starting rate and the date to revisit it.
- **Takeover.** For every stage, write who notices when it goes wrong, who takes over, and at which step.

### Step 5: Basis and evidence

- **Basis**: cite 0 to 3 nodes from `references/basis-index.md` for each row, only where the node supports that row's reasoning. Copy all five fields exactly as listed: node, one-line intro, shelf, verification status, permalink. Do not reword them, add fields, or cite anything not in the index. If you have a reference lookup tool that returns these fields for a node, you may use it instead; fill only the fields it returns.
- **Evidence grade**: the strongest kind of evidence behind the row's judgment, one of: `theory` (the cited research supports the row's reasoning), `own test` (this allocation has run and its results were recorded), `external adoption`, `external results`. The two questions themselves are a working rule, declared once in the header; they do not lower or raise a row's grade. A new ledger is usually `theory`. Never write "proven" or "validated".

Typical basis by column:

| Row content | Node |
|---|---|
| Splitting into stages; setting levels | Levels of automation |
| "The AI is better at it" as the reason | Fitts list (MABA-MABA) |
| Residual work | Ironies of automation; Out-of-the-loop performance problem |
| Takeover | Out-of-the-loop performance problem; Situation awareness |
| Checks | Automation complacency & bias; Vigilance decrement; Trust in automation |
| Who changes the level | Adaptive automation |
| Workload of the person | Mental workload (NASA-TLX) |

### Step 6: Compare (only when reviewing a running workflow)

Add a **Now** column with the level the stage runs at today, read from the current practice with the same scale (an AI agent doing the stage for the person counts as automation). Then list the rows where Now is above the recommended level (set too high) or below it (room to hand over more). These are findings for the owner. Do not change the workflow; changing a level is the owner's decision (Rule 3).

## Output

Write the ledger in the user's language. Keep the basis fields exactly as they appear in the index.

```text
Allocation ledger: {workflow}
Scope: This ledger holds only for the workflow and the error costs listed here.
Criterion: The two questions that set the levels (can an error be undone? does it travel on?) are a working rule from the Trigpoint studio, based on one documented case. They are not part of the published level-of-automation models.
Review by: {date}
Status: proposal until {owner} adopts it.

| Step | Stage | Level | Reason (Q1 · Q2) | Residual work | Check | Takeover | Basis | Evidence |
|---|---|---|---|---|---|---|---|---|

Basis
[B1] {node} · {one-line intro} · {shelf} · {verification status} · {permalink}

Findings
- {step / stage}: now {n}, recommended {m}, because {reason}. (review only)
- Residual risk: {step / stage}, {class} items that {the sorting} misses run at {n}; one miss costs {cost}; {accepted by {owner} on {date} | for the owner to accept or refuse}; review by {date}.

Not covered: {anything the inputs did not settle}
```

Add the **Now** column after Level when reviewing.

## Anti-patterns

- One level for the whole workflow.
- Setting a level because the AI does the task better than a person.
- A level with no reason, or a reason that answers neither question.
- "Someone will watch it" as the check.
- Raising a decide stage above level 1 because errors have been rare.
- Letting the automation switch its own level.
- Citing a node that does not support the row, or inventing a basis field.

## Limits

- The research behind the stages, the residual work and the checks is published and cited. The two-question rule and the five-level folding are this studio's working rule, tested so far only on its own workflows. Details are in `VALIDATION.md` and `SOURCES.md` in the skill's repository, not in this installed folder.
- The ledger is as good as the error costs it is given. If the costs are guesses, say so in "Not covered".
