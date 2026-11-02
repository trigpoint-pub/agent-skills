# Classify an AI incident before you fix it

> Snapshot of article version 1.0 at <https://trigpoint.pub/methods/classify-an-incident>, written for classify-ai-incident v0.1.x. The web page is the canonical version; corrections appear there first. Text by Ansel, licensed CC BY 4.0 (see [`LICENSE-CONTENT`](../../LICENSE-CONTENT)).

When an automated step goes wrong, the first reflex is to blame the person who was supposed to catch it. Parasuraman and Riley (1997) set out four categories that replace “was the person or the machine more reliable?” with “was the reliance appropriate?”. They are four independent ways the relationship between people and automation can go wrong. They carry no ranking, and misuse and disuse each have their own causes. One of them, abuse, turns the question back on whoever designed, configured or required the automation.

This article describes a procedure for putting one incident into one of the four categories and letting the category point to the fix, and an agent skill that runs it. The result is a short incident record.

## The four categories

| Category | What it means | Typical signs |
|---|---|---|
| Misuse | People relied on the automation more than its actual reliability warranted | Checks thinned out; output followed without challenge; a wrong recommendation accepted, or a missing one not noticed |
| Disuse | People did not use, ignored or switched off automation that was reliable enough to help, because they trusted it less than it deserved | Alerts skipped or muted; a tool abandoned after bad early results; work redone by hand that the tool did correctly. Too many false alarms are a common cause |
| Abuse | Whoever designed, configured or required the automation put it in place without regard for its consequences for the people working with it | Placed at a stage or level people cannot supervise; alarm thresholds set without regard for how often the event really happens; people told to “watch” it; no way to take over; the automation changes its own level |
| Use | Reliance matched the automation's reliability; the incident does not come from a mismatch between people and automation | A defect a reasonable check would not have caught; people relied on the step about as much as its record justified |

The wording of the categories is this method's summary; the paper's verbatim definitions have not been checked first-hand.

Three points carry most of the value. Misuse and disuse have separate causes and can occur together, in the same system in different situations; fixing one can make the other worse, as when cutting false alarms to win back trust leads to over-reliance. The abuse question must be asked separately every time; leaving it out records a design failure against the operator. And a fix aimed at a person's diligence rarely holds: attention under load is a structural limit that effort does not remove.

## The procedure

**1. Restate the facts.** Write the incident under five headings: what the automation does, at which stage and how far it runs on its own; what it did or failed to do; what the people involved did, and what they were told or set up to do; how the problem was noticed and by whom; what it cost and what was done. Mark what is unknown. Label nothing yet. If the account blames someone, keep the facts and set the blame aside.

The people side is whoever chose, set up, checked or relied on the automation's output. In AI-assisted work that is often another AI acting for a person: an assistant that ran a bulk tool, a reviewer agent that passed a result. Treat it as the people side, name the person it answers to, and classify as usual. When one automated step feeds another, such as an AI tool, then a reviewer agent, then a person, classify one link: the step where the defect entered is the automation, and the next party that relied on its output is the people side.

**2. Compare reliance with reliability.** What was the automation's actual reliability at that point, as far as the record shows (its track record, recent changes, known weak spots)? How much did the people involved rely on it (did they check, follow, ignore, override)? Reliance above reliability makes misuse a candidate; below it, disuse; about equal, use.

**3. Ask the abuse question every time.** Whatever step 2 found, ask: was the automation placed at a stage and level people could supervise and take over from? Were thresholds, scope and defaults set with regard to how often the event really occurs and what a false alarm costs? Did people have what they needed to judge when to trust it (its record, its process, its limits)? Was “keep an eye on it” the safeguard? Did the automation change its own level or scope without a person deciding (adaptable versus adaptive automation; Miller and Parasuraman 2007)? Was it required by someone who did not have to work with it?

Abuse is about disregard for the people, not about any wrong setting. A setting chosen with reasonable care that turned out wrong for the facts is a defect of the automation itself, step 2's use candidate, unless people kept relying on it after there was reason to doubt it, which is misuse.

An answer that points to abuse counts only if this incident turned on it: the missing information, threshold or takeover path would have prevented or exposed what happened. A gap the incident did not turn on is still worth fixing; list it as a fix of its own, not as evidence for the label.

**4. Label.** One primary category: the one whose fix would most directly have prevented this incident. A secondary only if it has its own evidence. One sentence of evidence for each, pointing back to the facts from step 1. “Insufficient facts” is a valid label; say which fact would settle it. For a gap found before any harm, label the relationship the gap would allow and add “near miss”. Confidence is high when the facts cover both reliance and setup and the primary is clearly strongest; medium when one deciding fact is unknown or the secondary is nearly as strong; low when the account is short or one-sided.

