# Changelog

Each skill has its own versions and tags (`{skill}-v{version}`).

## Collection maintenance (unreleased)

- Group the eight skills by task and link reading, practice, releases and evidence from the collection entry.
- Point current Inspect and Price Watch installation guides at the collection; clarify source-archive layout and helper working directories.
- Include the existing MIT license in all independently installable skill folders. Repository-only README links remain usable online after installation.
- Integrate the existing helper-test workflow and one shared Issue form. The migrated per-repo templates remain historical records.
- The repository moved to the `trigpoint-pub` organization. Issue, security-report, release and tutorial links in the skill folders, guides and validation records now use `github.com/trigpoint-pub/agent-skills`; old `anselbuilds/agent-skills` addresses redirect. Entries below keep the addresses that were current when they were written.
- Document consistent packaging and evidence for future releases. Published tags, assets, skill instructions and recorded test outcomes are unchanged.
- Method article links in the skill READMEs, the method snapshots and the prompt-architect tutorial now use the article addresses named after each skill, for example `trigpoint.pub/methods/allocate-ai-work`. The old addresses redirect. No other text changed.
- Each skill README's Install section now starts with a prompt to paste into an agent. It names the skill's latest release tag, copies only the skill folder and tells the agent not to run scripts or follow other repository instructions. The manual steps remain below it. Skill instructions, tags and releases are unchanged.

## allocate-ai-work

### Unreleased

- Validation record: the status line now reads "0.1.0 experimental prerelease, 2026-11-02" instead of "release candidate, not yet released". No test result changed.
- Method snapshot (`docs/allocate-ai-work/method.md`): the GitHub link now reads `github.com/trigpoint-pub/agent-skills`, as on the article page. No other text changed.
- Attribution correction. The skill, its README, `SOURCES.md` and the method snapshot used to say that the two questions and Rule 1 are not part of the published level-of-automation models, and that the folding into five levels is the skill's own. A prior-art check found that Parasuraman, Sheridan and Wickens (2000) already use the costs of decision and action outcomes as a secondary criterion for choosing levels and advise keeping decision automation at a moderate level or below in high-risk situations, and that Endsley (1987), as reported by Kaber and Endsley (2004), already has five levels with the same cut points. These texts now cite both and name Trigpoint (2026) as the source of what the skill changed. Kaber and Endsley (2004) is added to `SOURCES.md`.
- Method snapshot: now article version 1.1, with the attribution changes, the article's correction note and its section "When to run it again".
- In the skill's instructions only the attribution sentences changed, including the ledger header; the steps, levels and rules are the same. The `allocate-ai-work-v0.1.0` release is unchanged.

### 0.1.0, tag `allocate-ai-work-v0.1.0`, 2026-11-02

First public release, experimental. See `docs/allocate-ai-work/VALIDATION.md` for what was and was not tested.

## calibrate-ai-checks

### Unreleased

- Validation record: the status line now reads "0.1.0 experimental prerelease, 2026-11-02" instead of "release candidate, not yet released". No test result changed.
- Method snapshot (`docs/calibrate-ai-checks/method.md`): the GitHub link now reads `github.com/trigpoint-pub/agent-skills`, as on the article page. No other text changed.
- Attribution: the working defaults and the sampling inference are now credited to Trigpoint (2026) instead of "the studio", in the skill, its README, `SOURCES.md` and the method snapshot (now article version 1.1). No rule, number or test result changed.
- The `calibrate-ai-checks-v0.1.0` release is unchanged.

### 0.1.0, tag `calibrate-ai-checks-v0.1.0`, 2026-11-02

First public release, experimental. See `docs/calibrate-ai-checks/VALIDATION.md` for what was and was not tested.

## classify-ai-incident

### Unreleased

