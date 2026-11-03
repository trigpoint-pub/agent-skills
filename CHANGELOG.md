# Changelog

Each skill has its own versions and tags (`{skill}-v{version}`).

## Collection maintenance (unreleased)

- Group the eight skills by task and link reading, practice, releases and evidence from the collection entry.
- Point current Inspect and Price Watch installation guides at the collection; clarify source-archive layout and helper working directories.
- Include the existing MIT license in all independently installable skill folders. Repository-only README links remain usable online after installation.
- Integrate the existing helper-test workflow and one shared Issue form. The migrated per-repo templates remain historical records.
- The repository moved to the `trigpoint-pub` organization. Issue, security-report, release and tutorial links in the skill folders, guides and validation records now use `github.com/trigpoint-pub/agent-skills`; old `anselbuilds/agent-skills` addresses redirect. Entries below keep the addresses that were current when they were written.
- Document consistent packaging and evidence for future releases. Published tags, assets, skill instructions and recorded test outcomes are unchanged.

## allocate-ai-work

### Unreleased

- Validation record: the status line now reads "0.1.0 experimental prerelease, 2026-11-02" instead of "release candidate, not yet released". No test result changed.
- Method snapshot (`docs/allocate-ai-work/method.md`): the GitHub link now reads `github.com/trigpoint-pub/agent-skills`, as on the article page. No other text changed.
- The skill's instructions and the `allocate-ai-work-v0.1.0` release are unchanged.

### 0.1.0, tag `allocate-ai-work-v0.1.0`, 2026-11-02

First public release, experimental. See `docs/allocate-ai-work/VALIDATION.md` for what was and was not tested.

## calibrate-ai-checks

### Unreleased

- Validation record: the status line now reads "0.1.0 experimental prerelease, 2026-11-02" instead of "release candidate, not yet released". No test result changed.
- Method snapshot (`docs/calibrate-ai-checks/method.md`): the GitHub link now reads `github.com/trigpoint-pub/agent-skills`, as on the article page. No other text changed.
- The skill's instructions and the `calibrate-ai-checks-v0.1.0` release are unchanged.

### 0.1.0, tag `calibrate-ai-checks-v0.1.0`, 2026-11-02

First public release, experimental. See `docs/calibrate-ai-checks/VALIDATION.md` for what was and was not tested.

## classify-ai-incident

### Unreleased

- Validation record: the status line now reads "0.1.0 experimental prerelease, 2026-11-02" instead of "release candidate, not yet released". No test result changed.
- Method snapshot (`docs/classify-ai-incident/method.md`): the GitHub link now reads `github.com/trigpoint-pub/agent-skills`, as on the article page. No other text changed.
- The skill's instructions and the `classify-ai-incident-v0.1.0` release are unchanged.

### 0.1.0, tag `classify-ai-incident-v0.1.0`, 2026-11-02

First public release, experimental. See `docs/classify-ai-incident/VALIDATION.md` for what was and was not tested.

## prompt-architect

### 0.2.0, 2026-11-01

- The source list is split into one file per vendor (`references/openai.md`, `references/anthropic.md`, `references/google.md`). `references/official-sources.md` now says which file to open, and Step 5 opens only the target vendor's file. Each vendor file pairs the points Step 5 asks for with the page to check first. The skill still ships no vendor conventions.
- Source list: the Claude "Adaptive thinking" entry now uses the page's current title and address, "Steering thinking"; the old address already redirected there. All 28 links rechecked on 2026-11-01.
- The skill README and the first-use tutorial link to the method article; the tutorial no longer gives the NotebookLM tool's version number.
- Validation: new check 10 (only the target vendor's file is opened), three named-model practice requests, and the 0.2.0 acceptance runs (section 2b).

### 0.1.0, tag `prompt-architect-v0.1.0`, 2026-10-26

First public release, experimental, by Ansel under MIT. Includes the task-method workflow, first-party vendor source list, installation instructions, and a bilingual [first-use tutorial](docs/prompt-architect/FIRST-USE.md).

Codex installation and discovery, revised practice cases and a naturally refused-fetch fallback were checked on macOS; see [VALIDATION.md](docs/prompt-architect/VALIDATION.md). The instruction body is unchanged from that tested candidate; the identical description is now quoted so strict YAML parsers accept the frontmatter. Generated prompts have not been evaluated on their target platforms with real inputs. A separate Trigpoint method article is not part of this release.

## concept-relations

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

Standardized the display name and documentation titles as **GitHub Agent Resource Review**. Author and maintainer attribution remains Ansel. The `inspect-github-agent-resources` identifier, folder path and invocation are unchanged.

Helper fixes (not yet in a release):
- An excluded directory other than the snapshot's top-level `.git` (for example a nested `node_modules`, `.venv`, `__pycache__` or `.git`) is now a coverage gap (`excluded-directory:<path>`). Such a scan is `partial` and exits 1, and a comparison reports incomplete coverage instead of "Included fingerprints match". Previously a script inside such a directory could change while both scans reported `complete`. `references/scanner.md` and `references/maintenance.md` describe the new rule.
- Both helpers now run when started through a symlink, such as a symlinked skill folder or a linked temporary directory. Previously `compare-snapshots.mjs` exited 0 with no output in that case, and the scanner did the same when the link had a different file name.
- Regression tests cover both fixes.

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
- Helper fix (not yet in a release): `watchlist.py` stores `expires_at` and `baseline.observed_at` in the extended ISO 8601 form, for example `2027-01-01T00:00:00+08:00`. It also reads basic-format times, `+HHMM` offsets and fractional seconds of any length the same way on every supported Python. Previously a record saved with such a timestamp under Python 3.11 or later made `list` fail under Python 3.9. Regression tests cover both cases.
- The skill's instructions and the `price-watch-v0.1.0` release are unchanged.

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
