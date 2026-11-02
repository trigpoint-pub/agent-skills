---
name: calibrate-ai-checks
description: Sets how often, and how, a person checks the output of an AI step that prepares work or acts on its own, based on how reliable the step has been and what an undetected error costs. Splits checks into machine checks run on every item and human judgment checks taken as a random sample, states what the track record does and does not prove, keeps the sample rate from sliding to zero, and keeps a miss log so trust follows actual performance. Use when asked how much to review AI output, whether a spot-check rate is enough, how to stop rubber-stamping, or how to record AI errors to adjust review. Not a quality standard for regulated work and not a replacement for testing the automation itself.
---

# Calibrate AI Checks

Decide how much of an AI step's output a person checks, and keep that rate tied to what the step has actually done.

Two failure patterns pull in opposite directions. When a step has been reliable for a while, people check it less and less, until an error that nobody looked for goes through. When a step has produced too many false alarms or bad outputs, people stop trusting it even after it improves. The aim is neither more trust nor less: it is trust that matches the step's real reliability, and can tell the situations where the step is reliable from those where it is not.

Watching continuously does not solve this; detection falls off within a short time of watching. Telling people to verify is not a dependable fix either. What works better is a check that is scheduled, small, pushed to the person, and kept at a rate that never reaches zero.

## When to use

- An AI step drafts, extracts, classifies, or acts, and a person is supposed to review it.
- Review has become a click-through, or nobody knows how much is actually checked.
- An AI error got through and you want the review rate to respond.
- Setting the "Check" column of an allocation ledger (`allocate-ai-work`).

## When not to use

- Steps that decide, or act in ways that cannot be undone. Those should not be left to sampling: a person reviews each one, or the step is redesigned (see `allocate-ai-work`).
- Regulated or safety-critical review with its own required rates. Use those.
- Testing the automation before it runs. This skill sets ongoing human checks; it does not replace a test suite.

## Inputs

1. **The step**: what the AI produces, and at what level it runs (prepares for a person, or acts on its own).
2. **Volume**: how many outputs per week. One output that can be checked on its own is a **unit**.
3. **What counts as a defect** in a unit, as a short checklist.
4. **Track record**: how many units have been checked so far, and how many defects were found. "None yet" is a valid answer.
5. **Where an undetected defect ends up**: stays inside and can be undone; moves on to the next step or person; or reaches people outside, money, or something that cannot be undone.
6. **Cost of one check**, in minutes.

If the defect checklist is missing, write one with the user before anything else. A check without a definition of a defect is a glance.

**The unit** is an output that someone relies on. Outputs replaced by a newer one before anyone relies on them need no judgment check; count them, and check the one that is used. A unit too large to check whole (a long report, a batch of claims) is split: make the unit one claim or one section, and sample those.

**The checker** is usually a person, and may be an AI reviewer acting for one. An AI assistant working alongside the person counts as an AI reviewer unless the person checks each unit themselves. Checking a unit means opening the unit or its sources. A person who decides each unit from the AI reviewer's summary (accepts it, rejects it, sends it back) has not checked it: a summary that is consistent and cites its sources can still rest on a wrong premise, and reading it will not show that. Those decisions are not judgment checks, and they do not replace the person's re-check of the reviewer's verdicts below. Either way, the person who answers for the step's output sets and lowers the rate. An AI reviewer is itself an AI step: the person re-checks a random 1 in 10 of its verdicts, and at least one a week (a working default, like the rates in Step 3). A chain of AI reviewers is sampled at the last link the person relies on.

Some defects belong to a whole output rather than to one part of it (a missing section, a left-out item). Check those on every output, even when the parts are sampled.

## Workflow

### Step 1: Split machine checks from judgment checks

Go through the defect checklist and sort each item:

- **Machine checks**: anything a script, rule or schema can verify (format, required fields, counts, files present, links resolve, figures match their source). These run on every unit, automatically. They do not count as the human check, and their results are reported to the person, not just logged.
- **Judgment checks**: whether the content is right, fits the case, and says what it should. These are the ones a person samples.

### Step 2: Place the step in a cost tier

| Tier | An undetected defect | Example |
|---|---|---|
| A, contained | stays inside the workflow and is cheap to undo | a draft summary filed for internal reference |
| B, travels | moves on to a next step or person before anyone notices, or takes real time to undo | extracted figures fed into a report |
| C, external or irreversible | reaches people outside, money, a commitment, or cannot be undone | a message sent to a client |

A tier C step that acts on its own is outside this skill: send it back to `allocate-ai-work`. A tier C step that only prepares work gets a judgment check on every unit.

### Step 3: Set the starting rate

These are working defaults from the studio that wrote this skill, not figures from the cited research. Adjust them and write down why.

| Track record | Tier A | Tier B | Tier C |
|---|---|---|---|
| Fewer than 20 units checked | every unit | every unit | every unit |
| Any defect in the last 20 checked | every unit | every unit | every unit |
| 20 or more checked, no defect in the last 20 | eligible for 1 in 5 | eligible for 1 in 3 | every unit |

"Eligible" means the step may move to that rate when the owner decides so at a review (Step 6). Nothing moves to a lower rate on its own. If the record does not say where in the last 20 a defect fell, treat it as inside them.

**Floor**: never below 1 in 10 for tier A, 1 in 4 for tier B, and never fewer than one checked unit per week while the step is in use. Tier C has no floor below every unit. A rate that drifts to zero is the failure this skill exists to prevent.