- Validation record: the status line now reads "0.1.0 experimental prerelease, 2026-11-02" instead of "release candidate, not yet released". No test result changed.
- Method snapshot (`docs/classify-ai-incident/method.md`): the GitHub link now reads `github.com/trigpoint-pub/agent-skills`, as on the article page. No other text changed.
- Attribution: the abuse checklist and the fix table are now credited to Trigpoint (2026), and "fix the mechanism, not the person" cites the system approach of Reason (2000), added to `SOURCES.md`. Changed in the skill, its README, `SOURCES.md` and the method snapshot (now article version 1.1). No category, rule or test result changed.
- The `classify-ai-incident-v0.1.0` release is unchanged.

### 0.1.0, tag `classify-ai-incident-v0.1.0`, 2026-11-02

First public release, experimental. See `docs/classify-ai-incident/VALIDATION.md` for what was and was not tested.

## prompt-architect

### 0.3.0, tag `prompt-architect-v0.3.0`, 2026-11-07

- Step 2 is now "Break down the task": it writes down the task's sub-tasks, the decisions they call for and what each decision rests on, instead of a sequence of reasoning steps. Whether the prompt should ask the model to reason step by step or check its own work moves to Step 5, where it is answered from the vendor's pages for the target model. The description, Step 6 rule 3 and the README say the same.
- `SOURCES.md`: the task method is now credited as an arrangement by Trigpoint (2026) whose components follow the vendors' own guidance, instead of "our own working method".
- Validation: check 1 now asks for a real breakdown of the task; an instruction to reason step by step or to self-check is judged under check 6. The 0.3.0 acceptance run (section 2c) ran R1 to R6 and N1 to N3 on Claude Code with the skill path given; eight passed, and R2 failed check 6 on a usage note that came from the test host's own notes.
- The README, the first-use tutorial and the collection README point to the 0.3.0 release.

### 0.2.0, 2026-11-01

