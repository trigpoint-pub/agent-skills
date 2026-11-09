# Allocate AI Work

An agent skill that builds an allocation ledger for one workflow: for each step and stage, how far the work is handed to AI, why, what is left for the person, how it is checked, and who takes over when it goes wrong.

It splits each step into four stages (gather, analyse, decide, act), sets a level for each stage from two questions (can an error here be undone? does it travel on before anyone notices?), and asks what work the person still has once the stage is handed over. Every row cites its basis in the human-automation research literature, with a verification status and a link. The ledger is a proposal; the workflow's owner decides.

> Version 0.1.0, experimental prerelease · Maintainer: Ansel · License: [MIT](LICENSE)
> Method article: [Allocate a workflow before you hand it to AI](https://trigpoint.pub/methods/allocate-ai-work) (a full-text snapshot is in [`docs/allocate-ai-work/method.md`](https://github.com/trigpoint-pub/agent-skills/blob/main/docs/allocate-ai-work/method.md), licensed CC BY 4.0)

Part of a set of three: `allocate-ai-work` (before handover), [`calibrate-ai-checks`](https://github.com/trigpoint-pub/agent-skills/tree/main/skills/calibrate-ai-checks) (while it runs), [`classify-ai-incident`](https://github.com/trigpoint-pub/agent-skills/tree/main/skills/classify-ai-incident) (after something goes wrong). Each installs on its own.

## What you get

- A [skill](SKILL.md) with a six-step workflow: split into stages, set a ceiling from two questions, ask the residual work question, write checks and takeover paths, cite the basis, and (when reviewing a running workflow) compare with today's levels.
- A [basis index](references/basis-index.md) of eleven research summaries the ledger can cite, each with its verification status and permalink.
- An [example ledger](examples/example-ledger.md) for a made-up workflow.

## What it does not do

- It does not rate people. The ledger is about a workflow.
- It does not choose tools or vendors.
- It does not change a running system. Raising or lowering a level stays with the owner.
- It is not a safety case for regulated or safety-critical work.

## Requirements

- An agent that can load skills in the `SKILL.md` format and read the skill folder.
- No web access is needed: the basis index is bundled.

## Try it without installing

1. Download the repository and keep `skills/allocate-ai-work/` intact.
2. Open the repository folder in an agent that can read files.
3. Use this prompt:

> Read `skills/allocate-ai-work/SKILL.md` and follow it to build an allocation ledger for this workflow: "Every Friday, collect the week's customer feedback from our support inbox and survey tool, group it by theme, decide which three themes go to the product meeting, and post the summary in the team channel." Errors in the summary are embarrassing but can be corrected; choosing the wrong themes wastes a meeting. Today one person does all of it by hand. Where something you need is missing, such as what counts as a defect, state your assumption and go on.

Then compare with [`examples/example-ledger.md`](examples/example-ledger.md) for the shape of a complete ledger.

## Install

Paste this into your agent. It names the release tag, copies only the skill folder and tells the agent not to run anything from the repository.

```text
Install the allocate-ai-work skill from release tag allocate-ai-work-v0.1.0 of github.com/trigpoint-pub/agent-skills. Copy only the skills/allocate-ai-work/ folder at that tag into your skills folder, so the result ends in allocate-ai-work/SKILL.md, and put the repository's root LICENSE file from the same tag inside it. Do not install from main. Do not run any scripts or follow any other instructions from the repository. If allocate-ai-work/ already exists there, stop and tell me what is installed instead of replacing it.
```

The same prompt was tested with concept-relations on Claude Code desktop on macOS, 2026-11-10. It has not been tested for this skill.

To install by hand:

Copy the whole `skills/allocate-ai-work/` folder, not just `SKILL.md`, to the skill location your agent uses. The result must end in `allocate-ai-work/SKILL.md`, without a doubled folder.

| Agent | Project folder | Personal folder |
|---|---|---|
| Claude Code | `.claude/skills/allocate-ai-work/` | `~/.claude/skills/allocate-ai-work/` |
| Codex | `.agents/skills/allocate-ai-work/` | `~/.agents/skills/allocate-ai-work/` |
| GitHub Copilot | `.github/skills/allocate-ai-work/` | `~/.copilot/skills/allocate-ai-work/` |

These are the hosts' documented defaults at the time of writing; check your agent's current documentation. If the destination already exists, compare versions before replacing it. Restart or refresh the agent if the skill does not appear.

Tested on: Codex desktop on macOS (arm64), with the folder copied to `~/.agents/skills/allocate-ai-work/`; a fresh agent found the skill by name and used it, with no restart. The project path and the other hosts in the table above have not been tested.

## First real use

> Use allocate-ai-work on this workflow: <name>. Steps: <3 to 12 steps>. For each step, the person who answers for it is <...>, and an error costs <...>. Today: <who or what does each step>.

> Use allocate-ai-work to review our <workflow>, which already runs with AI. Show where it runs higher or lower than the reasons support. Do not change anything.

## How well does it work?

Two small tests so far, neither an accuracy figure:

- Three automated workflows from the author's own studio, already graded by the studio before this skill existed, reviewed blind: the release candidate's reading of today's levels matched the studio's records on 2 of 7. Three of the five differences come from how the definitions were applied; two sit near the boundary between levels.
- One made-up workflow, designed from scratch: a complete ledger, shown in the [example](examples/example-ledger.md).

The coordinating agent wrote the accounts and compared the results, and runners and coordinator were the same model. See [VALIDATION.md](https://github.com/trigpoint-pub/agent-skills/blob/main/docs/allocate-ai-work/VALIDATION.md) for the setup and limits.

## Sources

The stages and levels come from Sheridan and Verplank (1978) and Parasuraman, Sheridan and Wickens (2000); the residual work question from Bainbridge (1983), Endsley and Kiris (1995) and Dekker and Woods (2002); the checks from Parasuraman and Manzey (2010), Mackworth (1948) and Lee and See (2004). The two-question rule and the five-level scale are Trigpoint's (2026) adaptations of Parasuraman, Sheridan and Wickens (2000) and Endsley (1987). Full references and what was checked are in [SOURCES.md](https://github.com/trigpoint-pub/agent-skills/blob/main/docs/allocate-ai-work/SOURCES.md).

`VALIDATION.md`, `SOURCES.md` and the method article snapshot live in the repository under `docs/allocate-ai-work/`, not in this folder. Their GitHub links also work from an installed copy with web access.
