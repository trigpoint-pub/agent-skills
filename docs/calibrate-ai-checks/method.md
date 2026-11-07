# Calibrate how often you check AI output

> Snapshot of article version 1.1 at <https://trigpoint.pub/methods/calibrate-a-check>, written for calibrate-ai-checks v0.1.x. The web page is the canonical version; corrections appear there first. Text by Ansel, licensed CC BY 4.0 (see [`LICENSE-CONTENT`](../../LICENSE-CONTENT)).

When an AI step has been reliable for a while, people check it less and less, until an error nobody was looking for gets through. The opposite is just as common: a step that produced too many bad outputs or false alarms early on stops being trusted, even after it improves. The two failures pull in opposite directions and have separate causes (Parasuraman and Riley 1997). So the aim is neither more trust nor less: trust should match the step's real reliability, and should tell the situations where it is reliable from those where it is not (calibration and resolution, in Lee and See 2004).

Watching continuously does not solve this; detection falls off within a short time of watching (Mackworth 1948). Telling people to verify is not dependable either (Parasuraman and Manzey 2010; a contested point). What works better is a check that is scheduled, small, pushed to the person, and kept at a rate that never reaches zero.

This article describes a procedure for setting such a check, and an agent skill that runs it. The result is a check plan and a miss log.

## The procedure

**1. Separate machine checks from judgment checks.** First write a short defect checklist for the step: what counts as wrong. A check without a definition of a defect is a glance. Items a script, rule or schema can verify (format, required fields, counts, files present, links that resolve, figures that match their source) are machine checks: they run on every item, and their results go to a person. They do not count as the human check. Whether the content is right, fits the case and says what it should are judgment checks, which a person samples.

**2. Place the step in a cost tier.** Where would an undetected defect end up? Tier A: it stays inside the workflow and is cheap to undo. Tier B: it moves on to a next step or person before anyone notices, or takes real time to undo. Tier C: it reaches people outside, money or a commitment, or cannot be undone. A tier C step that acts on its own is outside this method; send it back to the allocation (see `allocate-ai-work`). A tier C step that only prepares work gets a judgment check on every item.

**3. Set the starting rate.** These are working defaults from Trigpoint (2026), not figures from the research; adjust them and write down why.

| Track record | Tier A | Tier B | Tier C |
|---|---|---|---|
| Fewer than 20 items checked | every item | every item | every item |
| Any defect in the last 20 checked | every item | every item | every item |
| 20 or more checked, none defective in the last 20 | eligible for 1 in 5 | eligible for 1 in 3 | every item |

“Eligible” means the owner may decide to move to that rate at a review; nothing moves lower on its own. Floors: never below 1 in 10 for tier A or 1 in 4 for tier B, and never fewer than one checked item a week while the step is in use; tier C has no floor below every item. A rate that drifts to zero is the failure this method exists to prevent.

The plan also says what the record proves. If no defect turned up in n checked items, the true defect rate can still be as high as about 3/n (the 95% upper bound known as the rule of three): twenty clean items leave room for a rate up to about 15%; sixty, about 5%. If nothing has been checked, or the number checked was never recorded, write “no record” and treat it as zero.

**4. Check the workload.** Multiply items per week by the share checked and the minutes per check, and ask the owner how much checking time the step can have. If the plan needs more, in order: move judgment items to machine checks; split large items and sample single claims or sections; lower the volume or the step's level with `allocate-ai-work`. Handing the check to another AI reviewer only moves the work: the person still samples that reviewer. Only then may the owner explicitly accept a lower rate, even one below the floor, recorded as an accepted risk with the rate, the upper bound it leaves and a review date. Never lower the rate quietly to fit the time available.

**5. Make the check happen.** Pick items at random, never the ones that are easy to check or look odd. Push the sample to the checker on a schedule, such as a weekly list. Keep each check to the judgment items from step 1. The checker may be an AI reviewer, but the owner samples its verdicts: by working default, 1 in 10, and at least one a week. Checking an item means opening the item or its sources: a person who accepts or rejects each item from the reviewer's summary has not checked it, and those decisions do not replace the sample of its verdicts.