- The source list is split into one file per vendor (`references/openai.md`, `references/anthropic.md`, `references/google.md`). `references/official-sources.md` now says which file to open, and Step 5 opens only the target vendor's file. Each vendor file pairs the points Step 5 asks for with the page to check first. The skill still ships no vendor conventions.
- Source list: the Claude "Adaptive thinking" entry now uses the page's current title and address, "Steering thinking"; the old address already redirected there. All 28 links rechecked on 2026-11-01.
- The skill README and the first-use tutorial link to the method article; the tutorial no longer gives the NotebookLM tool's version number.
- Validation: new check 10 (only the target vendor's file is opened), three named-model practice requests, and the 0.2.0 acceptance runs (section 2b).

### 0.1.0, tag `prompt-architect-v0.1.0`, 2026-10-26

First public release, experimental, by Ansel under MIT. Includes the task-method workflow, first-party vendor source list, installation instructions, and a bilingual [first-use tutorial](docs/prompt-architect/FIRST-USE.md).

Codex installation and discovery, revised practice cases and a naturally refused-fetch fallback were checked on macOS; see [VALIDATION.md](docs/prompt-architect/VALIDATION.md). The instruction body is unchanged from that tested candidate; the identical description is now quoted so strict YAML parsers accept the frontmatter. Generated prompts have not been evaluated on their target platforms with real inputs. A separate Trigpoint method article is not part of this release.

## concept-relations

### Unreleased

- Validation record: §7 no longer lists as untested what the October 2026 release test in §6 covered, namely installation and discovery through the Codex user path and the checking procedure (rules 2, 3 and 4) on the README example. No test result changed.
- The skill's instructions and the `concept-relations-v0.1.0` release are unchanged.

### 0.1.0, tag `concept-relations-v0.1.0`, 2026-10-28

First public release, experimental. Vocabulary v0.1. See `docs/concept-relations/VALIDATION.md` for what was and was not tested.

## red-team-gate

### Unreleased

- The skill README is reorganized: when the skill fits, why the review is kept separate, how to read a report, and a practice prompt that keeps the example report and answer key out of view until the review is finished. It links the method article in English and Traditional Chinese.
- Validation record: the status line now records the 0.1.0 publication on 2026-10-24 and says the acceptance results describe the release candidate, not a new test of the released package. No test result changed.
- The skill's instructions and the `red-team-gate-v0.1.0` release are unchanged.

### 0.1.0, tag `red-team-gate-v0.1.0`, 2026-10-24

First public release, experimental. Tested on Codex on macOS; see `docs/red-team-gate/VALIDATION.md` for what was and was not tested.

## inspect-github-agent-resources

### Unreleased

Standardized the display name and documentation titles as **GitHub Agent Resource Review**. Author and maintainer attribution remains Ansel. The `inspect-github-agent-resources` identifier, folder path, invocation and behavior are unchanged.

Attribution: the skill README's "Sources and attribution" section now names the working choices that are Trigpoint's (2026): the procedure as a whole, the four evidence labels, the order of the four dispositions, the starting scope budget, and re-reviewing only the conclusions a version change affects. It lists earlier forms of the underlying ideas from a prior-art check in November 2026; none is claimed as new. The new `docs/inspect-github-agent-resources/SOURCES.md` gives the full references and how they were checked. The skill's instructions, helpers and behavior are unchanged, and the `inspect-github-agent-resources-v0.1.0` release is unchanged.

### 0.1.0, tag `inspect-github-agent-resources-v0.1.0`, 2026-10-24

Moved from anselbuilds/inspect-github-agent-resources, release v0.1.0 (commit 2d43edf0). The content is the same as that release, except that the links for reporting issues and security problems now point to this repository, because the old repository is archived.

Relocated files:
- `.github/ISSUE_TEMPLATE/bug_report.yml` -> `docs/inspect-github-agent-resources/.github/ISSUE_TEMPLATE/bug_report.yml`.
- `.gitignore` -> `docs/inspect-github-agent-resources/.gitignore`.
- `CHANGELOG.md` -> `docs/inspect-github-agent-resources/CHANGELOG.md`.
- `SECURITY.md` -> `docs/inspect-github-agent-resources/SECURITY.md`.
- `VALIDATION.md` -> `docs/inspect-github-agent-resources/VALIDATION.md`.
- `README.md` -> `docs/inspect-github-agent-resources/README.md`.

The original `skills/inspect-github-agent-resources/README.md` is retained byte-for-byte. Only relocation paths/relative links and the explicitly listed reporting URLs differ.

Content/path changes:
- `docs/inspect-github-agent-resources/README.md`: `](LICENSE)` -> `](../../LICENSE)` (2 occurrence(s)).
- `docs/inspect-github-agent-resources/README.md`: `](skills/inspect-github-agent-resources/SKILL.md)` -> `](../../skills/inspect-github-agent-resources/SKILL.md)` (1 occurrence(s)).
- `docs/inspect-github-agent-resources/README.md`: `](skills/inspect-github-agent-resources/examples/review-example.md)` -> `](../../skills/inspect-github-agent-resources/examples/review-example.md)` (2 occurrence(s)).
- `docs/inspect-github-agent-resources/README.md`: `](skills/inspect-github-agent-resources/references/scanner.md)` -> `](../../skills/inspect-github-agent-resources/references/scanner.md)` (1 occurrence(s)).
- `docs/inspect-github-agent-resources/README.md`: `](skills/inspect-github-agent-resources/README.md)` -> `](../../skills/inspect-github-agent-resources/README.md)` (1 occurrence(s)).
- `docs/inspect-github-agent-resources/SECURITY.md`: `https://github.com/anselbuilds/inspect-github-agent-resources/issues` -> `https://github.com/anselbuilds/agent-skills/issues` (1 occurrence(s)).
- `docs/inspect-github-agent-resources/SECURITY.md`: `https://github.com/anselbuilds/inspect-github-agent-resources/security/advisories/new` -> `https://github.com/anselbuilds/agent-skills/security/advisories/new` (1 occurrence(s)).
- `skills/inspect-github-agent-resources/SECURITY.md`: `https://github.com/anselbuilds/inspect-github-agent-resources/issues` -> `https://github.com/anselbuilds/agent-skills/issues` (1 occurrence(s)).
- `skills/inspect-github-agent-resources/SECURITY.md`: `https://github.com/anselbuilds/inspect-github-agent-resources/security/advisories/new` -> `https://github.com/anselbuilds/agent-skills/security/advisories/new` (1 occurrence(s)).

## price-watch

### Unreleased

- Added a bilingual first-use tutorial, [`docs/price-watch/FIRST-USE.md`](docs/price-watch/FIRST-USE.md).
- The skill's instructions, helper scripts and the `price-watch-v0.1.0` release are unchanged.

### 0.1.0, tag `price-watch-v0.1.0`, 2026-10-24

Moved from anselbuilds/safari-price-watch, release v0.1.0 (commit 408477fe). The installable name `price-watch` is unchanged. The content is the same as that release, except that the links for reporting issues and security problems now point to this repository, because the old repository is archived.

Relocated files:
- `.github/ISSUE_TEMPLATE/bug_report.yml` -> `docs/price-watch/.github/ISSUE_TEMPLATE/bug_report.yml`.
- `.gitignore` -> `docs/price-watch/.gitignore`.
- `CHANGELOG.md` -> `docs/price-watch/CHANGELOG.md`.
- `README.zh-Hant.md` -> `docs/price-watch/README.zh-Hant.md`.
- `SECURITY.md` -> `docs/price-watch/SECURITY.md`.
- `VALIDATION.md` -> `docs/price-watch/VALIDATION.md`.
- `tests/test_watchlist.py` -> `tests/price-watch/test_watchlist.py`.
- `README.md` -> `docs/price-watch/README.md`.

The original `skills/price-watch/README.md` is retained, with only its two explicitly authorized reporting URLs changed; all other bytes match the original. Only relocation paths/relative links and the explicitly listed reporting URLs differ.

Content/path changes:
- `docs/price-watch/README.zh-Hant.md`: `](README.md)` -> `](https://github.com/anselbuilds/safari-price-watch/blob/408477fed8ee2b00af4759da69b4c7b90b00d2d2/README.md)` (1 occurrence(s)).
- `docs/price-watch/README.zh-Hant.md`: `](LICENSE)` -> `](../../LICENSE)` (1 occurrence(s)).
- `docs/price-watch/README.zh-Hant.md`: `](skills/price-watch/references/registry.md)` -> `](../../skills/price-watch/references/registry.md)` (1 occurrence(s)).
- `tests/price-watch/test_watchlist.py`: `Path(__file__).resolve().parents[1]` -> `Path(__file__).resolve().parents[2]` (1 occurrence(s)).
- `docs/price-watch/VALIDATION.md`: `discover -s tests -v` -> `discover -s tests/price-watch -v` (1 occurrence(s)).
- `docs/price-watch/README.zh-Hant.md`: `discover -s tests -v` -> `discover -s tests/price-watch -v` (1 occurrence(s)).
- `docs/price-watch/README.md`: `](LICENSE)` -> `](../../LICENSE)` (1 occurrence(s)).
- `docs/price-watch/README.md`: `](skills/price-watch/references/registry.md)` -> `](../../skills/price-watch/references/registry.md)` (1 occurrence(s)).
- `docs/price-watch/README.md`: `](skills/price-watch/README.md)` -> `](../../skills/price-watch/README.md)` (1 occurrence(s)).
- `docs/price-watch/README.md`: `discover -s tests -v` -> `discover -s tests/price-watch -v` (1 occurrence(s)).
- `docs/price-watch/SECURITY.md`: `https://github.com/anselbuilds/safari-price-watch/issues` -> `https://github.com/anselbuilds/agent-skills/issues` (1 occurrence(s)).
- `docs/price-watch/SECURITY.md`: `https://github.com/anselbuilds/safari-price-watch/security/advisories/new` -> `https://github.com/anselbuilds/agent-skills/security/advisories/new` (1 occurrence(s)).
- `skills/price-watch/README.md`: `https://github.com/anselbuilds/safari-price-watch/issues` -> `https://github.com/anselbuilds/agent-skills/issues` (1 occurrence(s)).
- `skills/price-watch/README.md`: `https://github.com/anselbuilds/safari-price-watch/security/advisories/new` -> `https://github.com/anselbuilds/agent-skills/security/advisories/new` (1 occurrence(s)).
