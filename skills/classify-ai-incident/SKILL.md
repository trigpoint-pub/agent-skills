---
name: classify-ai-incident
description: Classifies one incident involving AI or other automation as use, misuse, disuse or abuse (Parasuraman and Riley, 1997), always asking separately whether the setup itself ignored the people who had to work with it, and points the fix at a mechanism (the allocation level, the check, the alarm, the information shown) rather than at "be more careful". Returns a short incident record with the facts, the label and its evidence, and the fix direction. Use when asked why an AI-assisted process went wrong, whether a person or the design is at fault, how to write up an AI error, or what to change after one. Not a blame or performance review of a person, and not a root-cause analysis of the model's internals.
---

# Classify AI Incident

Put one incident where automation was involved into one of four categories, and let the category point to what should change.

When something goes wrong with an automated step, the first reflex is to blame the person who was supposed to catch it. The four categories below were set out by Parasuraman and Riley (1997) to replace "was the human or the machine more reliable?" with "was the reliance appropriate?". They are four independent ways a relationship between people and automation can go wrong. They are not a maturity scale, and two of them are not opposite ends of one dial. One of them, abuse, turns the question back on whoever designed, configured or required the automation.

## The four categories

| Category | What it means | Typical signs |
|---|---|---|
| **Misuse** | People relied on the automation more than its actual reliability warranted. | Checks thinned out; output was followed without challenge; a wrong recommendation was accepted, or a missing one was not noticed. |
| **Disuse** | People did not use, ignored, or switched off automation that was reliable enough to help, because they trusted it less than it deserved. | Alerts skipped or muted; a tool abandoned after bad early results; work redone by hand that the tool did correctly. Too many false alarms are a common cause. |
| **Abuse** | Whoever designed, configured or required the automation put it in place without regard for its consequences for the people working with it. | Automation placed at a stage or level people cannot supervise; alarm thresholds set without regard to how often the event really happens; people told to "watch" it; no way to take over; the automation changes its own level. |
| **Use** | Reliance matched the automation's reliability. The incident is not a mismatch between people and automation. | A defect that a reasonable check would not have caught; the people involved relied on the step about as much as its record justified. |

Three points carry most of the value:

- **Misuse and disuse have separate causes and can occur together**, in the same system in different situations. Fixing one can make the other worse: cutting false alarms to win back trust can lead to over-reliance.
- **Always ask the abuse question separately.** Leaving abuse out records a design failure against the operator.
- **A fix aimed at a person's diligence rarely holds.** Attention under load is a structural limit, not a matter of effort.

## When to use

- An AI-assisted or automated step produced a bad outcome, a near miss, or a pattern of being ignored.
- Writing an incident note or post-mortem that involves automation.
- Deciding whether to change the automation, the check, or the setup after an error.

## When not to use

- Judging an individual's performance. This classifies a relationship, not a person.
- Debugging the model or code itself. Classify first; if the result is use, the fix is in the automation's own defect, and that work is engineering.
- Many incidents at once. Run one incident per record; look for patterns across records afterwards.

## Inputs

An account of the incident with, as far as known:

1. The automation: what it does, at which stage (gather, analyse, decide, act), and how far it runs on its own.
2. What it did or failed to do.
3. What the people involved did, and what they were told or set up to do.
4. How the problem was noticed, and by whom.
5. What it cost, and what was done about it.

If the account blames someone, keep the facts and set the blame aside. If a fact the classification turns on is missing, ask one question, or record it as unknown.

**Who counts as "people".** The people side is whoever chose, set up, checked, or relied on the automation's output. In AI-assisted work that is often another AI agent acting for a person: an assistant that ran a bulk tool, a reviewer agent that passed a result. Treat that agent as the people side, name the person it answers to, and classify as usual.

**Chains.** When one automated step feeds another and a person relies on the last (an AI tool, then an AI reviewer, then a person), classify one link. The step where the defect entered is the automation; the next party that relied on its output, person or AI reviewer, is the people side. Name the link in the Automation line of the record. If a later link also relied on the output more than its record warranted, that can be a secondary label with its own evidence.

## Workflow

### Step 1: Restate the facts

Write the incident as plain facts under the five input headings. Mark what is unknown. Do not label anything yet.

### Step 2: Reliance against reliability

- What was the automation's actual reliability at that point, as far as the record shows (its track record, recent changes, known weak spots)?
- How much did the people involved rely on it (did they check, follow, ignore, override)?
- Reliance above reliability: misuse candidate. Reliance below reliability: disuse candidate. Reliance about equal to reliability: use candidate.

### Step 3: The abuse question, always

Ask each of these, whatever Step 2 found:

