# Validation

What has been tested and what has not.

**Status:** release candidate, not yet released. Tests so far are small and were run on the author's own studio workflows. None is an accuracy figure.

## 1. Tests so far

**Setup, common to all runs**

- Each run was one fresh sub-agent given only the skill folder and written accounts of the workflows, with instructions not to open anything else, not to search, and not to ask questions.
- The coordinating agent wrote the accounts and compared the results. Runners and coordinator were the same model. This was not a blind or preregistered test.
- Two runs: the first candidate, and revision 1 (the release candidate). The revision was made for problems the first runner reported in the instructions, and re-run on all four workflows (§1.3).

### 1.1 Three running workflows (review mode)

Three automated workflows from the studio's own operations, each already graded by the studio, mechanism by mechanism, on its own internal five-level scale, written down before this skill existed. The accounts given to the runners described the steps, who answers for them, what errors cost, and what runs automatically today; they did not include the studio's grades.

| | First candidate | Revision 1 |
|---|---|---|
| The skill's reading of today's level ("Now") equals the studio's recorded level | 1 of 7 | 2 of 7 |

Of the five differences in the release candidate:

- Three come from how the definitions were applied: the skill read the stages as the scale defines them, and the studio's earlier records had not. Those are for the studio to review in its records.
- Two are near the boundary between levels (a background watcher started by a session; a report that surfaces items for a decision).

The first candidate rated a scheduled job that only prepares work at level 4. The revision fixed that, and the job's level then matched the studio's record.

Where the skill recommended a different level from today's, it recommended a lower one in most rows. Those recommendations are proposals for the owner; nothing was changed.

### 1.2 A made-up workflow (design mode)

A monthly client report for a freelance consultant, designed before any of it is handed over. Both runs produced a complete ledger, with every row carrying a reason, residual work, a check, a takeover path and basis fields copied exactly from the index. The release candidate's ledger is `skills/allocate-ai-work/examples/example-ledger.md`.

### 1.3 Changes made after the first run

- The scale now separates its levels by whether a person reviews the result before it takes effect (2 versus 3) and whether anyone is present (3 versus 4); a job that only prepares work stays at 2 even when it starts itself.
- "The person" is the human who answers for the stage; an AI agent doing a stage on their behalf is automation of that stage.
- The ceiling row "a stage whose outcome a named person must answer for" capped every stage, since someone answers for every step; it was replaced by "a stage that speaks or commits for a person: sends, publishes, pays, signs".
- Q2 is judged with the following stages at their recommended levels; sorting by fixed rules counts as Analyse; the evidence grades say what "theory" covers.

Known open points reported by the last run, not yet changed: the ceiling for a stage that only prepares work reads as 3 while the scale places such a stage at 2; Q2 can go in a circle when two adjacent stages could each hold the check; "sends" does not say whether a message to another automated system counts; a stage done sometimes by the owner and sometimes by an assistant has no single Now level; no default review interval.

**Cost:** each run wrote four ledgers in about 15 to 18 minutes of agent time (about 190,000 to 200,000 tokens per run, including reading the skill).

### 1.4 Changes made after these tests

The runs above were not repeated on these changes.

- What starts a job no longer decides level 3 versus 4; whether the person is present does. A background process that an AI agent starts and leaves running is at level 4 when its results take effect while the person is away. The skill now places the first boundary case in §1.1 at level 4.
- The level 4 ceiling row now covers a one-off run: a miss must be reported before its result is relied on.
- A stage whose errors fall into classes with different answers (most can be undone, one cannot) gets a ceiling for each class, provided something sorts the items before the stage acts. Items the sorting misses are listed as a residual risk for the owner to accept or refuse.

### 1.5 Release test on a second host, November 2026

- Host and setup as in §2: all three skills of the set installed, one fresh agent per run, with no parent conversation. It ran on the text after the changes in §1.4. Model and reasoning effort were not recorded.
- First run, the README "Try it" prompt: no ledger. The agent used `calibrate-ai-checks`, which was installed, to set the check rates, and stopped to ask the user to agree a defect checklist, as that skill requires before anything else. The prompt gave none.
- The prompt now ends: "Where something you need is missing, such as what counts as a defect, state your assumption and go on." Re-run with a new agent and the same three skills installed: a complete ledger with every output item, its assumptions listed, and a check plan for the stages at level 2.
- One run each. It shows that the prompt now runs to the end, not that the ledger is right.

## 2. Hosts

- All runs: sub-agents in Claude Code on macOS, reading the skill folder from a working directory. The skill was not installed, so discovery by an agent's skill loader was not tested.
- Release test, November 2026: Codex desktop on macOS, arm64. The skill folder was copied to `~/.agents/skills/allocate-ai-work/`, and a fresh agent listed the skill and loaded it by name, with no restart (§1.5). The app version, model and reasoning effort were not available to the test and are not recorded. The project path `.agents/skills/allocate-ai-work/` and the other hosts in the README were not tested.

## 3. Not yet tested

- Installation and discovery through the project paths listed in `skills/allocate-ai-work/README.md`, and on hosts other than Codex on macOS.
- Workflows written by people other than the author, and teams with more than one person.
- Whether a ledger, once adopted, changes how a workflow fails.
- Agreement between two runs on the same workflow.
