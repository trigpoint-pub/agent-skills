# Allocate a workflow before you hand it to AI

> Snapshot of article version 1.0 at <https://trigpoint.pub/methods/allocate-a-workflow>, written for allocate-ai-work v0.1.x. The web page is the canonical version; corrections appear there first. Text by Ansel, licensed CC BY 4.0 (see [`LICENSE-CONTENT`](../../LICENSE-CONTENT)).

“Should we hand this to AI?” treats automation as a single switch. A workflow usually gathers information, analyses it, decides and acts, and each of those stages can be handed over to a different degree. Handing over more is a trade rather than an upgrade: once a stage is handed over, the work left to the person changes, and so does their ability to take over when it fails.

Two questions are more useful. Once this stage is handed over, what work is left for the person? And when it goes wrong, who takes over, and at which step?

This article describes a procedure for settling the allocation stage by stage, and an agent skill that runs it. The result is an allocation ledger: one row per stage of each step, with the level, the reason, the work left for the person, the check, the takeover path, and the research each row rests on.

## The procedure

**1. Split each step into four stages.** Gather, analyse, decide, act. The split follows the four-stage model of Parasuraman, Sheridan and Wickens (2000): different stages of one workflow can be automated to different levels. List only the stages a step actually has. Sorting or filtering by fixed rules a person wrote (a threshold, a pattern list) is analysis; choosing among options in a way someone must answer for is a decision.

**2. Set a ceiling with two questions.** For each stage: if it gets something wrong, can the error be undone, by whom, how, and up to what point? Does an error here travel on, to the next step or to people outside the workflow, before anyone would notice?

The answers set the highest level the stage may reach. There are five levels: manual; suggest (alert or recommend); prepare (the automation does the work and a person reviews the result before it is used); act, undoable (the result takes effect without review, only where it can be undone, with a receipt for each); and act unattended. Two things separate the upper three: whether a person reviews the result before it takes effect, and whether anyone is present when it does. A scheduled job that only prepares work for a person stays at prepare, even though it starts itself. What starts a job does not decide between act, undoable and act unattended; whether anyone is present does. A background process that an AI agent starts and leaves running, such as a watcher or a retry loop, acts unattended when its results take effect while the person is away; an AI agent that is still running does not count as someone present.

| Situation | Ceiling |
|---|---|
| A decide stage | Suggest |
| A stage that speaks or commits for a person: sends, publishes, pays, signs | Suggest |
| The error cannot be undone | Suggest |
| Undoable, but travels on before anyone would notice | Prepare |
| Undoable, and does not travel | Act, undoable |
| As above, and a missed or wrong run would be reported by something that needs no one present (an alert, a watchdog, a failure report) before the next run, or, for a one-off run, before its result is relied on | Act unattended |

Sometimes most errors at a stage can be undone and one class cannot. Then set a ceiling for each class, but only if something sorts each item into its class before the stage acts (a filter, a rule, a person); if nothing does, the lowest ceiling holds for the whole stage. Items the sorting misses still run at the higher level. That is a residual risk: either lower the whole stage, or list it for the owner to accept or refuse by name.

The ceiling is the most the reasons allow; it is not a target. When the recommendation sits below it, say why.

The two questions, and the rule that decide stages and irreversible actions never go above suggest, are a working rule from our studio, drawn from one documented case. They are not part of the published level-of-automation models. The five levels fold the ten-level scale of Sheridan and Verplank (1978); the folding is ours too. The ledger header says so.

**3. Ask what work is left.** For every stage at prepare or above, write what the person still does after handover, then ask: will they still see enough of the work to notice a failure and understand it? Will they still have the practice to do the stage by hand when the automation stops? If either answer is no, lower the level by one, or add a takeover path that keeps them in practice, such as doing the stage by hand on a fixed schedule. The work left behind is a different job: checking data someone else cleaned is a different task from cleaning it (Bainbridge 1983; Endsley and Kiris 1995; Dekker and Woods 2002 on “who is better at it” lists).

**4. Write the check and the takeover.** For every stage at prepare or above, write what is checked, how much, how often and by whom. “Keep an eye on it” and “remember to check” are not checks: research on automation bias reports that telling people to verify does not reliably prevent it (Parasuraman and Manzey 2010; a contested point). For every stage, also write who notices when it goes wrong, who takes over, and at which step.

**5. Cite the basis and grade the evidence.** Each row cites 0 to 3 research summaries, only where they support that row's reasoning. Each comes with five fields: title, one-line intro, shelf, verification status and link; the verification status is the one shown on the summary's page (Bibliography checked, Abstracts checked, Checked against the sources). The evidence grade is one of theory, own test, external adoption and external results. A new ledger is usually theory. Never write “validated”.

