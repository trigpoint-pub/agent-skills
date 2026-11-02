# Validation

What has been tested and what has not.

**Status:** release candidate, not yet released. Tests so far are small and were run on the author's own studio steps and on made-up steps. None is an accuracy figure.

## 1. Tests so far

**Setup, common to all runs**

- Each run was one fresh sub-agent given only the skill folder and written accounts of the steps, with instructions not to open anything else, not to search, and not to ask questions. Where the skill says to ask the owner (for example, the checking budget), the runner had to assume and record the assumption.
- The coordinating agent wrote the accounts and compared the results. Runners and coordinator were the same model. This was not a blind or preregistered test.
- Four runs: the first candidate and three revisions; revision 3 is the release candidate. Each revision was made for problems the previous runner reported in the instructions and re-run on every step (§1.3).

### 1.1 Two checking steps already running in the studio

Accepting deliverables returned by an external AI agent, and using facts that sub-agents gather inside a working session. The comparison is with what the studio actually did over one month, from its own records.

- Neither step had a written check rate.
- Neither step kept a count of units checked, so the plans had to report "no record" for most classes, and the classes that move on or go public came out at every unit.
- The workload step put the owner's share of the checking at about half an hour to an hour a week. The first candidate did not use the cost of a check at all; that was the largest change (§1.3).

### 1.2 Two made-up steps

- Supplier invoice extraction: tier C (a wrong total is paid), every unit, within the assumed budget.
- Support ticket tagging: tier B, every unit after two defects, five times over the stated budget. The release candidate's plan worked through the workload options, put an AI reviewer to the owner as a decision, and refused to treat a lower rate as accepted until the owner decides. It is `skills/calibrate-ai-checks/examples/example-check-plan.md`.

### 1.3 Changes made after the runs

- Revision 1: a workload step that uses the cost of a check; large units split into claims or sections; an AI reviewer's verdicts sampled by the person; "eligible" for a lower rate rather than lowered automatically; an upper bound when defects were found; separate handling for defects found by sample checks, by machine checks, and missed.
- Revision 2: a default sample rate for an AI reviewer; the owner may go below the floor only as a recorded, accepted risk; more values for "found by"; checks on the whole output; what the evidence grade covers.
- Revision 3: a defect caught by a safeguard designed for it later in the workflow (a reroute, a reconciliation) is no longer a miss. Before this, every routine reroute on a high-volume step sent it back to checking every unit, so sampling could never be reached. Also: the exact binomial bound when defects were found; "not recorded" counts treated as no record; an assistant working alongside the person counts as an AI reviewer.

Known open points reported by the last run, not yet changed: the AI reviewer's sample rate is the same for every tier; the skill does not say what rate runs while the owner is deciding; one unit can hold fields of different tiers; "no record" can hide known defect counts; a reversed reviewer verdict is not covered by the miss definition.

**Cost:** each run wrote four plans in about 8 to 14 minutes of agent time (about 130,000 to 175,000 tokens per run, including reading the skill).

### 1.4 Changes made after these tests

The runs above were not repeated on this change.

- Checking a unit means opening the unit or its sources. A person who decides each unit from an AI reviewer's summary has not checked it; those decisions are not judgment checks and do not replace the re-check of the reviewer's verdicts.

### 1.5 Release test on a second host, November 2026

- Host and setup as in §2: one fresh agent per run, with no parent conversation. It ran on the text after the change in §1.4. Model and reasoning effort were not recorded.
- First run, the README "Try it" prompt: no plan. The agent asked the user to agree a defect checklist first, as the skill requires; the prompt gave none.
- The prompt now states the defect checklist and ends: "Where something else you need is missing, state your assumption and go on." Re-run with a new agent: a complete plan with every output item and a miss log, its assumptions listed.
- One run each. It shows that the prompt now runs to the end, not that the plan is right.

## 2. Hosts

- All runs: sub-agents in Claude Code on macOS, reading the skill folder from a working directory. The skill was not installed, so discovery by an agent's skill loader was not tested.
- Release test, November 2026: Codex desktop on macOS, arm64. The skill folder was copied to `~/.agents/skills/calibrate-ai-checks/`, and a fresh agent listed the skill and loaded it by name, with no restart (§1.5). The app version, model and reasoning effort were not available to the test and are not recorded. The project path `.agents/skills/calibrate-ai-checks/` and the other hosts in the README were not tested.

## 3. Not yet tested

- Installation and discovery through the project paths listed in `skills/calibrate-ai-checks/README.md`, and on hosts other than Codex on macOS.
- Whether a plan, once followed, catches more defects or changes trust; the miss log has not been run over time.
- Steps described by people other than the author.
- Agreement between two runs on the same step.