- Was the automation placed at a stage and level the people could supervise and take over from?
- Were thresholds, scope and defaults set with regard to how often the event really occurs and what a false alarm costs?
- Did the people have the information they needed to judge when to trust it (its record, its process, its limits)?
- Were people asked to "keep an eye on it" as the safeguard?
- Did the automation change its own level or scope without a person deciding? Handing that switch to the system takes the decision away from the person who answers for it (adaptable versus adaptive automation; Miller and Parasuraman, 2007).
- Was the automation required or rolled out by someone who did not have to work with it?

One or more clear "no, it was not set up with regard for them" answers make abuse a candidate, even when misuse or disuse also happened.

Abuse is about disregard for the people, not about any wrong setting. A setting (a threshold, a source list, a scope, a default) is evidence of abuse only when it was chosen without regard to the people who supervise or rely on the automation: a threshold set with no thought for how often the event really occurs and what a false alarm or a miss costs them, or a scope they cannot supervise. A setting chosen with reasonable care that turned out wrong for the facts is the automation's own defect (Step 2's use candidate), unless people kept relying on it after there was reason to doubt it (misuse).

A "no" counts towards abuse only if this incident turned on it: the reliance, the miss or the failed takeover happened in a way that the missing information, threshold or takeover path would have prevented or exposed. If Step 2 found reliance about equal to reliability, a missing track record did not change this incident. Whether a gap belongs to this one automation or runs through the whole setup changes nothing on its own. A gap the incident did not turn on is still worth fixing: list it in Fix direction as its own item, not as evidence for the label.

### Step 4: Label

- One **primary** category: the one whose fix would most directly have prevented this incident.
- A **secondary** category only if it has its own evidence. Drop a candidate you cannot support with a sentence.
- One sentence of evidence for each, pointing to the facts from Step 1.
- `insufficient facts` is a valid label. Say which fact would settle it.
- If nothing has gone wrong yet (a gap found before any harm), classify the relationship the gap would allow and add `near miss` after the label.
- Confidence: **high** when the facts cover both reliance and setup and the primary is clearly the strongest; **medium** when one deciding fact is unknown or the secondary is nearly as strong as the primary; **low** when the account is short or one-sided. A secondary label with its own evidence does not lower confidence by itself.

### Step 5: Fix direction

Point the fix at a mechanism:

| Category | Fix direction |
|---|---|
| Misuse | Show people the step's track record and limits; put a scheduled sample check in place (`calibrate-ai-checks`); consider a lower level for that stage. |
| Disuse | Bring the false-alarm rate in line with how often the event really happens; show the step's actual reliability; repair the trust problem before abandoning a tool that works. |
| Abuse | Redesign the allocation: stage, level, thresholds, takeover path (`allocate-ai-work`). Return the level switch to a person. |
| Use | Fix the automation's own defect; reliance can stay as it is. |

"Remind people to be careful" or "train them to pay attention" is never the fix on its own. Fixing the mechanism, not the person, follows the system approach described by Reason (2000); making it a fixed repair step in this record is Trigpoint's (2026). The research basis is that abuse places the cause upstream, and that attention-based failures persist with practice and are not reliably removed by instructions to verify.

## Output

Write the record in the user's language. Keep the basis fields exactly as in `references/basis-index.md`.

```text
Incident record: {short title}
Facts
- Automation: {what, stage, how far it runs on its own; in a chain, which link this record classifies}
- Event: {what it did or failed to do}
- People: {what they did; what they were told or set up to do}
- Detection: {how and by whom}
- Cost: {what it cost}
- Unknown: {facts not available}
Reliance vs reliability: {one or two sentences}
Abuse question: {which answers were "no", or "none"}
Label: primary {category}; secondary {category | none}
Evidence: {primary: one sentence}
          {secondary: one sentence, if any}
Confidence: {high | medium | low}
Fix direction: {mechanism to change}
Not the fix: {what would only blame or exhort a person}
Basis:
[B1] {node} · {one-line intro} · {shelf} · {verification status} · {permalink}
```

Cite 0 to 3 basis nodes (write `Basis: none` for zero), only where they support the record: the four categories (Use, misuse, disuse, abuse), trust and its calibration (Trust in automation), why checking slides (Automation complacency & bias), who holds the switch (Adaptive automation), stage and level (Levels of automation).

## Anti-patterns

- Labelling the person ("careless", "lazy") instead of the relationship.
- Treating misuse and disuse as two ends of one scale.
- Skipping the abuse question because an operator also made a mistake.
- Choosing the category first and then picking the facts that fit.
- Calling everything abuse. If the setup was reasonable and the person over-relied, the label is misuse.
- A fix that only asks people to try harder.

## Limits

- The four categories come from Parasuraman and Riley (1997); this skill's wording of them is a summary, and the paper's verbatim definitions are not quoted here. The abuse checklist in Step 3 and the fix table are working choices from Trigpoint (2026), tested so far on its own incident records. Details are in `VALIDATION.md` and `SOURCES.md` in the skill's repository, not in this installed folder.
- A classification is only as good as the account of the incident. Short or one-sided accounts lead to low confidence; say so.
