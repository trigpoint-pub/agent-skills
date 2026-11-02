# Classify AI Incident

An agent skill that classifies one incident involving AI or other automation as use, misuse, disuse or abuse, and points the fix at a mechanism rather than at "be more careful".

The four categories come from Parasuraman and Riley (1997). The skill restates the incident as facts, compares how much people relied on the automation with how reliable it actually was, always asks separately whether the setup itself ignored the people who had to work with it, and returns a short record with the label, its evidence, and the direction of the fix.

> Version 0.1.0, experimental prerelease · Maintainer: Ansel · License: [MIT](LICENSE)
> Method article: [Classify an AI incident before you fix it](https://trigpoint.pub/methods/classify-an-incident) (a full-text snapshot is in [`docs/classify-ai-incident/method.md`](https://github.com/trigpoint-pub/agent-skills/blob/main/docs/classify-ai-incident/method.md), licensed CC BY 4.0)

Part of a set of three: [`allocate-ai-work`](https://github.com/trigpoint-pub/agent-skills/tree/main/skills/allocate-ai-work) (before handover), [`calibrate-ai-checks`](https://github.com/trigpoint-pub/agent-skills/tree/main/skills/calibrate-ai-checks) (while it runs), `classify-ai-incident` (after something goes wrong). Each installs on its own.

## What you get

- A [skill](SKILL.md) with a five-step workflow: restate the facts, compare reliance with reliability, ask the abuse question, label with evidence, and set the fix direction.
- A [basis index](references/basis-index.md) of five research summaries the record can cite, each with its verification status and permalink.
- [Practice incidents](examples/practice-incidents.md), with the answer key in [VALIDATION.md](https://github.com/trigpoint-pub/agent-skills/blob/main/docs/classify-ai-incident/VALIDATION.md).

## What it does not do

- It does not judge a person's performance. It classifies the relationship between people and the automation.
- It does not debug the model or the code.
- It does not handle many incidents at once; run one record per incident.

## Requirements

- An agent that can load skills in the `SKILL.md` format and read the skill folder.

## Try it without installing

1. Download the repository and keep `skills/classify-ai-incident/` intact.
2. Open the repository folder in an agent that can read files.
3. Use this prompt:

> Read `skills/classify-ai-incident/SKILL.md` and follow it to classify practice incident P3 in `skills/classify-ai-incident/examples/practice-incidents.md`. Do not open anything under `docs/` until the record is written.

Then compare with the answer key in [VALIDATION.md](https://github.com/trigpoint-pub/agent-skills/blob/main/docs/classify-ai-incident/VALIDATION.md).

## Install

Copy the whole `skills/classify-ai-incident/` folder, not just `SKILL.md`, to the skill location your agent uses. The result must end in `classify-ai-incident/SKILL.md`, without a doubled folder. The answer key stays in `docs/classify-ai-incident/` and is not part of the installed folder.

| Agent | Project folder | Personal folder |
|---|---|---|
| Claude Code | `.claude/skills/classify-ai-incident/` | `~/.claude/skills/classify-ai-incident/` |
| Codex | `.agents/skills/classify-ai-incident/` | `~/.agents/skills/classify-ai-incident/` |
| GitHub Copilot | `.github/skills/classify-ai-incident/` | `~/.copilot/skills/classify-ai-incident/` |

These are the hosts' documented defaults at the time of writing; check your agent's current documentation. If the destination already exists, compare versions before replacing it. Restart or refresh the agent if the skill does not appear.

Tested on: Codex desktop on macOS (arm64), with the folder copied to `~/.agents/skills/classify-ai-incident/`; a fresh agent found the skill by name and used it, with no restart. The project path and the other hosts in the table above have not been tested.

## First real use

> Use classify-ai-incident on this: <what the automation was, what it did, what people did, how it was noticed, what it cost>.

> Use classify-ai-incident on the incident in this post-mortem. Separate the facts from the blame first.

## How well does it work?

Two small tests so far, neither an accuracy figure:

- Six practice incidents with a fixed answer key, classified by a fresh agent with only this folder, three times across three wordings of the skill: all six within the key each time.
- Six incidents from the author's own records that had been labelled earlier with the same four categories, classified blind: the release candidate agreed on three. In two of the other three, the skill's reading was judged at least as defensible as the earlier label; one switched with the wording about settings, which is the least stable part of the method.

The coordinating agent wrote the incidents and scored the results, and runners and coordinator were the same model. See [VALIDATION.md](https://github.com/trigpoint-pub/agent-skills/blob/main/docs/classify-ai-incident/VALIDATION.md) for the setup and limits.

## Sources

The four categories are from Parasuraman and Riley (1997); who holds the switch between levels is from Miller and Parasuraman (2007); trust calibration from Lee and See (2004); attention-based failures from Parasuraman and Manzey (2010). The abuse checklist and the fix table are the studio's own working choices. Full references are in [SOURCES.md](https://github.com/trigpoint-pub/agent-skills/blob/main/docs/classify-ai-incident/SOURCES.md).

`VALIDATION.md`, `SOURCES.md` and the method article snapshot live in the repository under `docs/classify-ai-incident/`, not in this folder, their GitHub links also work from an installed copy with web access.
