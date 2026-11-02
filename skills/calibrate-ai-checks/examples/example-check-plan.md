# Example check plan

This is a demonstration sample. The step below is made up for this example. The plan after it was produced by running the skill on it, and is reproduced as written.

## The input

An AI assistant tags each incoming support ticket with a product area and an urgency level, about 300 tickets a week. Tags route tickets to teams; a wrong tag delays a ticket by a day until someone reroutes it. So far 40 tickets were checked and 2 had a wrong urgency. A check takes about 30 seconds. The support lead can spend about 30 minutes a week on checking.

## The plan

```text
Check plan: Support ticket tagging: product area and urgency (software company support team: incoming tickets routed to team queues)
Level: acts on its own (the tags route each ticket to a team with no person in between)
Unit: one ticket's pair of tags (product area, urgency)
Machine checks (every unit): both tags present; each tag is a value from the allowed list; every incoming ticket is tagged (tickets in against tickets tagged, daily); every reroute is logged with the original and the corrected tag, so wrong areas caught by rerouting enter the defect record without anyone writing them down. Results go to the support lead with each week's sample.
Judgment checks (at the rate below): the product area is right for what the ticket describes; the urgency is right by the team's urgency definitions.
Whole-output checks (every output): none (each ticket stands alone; the "every ticket tagged" count runs as a machine check)
Cost tier: B, because a wrong tag moves the ticket to the wrong team and delays it by a day until someone reroutes it
Track record: 40 checked, 2 defects (both wrong urgency); observed 2 in 40 (5%), one-sided 95% upper bound about 15%
Rate now: every unit (Step 3: where the 2 defects fell among the 40 is not recorded, so they are treated as within the last 20); floor 1 in 4; at least one unit per week
Workload: 300 × 1 × 0.5 = 150 minutes per week; over the lead's 30 minutes, five times over (even the tier B floor, 1 in 4, would be 37.5 minutes). Done per Step 3a: (1) presence, allowed values and the tagged count are machine checks, and area errors that cause a reroute now reach the record automatically, but no judgment time is saved, because both judgment items need the ticket read; (2) not applicable: the unit already takes 30 seconds; (3) put to the lead for a decision via allocate-ai-work: an AI reviewer that tags every ticket independently, with the lead re-checking a random 1 in 10 of its verdicts (30 × 0.5 = 15 minutes) plus every ticket where it disagrees with the tagger (assumed about 5% of 300, 15 × 0.5 = 7.5 minutes), about 23 minutes a week in all; this moves the work rather than removing it; (4) otherwise, only by the lead's explicit decision, an accepted risk of 1 in 5 (60 tickets, 30 minutes), below the floor, leaving an upper bound of about 15% now, reviewed on 2026-11-25. Until the lead decides, the lead checks a random 60 tickets a week (the full 30 minutes), and the record shows "every unit required, 1 in 5 run, decision pending": this is not an accepted rate.
Selection and delivery: random: each working day a script draws about 12 tickets from the previous day's tickets and pushes them to the lead as a short list, with the ticket text and both tags shown; daily, so a wrong urgency is corrected within about a day
Checker: person (the support lead); if option (3) is chosen, AI reviewer for the support lead, with its own sample (1 in 10 of its verdicts, at least one a week)
Raise rule: any defect from a sample check, or any miss -> every unit until 20 in a row are clean
Lower rule: owner (the support lead, taken as the person who answers for the tags) decides on 2026-11-25, with the track record in view
Review on: 2026-11-25, then monthly, and after every miss; the decision between options (3) and (4) is due at once, not at the review
Miss log: a shared sheet beside the support queue dashboard, where the support teams can see it; format as in Step 5
Basis:
[B1] Trust in automation · “The more they trust it, the better”: wrong. · Human-Automation Interaction · Bibliography checked · https://trigpoint.pub/collections/hai/trust-in-automation
[B2] Use, misuse, disuse, abuse · Over-reliance and refusal to use have independent causes. · Human-Automation Interaction · Bibliography checked · https://trigpoint.pub/collections/hai/use-misuse-disuse-abuse
Evidence: theory (the cited research supports the plan's direction; the rates themselves are working defaults, declared above)
Not covered: who answers for the tags (taken to be the support lead); the level (not stated; read as acting on its own because tags route tickets directly); how the 40 tickets were chosen and where the 2 defects fell; rerouting is a designed safeguard for wrong areas, but a wrong urgency usually keeps the ticket in the right team at the wrong priority and is not rerouted, so the sample is the only signal for urgency, which is where both defects were; whether urgency carries a response-time promise to customers (if a too-low urgency breaks such a promise, the urgency tag reaches people outside and is tier C, every unit, and option (3) or a change of level becomes necessary rather than optional); whether an AI reviewer can be built and how often it would disagree (5% assumed from the observed rate); tickets about one incident arrive together and tend to be tagged wrong together, which breaks the independence the bound assumes; the interim run of 1 in 5 before the lead decides is this plan's reading, since SKILL.md says what to do after the owner decides but not before.
```

## Miss log

| Date found | Unit | What was wrong | Found by | Should a check have caught it? Which one? | How far it travelled | Cost | Change made |
|---|---|---|---|---|---|---|---|
| Before 2026-10-25 (exact date not recorded) | One ticket (which not recorded) | Wrong urgency level | judgment check (sampled: 40 checked; how they were chosen not recorded) | Yes, and it did: the urgency judgment item; no machine check can verify urgency, and rerouting does not catch it | Not recorded whether the ticket was delayed | Not recorded | This plan: every unit until 20 in a row are clean (run at 1 in 5 pending the lead's decision); urgency kept as a judgment item |
| Before 2026-10-25 (exact date not recorded) | One ticket (which not recorded) | Wrong urgency level | judgment check (sampled: 40 checked; how they were chosen not recorded) | Yes, and it did: the urgency judgment item; no machine check can verify urgency, and rerouting does not catch it | Not recorded whether the ticket was delayed | Not recorded | As above |