**6. Keep a miss log.** Record every defect, however it was found: date, item, what was wrong, who or what found it, which check should have caught it, how far it travelled, what it cost, what was changed. A defect found by a sample check means the check worked: return to every item until 20 in a row are clean. One found by a machine check means fixing the automation or its input; the judgment rate stays as it is. One caught by a safeguard designed for it later in the workflow (a reroute, a month-end reconciliation) goes into the defect record and is not a miss. A miss is a defect found downstream, or reported from outside, where nothing was designed to catch it: return to every item, change the check so it would catch this defect next time, and if the same kind of miss repeats, review the step's level. A miss means the rate or the check was wrong, not that someone was careless.

**7. Recalibrate, and keep the record visible.** Raise the rate at once after a defect or a miss; that is the safe direction. Lowering it is the owner's decision, made on a set review date with the record and its upper bound in front of them. Monthly is a reasonable start, plus a review after every miss. Keep the check record and the miss log where the people who rely on the step will see them: trust can only follow performance that people can see.

## Corrections we built in

We ran the method on two checking steps from our own studio and two made-up steps, and revised it three times.

The first version collected the minutes each check takes and never used them. One plan as a result called for about 40 hours of checking a week. The revision added step 4: work out the load first, deal with any excess in order, and leave an owner's accepted risk as the last resort.

The third revision changed what counts as a miss. Before it, every defect caught downstream counted, so a high-volume step with routine daily reroutes went back to checking every item at each reroute and could never reach sampling. Now a defect caught by a safeguard designed for it only goes into the defect record.

One correction concerns wording. The research notes that experience of automation failures may reduce complacency (Parasuraman and Manzey 2010); it does not list sample checks as a countermeasure. Treating a sample check as a deliberate way to collect failure experience is an inference by Trigpoint (2026).

## How well it works so far

The tests are small; none is an accuracy figure.

The first set covered two checking steps already running in our studio: accepting work returned by an external AI agent, and using facts that sub-agents gather during a working session. We compared the plans with one month of actual records. Neither step had a written check rate, and neither kept a count of items checked.

Without counts, most classes could only be recorded as “no record”, and the classes that move on or go public came out at every item. The workload step put the owner's share of the checking at about half an hour to an hour a week.

The second set covered two made-up steps. Supplier invoice extraction is tier C (a wrong total gets paid): every item, within the assumed budget. Support ticket tagging is tier B: back to every item after two defects, five times over the stated budget. The plan worked through the workload options, put the use of an AI reviewer to the owner as a decision, and did not treat a lower rate as accepted until the owner decides. That plan is the example on GitHub.

The limits: each run was a fresh AI agent that read only the skill and the accounts, and could not search or ask questions; where the skill says to ask the owner, it had to assume and record the assumption. The accounts were written, and the results compared, by the agent coordinating the test, which was the same model. The scoring was not blind and the test was not preregistered. Four runs, each writing four plans in about 8 to 14 minutes, roughly 130,000 to 175,000 tokens including reading the skill. Not yet tested: whether following a plan catches more defects or changes trust; a miss log kept over time; steps described by other people; agreement between two runs on the same step.

The rule in step 5 on what counts as checking an item was added after these tests, and the runs were not repeated on it.

The evidence so far is our own test: one small studio has used it and recorded the result.

## When to use it

When an AI step drafts, extracts, classifies or acts and a person is supposed to review it; when review has become a click-through and nobody knows how much is actually checked; or when an AI error got through and the review rate should respond. Not for steps that decide or take irreversible actions (those should not be left to sampling: a person reviews each one, or the step is redesigned, see `allocate-ai-work`), for regulated review with required rates, or for testing the automation before it runs.

## Get the skill

The skill, its research index and an example plan are on GitHub: [github.com/trigpoint-pub/agent-skills](https://github.com/trigpoint-pub/agent-skills) (`skills/calibrate-ai-checks/`). The set also has `allocate-ai-work` (before handover) and `classify-ai-incident` (after something goes wrong). Each installs on its own.

## References

1. Lee and See (2004) on calibration and resolution of trust.
2. Parasuraman and Manzey (2010) on complacency and bias.
3. Mackworth (1948) on vigilance decrement.
4. Parasuraman and Riley (1997) on misuse and disuse.
5. The rule of three is the standard binomial upper bound when no events are observed.

Full references and how they were checked are in [`docs/calibrate-ai-checks/SOURCES.md`](SOURCES.md) on GitHub.