**5. Point the fix at a mechanism.**

| Category | Fix direction |
|---|---|
| Misuse | Show people the step's record and limits; schedule a sample check (see `calibrate-ai-checks`); consider a lower level for that stage |
| Disuse | Bring the false-alarm rate in line with how often the event really happens; show the step's actual reliability; repair trust before abandoning a tool that works |
| Abuse | Redesign the allocation: stage, level, thresholds, takeover path (see `allocate-ai-work`); return the level switch to a person |
| Use | Fix the automation's own defect; reliance can stay as it is |

“Remind people to be careful” or “train them to pay attention” is never the fix on its own. Fixing the mechanism rather than the person is our studio's repair pattern; the research basis is that abuse places the cause upstream, and that attention-based failures persist with practice and are not reliably removed by instructions to verify (Parasuraman and Manzey 2010; the latter point is contested).

## Corrections we built in

We ran it on six newly written practice incidents and six incidents our studio had already classified, and revised it twice.

The first version assumed the people side was a human operator. In several of our own incidents, the one relying on the tool was an AI assistant, such as one that ran a bulk tool. The first revision says an AI can be the people side.

After the first revision, abuse appeared in 10 of the 12 records: the net was too wide. The second revision limits abuse to settings chosen without regard for the people who supervise or rely on the automation; a setting chosen with reasonable care that turned out wrong is a defect of the automation itself.

## How well it works so far

The tests are small; none is an accuracy figure.

Six practice incidents: all three runs fell within the answer key on all six, and each time gave the incident that needs two labels both of them. The answer key was written before the first run and is published on GitHub.

Six incidents from our own records: before this skill existed, we had sorted them with the same four categories. Restated as neutral accounts without the earlier labels, they were classified blind. Each run matched our earlier label on 3 of 6.

Two agreed in every run. Two disagreed in every run: the skill found that people had relied on the automation about as much as its record justified and put the fault in the automation, where our earlier label had recorded a consequence (a tool set aside after it failed) or a risk (false alarms that could erode trust). For the false-alarm incident, a later check of the records showed every false alarm still went on the priority list and was fixed within two days: the loss of trust the label anticipated did not happen, and the skill's reading matches the record. For the other, on review, we judged the skill's reading at least as defensible as our label. One moved into agreement once the first revision said an AI can be the one relying on a tool. One switched between abuse and use as the wording about settings changed: the line between a setting chosen carelessly and one chosen without regard for people is the least stable part of the method. The two revisions did not raise the number of agreements; each was made for flaws the runners reported in the instructions.

The limits: each run was a fresh AI agent that read only the skill and the accounts, could not search or ask questions, and never saw the answer key or earlier outputs. The practice incidents, their answer key and the neutral accounts of our own incidents were written, and the results scored, by the agent coordinating the test, which was the same model. The scoring was not blind and the test was not preregistered. Each run classified 12 incidents in about 7.5 to 9 minutes, roughly 130,000 to 140,000 tokens including reading the skill. Not yet tested: installation and discovery on agent hosts; incidents written by other people, and long post-mortems; agreement between two independent reviewers on the same incident; any effect on what teams actually change afterwards.

The rules on chains in step 1 and on what counts towards abuse in step 3 were added after these tests. The runs were not repeated on them; the answer key for the practice incidents, re-read against them, is unchanged.

The evidence so far is our own test: one small studio has used it and recorded the result.

## When to use it

When an AI-assisted or automated step produced a bad outcome, a near miss, or a pattern of being ignored; when writing an incident note or post-mortem that involves automation; when deciding whether to change the automation, the check or the setup after an error. Not for judging an individual's performance (the method classifies the relationship between people and automation), for debugging the model or code itself (classify first; if the result is use, the fix is engineering work), or for many incidents at once (one record per incident; look for patterns across records afterwards).

## Get the skill

The skill, its research index and the practice incidents are on GitHub: [github.com/trigpoint-pub/agent-skills](https://github.com/trigpoint-pub/agent-skills) (`skills/classify-ai-incident/`); their answer key is in `docs/classify-ai-incident/VALIDATION.md`. The set also has `allocate-ai-work` (before handover) and `calibrate-ai-checks` (while it runs). Each installs on its own.

## References

1. Parasuraman and Riley (1997) on use, misuse, disuse and abuse.
2. Miller and Parasuraman (2007) on adaptable versus adaptive automation.
3. Parasuraman and Manzey (2010) on complacency and bias.

Full references and how they were checked are in [`docs/classify-ai-incident/SOURCES.md`](SOURCES.md) on GitHub.
