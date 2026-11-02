# Validation

What has been tested, what has not, and the answer key for the practice incidents.

**Status:** 0.1.0 experimental prerelease, 2026-11-02. Tests so far are small and were run by the author's studio, on two agent hosts. None is an accuracy figure.

## 1. Tests so far

**Setup, common to all runs**

- Each run was one fresh sub-agent given only the skill folder and the incident accounts, with instructions not to open anything else, not to search, and not to ask questions. It never saw an answer key or earlier outputs.
- The coordinating agent wrote the practice incidents and the answer key before the first run, wrote the neutral accounts of the studio's own incidents, and scored the results. The runners and the coordinator were the same model. This was not a blind or preregistered test.
- Three runs, one per wording of the skill: the first candidate, revision 1, and revision 2 (the release candidate). Revisions were made only for problems the runners reported in the instructions, and each was re-run on all twelve incidents (§1.3).

### 1.1 Practice incidents P1 to P6

All three runs fell within the answer key (§4) on all six incidents: 6 of 6 each time. P5 was given both of its required labels each time.

### 1.2 Six incidents from the studio's own records

Before this skill existed, the studio had already sorted six of its own automation incidents with the same four categories. They were restated as neutral accounts, without the earlier labels, and classified blind. The incidents themselves stay private; this section reports only the comparison.

| | First candidate | Revision 1 | Revision 2 |
|---|---|---|---|
| Same category as the studio's earlier label | 3 of 6 | 3 of 6, plus 1 as secondary | 3 of 6 |

- Two incidents agreed in every run.
- Two disagreed in every run. In both, the skill found that people relied on the automation about as much as its record justified and put the fault in the automation itself, where the earlier label had recorded a consequence (a tool set aside after it failed) or a risk (false alarms that could erode trust). For the false-alarm incident, a later check of the studio's records showed every false alarm still went on the priority list and was fixed within two days: the loss of trust the earlier label anticipated did not happen, and the skill's reading matches the record. For the other, on review, the author judged the skill's reading at least as defensible as the earlier label.
- One moved into agreement once the skill said that an AI agent can be the one relying on a tool (revision 1).
- One switched between abuse and use as the wording about settings changed. The line between a setting chosen without care and a setting chosen without regard for the people is the least stable part of the method.

### 1.3 Changes made after the runs

- Revision 1: who counts as "people" when an AI agent ran or relied on the tool; how to choose the primary label; criteria for confidence; how to cite no basis.
- Revision 2: revision 1 had pushed every wrong setting towards abuse (abuse appeared in 10 of 12 records); the rule now limits abuse to settings chosen without regard for the people who supervise or rely on the automation. Also: where to mark a near miss, and one evidence line per label.

Known open points reported by the last run, not yet changed: a setting chosen carelessly but not in disregard of people has no explicit rule; the primary-label rule (whose fix prevents it most directly) can disagree with the reliance test; the "use" fix row has no place to recommend moving a check.

**Cost:** each run classified twelve incidents in about 7.5 to 9 minutes of agent time (about 130,000 to 140,000 tokens per run, including reading the skill).

### 1.4 Changes made after these tests

The runs above were not repeated on these changes. The coordinating agent re-read the answer key in §4 against them; it is unchanged.

- Chains: when one automated step feeds another and a person relies on the last, the record classifies one link: the step where the defect entered, and the next party that relied on its output.
- A "no" to an abuse question counts only if the incident turned on it; a gap it did not turn on is listed as a separate fix. Whether a gap is local or runs through the whole setup changes nothing on its own.
- Practice incident P5 gained one sentence: the founder had connected the agent that morning, and this was its first batch. Without it, the account gave no fact about the agent's reliability, so a runner that followed the skill's rule for missing facts could not establish misuse, although the answer key requires it. The key's labels are unchanged; its reason for P5 now cites the first batch.

### 1.5 Release test on a second host, November 2026

- Host and setup as in §2: one fresh agent per run, with no parent conversation. Each record was written before the coordinating agent compared it with the answer key; the runner never saw the key. It ran on the text after the changes in §1.4. Model and reasoning effort were not recorded.
- First run: the README "Try it" prompt (P3) fell within the key. Through the installed skill, P1 to P6 gave 5 of 6 within the key. P5 was given abuse only: its account then had no fact about the agent's reliability, so the runner recorded that as unknown instead of inferring misuse, as the skill says to. P5 then gained one sentence (§1.4).
- Re-run of P1 to P6 on the revised account, with a new agent: 6 of 6 within the key, P5 with both required labels.
- One runner per run, on one host. Not an accuracy figure.

## 2. Hosts

- All runs: sub-agents in Claude Code on macOS, reading the skill folder from a working directory. The skill was not installed, so discovery by an agent's skill loader was not tested.
- Release test, November 2026: Codex desktop on macOS, arm64. The skill folder was copied to `~/.agents/skills/classify-ai-incident/`, and a fresh agent listed the skill and loaded it by name, with no restart (§1.5). The app version, model and reasoning effort were not available to the test and are not recorded. The project path `.agents/skills/classify-ai-incident/` and the other hosts in the README were not tested.

## 3. Not yet tested

- Installation and discovery through the project paths listed in `skills/classify-ai-incident/README.md`, and on hosts other than Codex on macOS.
- Incidents written by people other than the author, and long post-mortems.
- Agreement between two independent reviewers classifying the same incident.
- Any measured effect on what teams actually change after an incident.

## 4. Answer key for the practice incidents

"Acceptable" lists every label that a careful reading supports. A record that names an unacceptable primary label, or misses a label marked required, does not match.

| Incident | Intended | Acceptable | Not acceptable | Why |
|---|---|---|---|---|
| P1 Invoice reminders | misuse | primary misuse; secondary none, or abuse at low confidence | disuse; use; abuse as primary | The setup gave her every amount before sending; approvals shrank to seconds after months of correct drafts. Reliance rose above what an every-item approval should mean. |
| P2 Action-item flags | disuse | primary disuse; secondary abuse acceptable (the early false-alarm rate, and an email as the only notice of the fix) | misuse; use | The tool was accurate when the item was missed; the team had stopped reading flags because of earlier false alarms. |
| P3 Automatic dependency updates | abuse | primary abuse; secondary none | misuse or use as primary | Required by a manager over known thin tests; acts on its own into production; "watch the dashboard" as the safeguard. |
| P4 Date format in exports | use | primary use, with abuse acceptable as secondary (the review sat before the export step); or primary abuse at medium or low confidence for the same reason | misuse; disuse | Reliance matched a long, stable record on what the reviewers could see; the defect arose after their check, in the automation itself. |
| P5 Email agent | abuse and misuse | both labels required, in either order | a record with only one of the two; disuse; use | No step showed the actual reply before an irreversible send (setup), and she approved a forty-item plan at a glance on the agent's first batch, with no record to justify that much trust (reliance). |
| P6 Calendar assistant | abuse | primary abuse | misuse; disuse; use | A default-on feature switched the assistant from suggesting to accepting by itself; nobody chose it. |