**6. When reviewing, add today's level.** If the workflow already runs, read each stage's current level on the same scale and list the stages set higher than recommended (too high) or lower (room to hand over more). These are findings for the workflow's owner; the ledger changes no settings.

Two rules hold throughout. The person is whoever answers for the stage: if an AI does a stage on their behalf, such as reviewing a result, deciding or replying, that stage is automated even when the person is nearby. And a level is changed by a person, on a date; the automation never raises or lowers its own level (Miller and Parasuraman 2007 on adaptable versus adaptive automation). Every ledger has a review date.

## A blank ledger and an example

A blank ledger has four header lines: scope (it holds only for the workflow and error costs listed), the criterion statement (the two questions are the studio's own rule), a review date, and a status (a proposal until the owner adopts it). Its nine columns are step, stage, level, reason (the answers to the two questions), work left for the person, check, takeover, basis and evidence.

This is a demonstration sample. A freelance consultant sends six retainer clients a monthly performance report and wants to hand the sensible parts to an AI assistant that can read her analytics exports, draft text, build a PDF and send email from her account. The analysis stage sits at prepare: the assistant computes the changes and lists candidate reasons, each marked as a hypothesis, and she keeps, rewrites or drops each one; a made-up reason reads as well as a true one, and this analysis is what her clients pay for. The sending action sits at suggest: an email to the wrong person would hand one client's data to another and cannot be recalled. The assistant may alert her when the client name on the report does not match the recipient; she presses send. The full example ledger is on GitHub.

## Corrections we built in

When we ran the first version on our own workflows, the agent running it reported flaws in the instructions. Two of them changed the scale itself.

The first scale had no place for a scheduled job that only prepares work, and the runner read a weekly job of that kind as unattended. The revised scale separates the levels by whether a person reviews the result before it takes effect and whether anyone is present when it does.

The first ceiling table had a row for “a stage a named person must answer for”, capped at suggest. Someone answers for every stage, so the row capped them all. It now reads “a stage that speaks or commits for a person: sends, publishes, pays, signs”.

The same revision said who “the person” is: whoever answers for the stage.

## How well it works so far

Two small tests, neither an accuracy figure.

The first covered three automated workflows already running in our studio. Before this skill existed, we had recorded their levels, mechanism by mechanism, on our own five-level scale. The accounts given to the runner described the steps, who answers for them, what errors cost and what runs today, without our levels. The revised version's reading of today's levels matched our records on 2 of 7 (the first version, 1 of 7).

Of the five differences, three come from how the definitions were applied: the skill read the stages as the scale defines them, and our earlier records had not; those are ours to review in our records. Two sit near the boundary between levels. Where the skill recommended a level different from today's, it was mostly lower. Those recommendations went to the owner; no workflow was changed.

The second test was a made-up workflow, designed from scratch: every row carried a reason, the work left for the person, a check, a takeover path and basis fields. It is the example above.

The limits: each run was a fresh AI agent that read only the skill and the accounts, and could not search or ask questions. The accounts were written, and the results compared, by the agent coordinating the test, which was the same model. The scoring was not blind and the test was not preregistered. Each run wrote four ledgers in about 15 to 18 minutes, roughly 190,000 to 200,000 tokens including reading the skill. Not yet tested: installation and discovery on agent hosts; workflows written by other people, and teams; whether an adopted ledger changes how a workflow fails; and agreement between two runs on the same workflow.

The rules in step 2 on presence and on mixed error classes were added after these tests, and the runs were not repeated on them.

The evidence so far is our own test: one small studio has used it and recorded the result.

## When to use it

Before handing one concrete workflow (3 to 12 steps) to AI, or when reviewing one that already runs. Not for rating how well a person uses AI, choosing tools or vendors, regulated or safety-critical work (those have their own standards; a ledger can sit beside them, not replace them), or a request with no concrete workflow, such as “use AI more”.

## Get the skill

The skill, its research index and the example ledger are on GitHub: [github.com/trigpoint-pub/agent-skills](https://github.com/trigpoint-pub/agent-skills) (`skills/allocate-ai-work/`). Two more belong to the same set: `calibrate-ai-checks`, for how often to check a step while it runs, and `classify-ai-incident`, for after something goes wrong. Each installs on its own.

## References

1. Sheridan and Verplank (1978) on levels of automation.
2. Parasuraman, Sheridan and Wickens (2000) on stages and levels.
3. Fitts (1951), and Dekker and Woods (2002), on “who is better at it” lists.
4. Bainbridge (1983) on the ironies of automation.
5. Endsley and Kiris (1995) on the out-of-the-loop problem.
6. Parasuraman and Manzey (2010) on complacency and bias.
7. Miller and Parasuraman (2007) on who changes the level.

Full references and how they were checked are in [`docs/allocate-ai-work/SOURCES.md`](SOURCES.md) on GitHub.
