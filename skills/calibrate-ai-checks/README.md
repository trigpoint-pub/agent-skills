# Calibrate AI Checks

An agent skill that sets how often, and how, a person checks the output of an AI step, and keeps that rate tied to what the step has actually done.

It separates machine checks (run on every item) from human judgment checks (taken as a random sample), sets a starting rate from the step's track record and what an undetected error costs, states what a clean record does and does not prove, keeps the rate from sliding to zero, and keeps a miss log so that a missed error changes the check, not just the mood.

> Version 0.1.0, experimental prerelease · Maintainer: Ansel · License: [MIT](LICENSE)
> Method article: [Calibrate how often you check AI output](https://trigpoint.pub/methods/calibrate-a-check) (a full-text snapshot is in [`docs/calibrate-ai-checks/method.md`](https://github.com/trigpoint-pub/agent-skills/blob/main/docs/calibrate-ai-checks/method.md), licensed CC BY 4.0)

Part of a set of three: [`allocate-ai-work`](https://github.com/trigpoint-pub/agent-skills/tree/main/skills/allocate-ai-work) (before handover), `calibrate-ai-checks` (while it runs), [`classify-ai-incident`](https://github.com/trigpoint-pub/agent-skills/tree/main/skills/classify-ai-incident) (after something goes wrong). Each installs on its own.

## What you get

- A [skill](SKILL.md) with a seven-step workflow: split machine from judgment checks, place the step in a cost tier, set the starting rate and floor and check the workload, make the check happen, keep a miss log, recalibrate, and keep the record visible.
- A [basis index](references/basis-index.md) of five research summaries the plan can cite, each with its verification status and permalink.
- An [example check plan](examples/example-check-plan.md) for a made-up step.

## What it does not do

- It does not set review for steps that decide or act in ways that cannot be undone; those need a person on every item or a redesign.
- It does not replace testing the automation itself.
- It does not meet any regulated sampling standard.

## Requirements

- An agent that can load skills in the `SKILL.md` format and read the skill folder.

## Try it without installing

1. Download the repository and keep `skills/calibrate-ai-checks/` intact.
2. Open the repository folder in an agent that can read files.
3. Use this prompt:

> Read `skills/calibrate-ai-checks/SKILL.md` and follow it to write a check plan for this step: an AI assistant tags incoming support tickets with a product area and an urgency level, about 300 tickets a week. Tags route tickets to teams; a wrong tag delays a ticket by a day until someone reroutes it. A defect is a missing tag, a tag outside the allowed list, the wrong product area for what the ticket describes, or the wrong urgency by the team's definitions. So far 40 tickets were checked and 2 had a wrong urgency. A check takes about 30 seconds. The support lead can spend about 30 minutes a week on checking. Where something else you need is missing, state your assumption and go on.

Then compare with [`examples/example-check-plan.md`](examples/example-check-plan.md) for the shape of a complete plan.

## Install

Copy the whole `skills/calibrate-ai-checks/` folder, not just `SKILL.md`, to the skill location your agent uses. The result must end in `calibrate-ai-checks/SKILL.md`, without a doubled folder.

| Agent | Project folder | Personal folder |
|---|---|---|
| Claude Code | `.claude/skills/calibrate-ai-checks/` | `~/.claude/skills/calibrate-ai-checks/` |
| Codex | `.agents/skills/calibrate-ai-checks/` | `~/.agents/skills/calibrate-ai-checks/` |
| GitHub Copilot | `.github/skills/calibrate-ai-checks/` | `~/.copilot/skills/calibrate-ai-checks/` |

These are the hosts' documented defaults at the time of writing; check your agent's current documentation. If the destination already exists, compare versions before replacing it. Restart or refresh the agent if the skill does not appear.

Tested on: Codex desktop on macOS (arm64), with the folder copied to `~/.agents/skills/calibrate-ai-checks/`; a fresh agent found the skill by name and used it, with no restart. The project path and the other hosts in the table above have not been tested.

## First real use

> Use calibrate-ai-checks for <step>. It produces <output>, about <n> a week. A defect means <checklist>. So far <n> checked, <d> defects. An undetected defect <stays inside | moves on to ... | reaches ...>. A check takes <minutes>.

> Use calibrate-ai-checks to turn this list of AI errors into a miss log and tell me whether our review rate should change.

## How well does it work?

Two small tests so far, neither an accuracy figure:

- Two checking steps from the author's own studio, compared with a month of its records: neither had a written rate or a count of units checked. The plans set rates and named the missing counts.
- Two made-up steps, including one where the required checking was five times the time available: the plan worked through the options and left the lower rate to the owner. It is the [example](examples/example-check-plan.md).

The coordinating agent wrote the accounts and compared the results, and runners and coordinator were the same model. See [VALIDATION.md](https://github.com/trigpoint-pub/agent-skills/blob/main/docs/calibrate-ai-checks/VALIDATION.md) for the setup and limits.

## Sources

Trust calibration comes from Lee and See (2004); the slide in checking as automation proves reliable, and the weakness of instructions to verify, from Parasuraman and Manzey (2010); the limits of sustained watching from Mackworth (1948). The starting rates, floors and the 20-unit clean run are working defaults from Trigpoint (2026), and the cited research does not supply those numbers. Full references are in [SOURCES.md](https://github.com/trigpoint-pub/agent-skills/blob/main/docs/calibrate-ai-checks/SOURCES.md).

`VALIDATION.md`, `SOURCES.md` and the method article snapshot live in the repository under `docs/calibrate-ai-checks/`, not in this folder. Their GitHub links also work from an installed copy with web access.