**What the record shows.** If no defect turned up in n checked units, the true defect rate can still be as high as about 3/n (the 95% upper bound, known as the rule of three). Twenty clean units leave room for a rate up to about 15%; sixty, about 5%. If d defects turned up in n units, write the observed rate d/n and the one-sided 95% upper bound from an exact binomial interval (one defect in 30 leaves room for about 15%; two in 40, also about 15%). If nothing has been checked, or the number checked was never recorded, write "no record" and treat the step as having none. Put this in the plan, so a clean run is not read as proof.

### Step 3a: Check the workload

Multiply: units per week × share checked × minutes per check. Ask the owner how much checking time the step can have. If the plan needs more:

1. Move judgment items to machine checks where a rule can do them.
2. Split large units and sample claims or sections inside them (see Inputs).
3. Lower the volume or the step's level with `allocate-ai-work`.
   (Handing the check to an AI reviewer moves the work rather than removing it: the person still samples the reviewer.)
4. Only then, and only by the owner's explicit decision, accept a lower rate, even one below the floor: record it as an accepted risk, with the rate, the upper bound it leaves, and the date it will be reviewed.

Never lower the rate quietly to fit the time available.

### Step 4: Make the check happen

- **Pick units at random**, not the ones that are easy to check or that look odd. A sample chosen by convenience measures convenience.
- **Push the sample to the person** on a schedule, with the units attached: a short queue, a weekly list. Do not rely on someone noticing.
- **Keep each check short**: the judgment items from Step 1 and nothing else.

### Step 5: Keep a miss log

Record every defect, however it was found:

```text
| Date found | Unit | What was wrong | Found by | Should a check have caught it? Which one? | How far it travelled | Cost | Change made |
```

`Found by` is one of: machine check, judgment check (every unit or sampled), AI reviewer, designed safeguard, downstream (a later step or person not meant to catch it), outside report, not recorded.

What each kind of defect changes:

- **Found by a sample check**: the check worked. Return the step to every unit until 20 in a row are clean.
- **Found by a machine check**: fix the automation or its input; the judgment rate does not change.
- **Caught by a safeguard designed for it later in the workflow** (a reroute, a month-end reconciliation): count it in the defect record that the owner reviews; it is not a miss, and it does not by itself send the step back to every unit.
- **A miss**: a defect found downstream where nothing was designed to catch it, or reported from outside, in a unit that passed its check or was never sampled. A miss means the rate or the check was wrong, not that the person was careless. Return to every unit until 20 in a row are clean; change the check so it would have caught this defect, or move the item to a machine check; if the same kind of miss repeats, review the step's level with `allocate-ai-work`.

### Step 6: Recalibrate

- **Raising** the rate after a defect or a miss is immediate; it is the safe direction.
- **Lowering** the rate is a decision by the person who answers for the step's output, made on a set review date, with the track record and its upper bound in front of them. Write the decision and the date into the plan. The workflow never lowers its own rate.
- Review on a fixed date (monthly is a reasonable start) and after every miss.

### Step 7: Keep the record visible

Put the check record and the miss log where the people who rely on the step's output will see them. Trust stays calibrated when people can see how the step has actually performed.

## Output

Write the plan in the user's language. Keep the basis fields exactly as in `references/basis-index.md`.

```text
Check plan: {step} ({workflow})
Level: {prepares for a person | acts on its own}
Unit: {one output that can be checked on its own}
Machine checks (every unit): {list}
Judgment checks (at the rate below): {list}
Whole-output checks (every output): {list, or none}
Cost tier: {A | B | C}, because {where an undetected defect ends up}
Track record: {n} checked, {d} defects; {bound as in Step 3, or "no record"}
Rate now: {every unit | 1 in k}; floor {1 in k | none below every unit}; at least one unit per week
Workload: {units per week} × {share} × {minutes} = {minutes per week}; {within the owner's budget | over: what was done, per Step 3a}
Selection and delivery: {random, when sampling}; {how the units reach the checker, when}
Checker: {person | AI reviewer for {person}, with its own sample}
Raise rule: any defect from a sample check, or any miss -> every unit until 20 in a row are clean {tier C: n/a, already every unit; a miss changes the check}
Lower rule: owner decides on {review date}, with the track record in view {tier C: n/a}
Review on: {date}
Miss log: {where it is kept}; format as in Step 5
Basis:
[B1] {node} · {one-line intro} · {shelf} · {verification status} · {permalink}
Evidence: {one of: theory (the cited research supports the plan's direction; the rates themselves are working defaults, declared above) | own test (this plan has run and its record was kept) | external adoption | external results}
Not covered: {what the inputs did not settle}
```

Cite 0 to 3 basis nodes from the index (write `Basis: none` for zero), only where they support the plan: trust calibration (Trust in automation), why checking slides as reliability rises (Automation complacency & bias), why watching is not checking (Vigilance decrement), what a miss means (Use, misuse, disuse, abuse), why the person's leftover job of checking is hard (Ironies of automation).

## Anti-patterns

- "Review everything" with no schedule, which in practice becomes review nothing.
- A rate that is lowered by the workflow itself, or quietly by whoever is busy.
- Sampling only the units that look wrong.
- Counting machine checks as the human review.
- Reading a clean run as proof of reliability.
- Answering a miss with "be more careful" instead of changing the rate or the check.
- Telling people to verify, and calling that the safeguard.

## Limits

- The research cited supports the direction of the method: trust should be calibrated, reliable automation erodes checking, sustained watching fails, and instructions to verify are weak. The starting rates, the floors, the 20-unit run, and the idea that a sample check is a deliberate way of collecting failure experience are this studio's working choices, tested so far on its own workflows. The cited research does not supply those numbers. Details are in `VALIDATION.md` and `SOURCES.md` in the skill's repository, not in this installed folder.
- The rule-of-three bound assumes units are independent and sampled at random. Batches that fail together break that assumption; say so in "Not covered" when it applies.
