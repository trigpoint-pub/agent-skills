# Agent skills

Practical agent skills for [Trigpoint](https://trigpoint.pub) methods. Go from a method article to a tutorial, then try the corresponding skill. Created and maintained by Ansel. Each folder under `skills/` installs on its own.

Skill folder names and the `name` field in `SKILL.md` are the technical identifiers. Display names describe the task; author and maintainer credits are listed separately.

## Choose by task

| Task | Skill | Start here |
|---|---|---|
| **Manage AI work:** decide what to hand over | [allocate-ai-work](skills/allocate-ai-work/) | [Try an allocation ledger](skills/allocate-ai-work/README.md#try-it-without-installing) |
| Set checks while an AI step runs | [calibrate-ai-checks](skills/calibrate-ai-checks/) | [Try a check plan](skills/calibrate-ai-checks/README.md#try-it-without-installing) |
| Diagnose an incident before choosing a fix | [classify-ai-incident](skills/classify-ai-incident/) | [Classify a practice incident](skills/classify-ai-incident/README.md#try-it-without-installing) |
| **Claims and knowledge:** challenge one claim | [red-team-gate](skills/red-team-gate/) | [Try a claim](skills/red-team-gate/README.md#try-it-without-installing) · [Read a report](skills/red-team-gate/README.md#read-a-report) |
| Propose or check typed links between notes | [concept-relations](skills/concept-relations/) | [Try the six-link example](skills/concept-relations/README.md#try-it-without-installing) |
| **Agent tools:** write a prompt for a task and platform | [prompt-architect](skills/prompt-architect/) | [First-use tutorial](docs/prompt-architect/FIRST-USE.md) |
| Inspect an agent resource before trying it | [inspect-github-agent-resources](skills/inspect-github-agent-resources/) | [Try a synthetic review](docs/inspect-github-agent-resources/README.md#try-it-without-installation) |
| **Safari utility:** prepare price-watch conditions | [price-watch](skills/price-watch/) | [First-use tutorial](docs/price-watch/FIRST-USE.md) |

For an AI workflow, start with allocation, set its checks, and use incident classification when something goes wrong. These three skills also work independently. Safari performs actual monitoring and notifications; price-watch only prepares and records the setup.

Looking for the research first? [Trigpoint reading notes](https://github.com/trigpoint-pub/trigpoint) provide the reading and citation mirror. Method articles linked from the individual skill READMEs explain how the methods are applied; [trigpoint.pub](https://trigpoint.pub) is the source of record.

## Releases and evidence

The versions below are published prereleases. Documentation and packaging changes on `main` may be newer than their release archives; see [unreleased changes](CHANGELOG.md#collection-maintenance-unreleased). Choose a skill-specific release for reproducible use.

| Skill / release | Version | Status | Verified on |
|---|---|---|---|
| [red-team-gate](https://github.com/trigpoint-pub/agent-skills/releases/tag/red-team-gate-v0.1.0) · [Evidence](docs/red-team-gate/VALIDATION.md) | 0.1.0 | experimental prerelease | Codex on macOS |
| [inspect-github-agent-resources](https://github.com/trigpoint-pub/agent-skills/releases/tag/inspect-github-agent-resources-v0.1.0) · [Evidence](docs/inspect-github-agent-resources/VALIDATION.md) | 0.1.0 | trial release (prerelease) | macOS arm64 helper tests; host-native discovery untested |
| [price-watch](https://github.com/trigpoint-pub/agent-skills/releases/tag/price-watch-v0.1.0) · [Evidence](docs/price-watch/VALIDATION.md) | 0.1.0 | experimental prerelease | macOS arm64 CLI tests; host-native discovery untested |
| [prompt-architect](https://github.com/trigpoint-pub/agent-skills/releases/tag/prompt-architect-v0.3.0) · [Evidence](docs/prompt-architect/VALIDATION.md) | 0.3.0 | experimental prerelease | Claude Code on macOS (0.3.0 fresh-agent checks, skill path given); Codex on macOS (0.2.0 installed discovery); generated prompts not tested on target platforms |
| [concept-relations](https://github.com/trigpoint-pub/agent-skills/releases/tag/concept-relations-v0.1.0) · [Evidence](docs/concept-relations/VALIDATION.md) | 0.1.0 | experimental prerelease | Codex on macOS |
| [allocate-ai-work](https://github.com/trigpoint-pub/agent-skills/releases/tag/allocate-ai-work-v0.1.0) · [Evidence](docs/allocate-ai-work/VALIDATION.md) | 0.1.0 | experimental prerelease | Codex on macOS |
| [calibrate-ai-checks](https://github.com/trigpoint-pub/agent-skills/releases/tag/calibrate-ai-checks-v0.1.0) · [Evidence](docs/calibrate-ai-checks/VALIDATION.md) | 0.1.0 | experimental prerelease | Codex on macOS |
| [classify-ai-incident](https://github.com/trigpoint-pub/agent-skills/releases/tag/classify-ai-incident-v0.1.0) · [Evidence](docs/classify-ai-incident/VALIDATION.md) | 0.1.0 | experimental prerelease | Codex on macOS |

"Verified on" states the tested scope for each skill. Helper or CLI tests do not establish host-native installation or discovery. See each skill's validation record under `docs/`.

## Install

1. Choose the skill and open its release above. If it has a named skill ZIP, use that; GitHub's **Source code** archives contain the whole collection at that tag.
2. Extract it and copy only the complete `{skill-name}/` folder (or `skills/{skill-name}/` from a source archive). Keep its references, scripts, examples and `LICENSE`. Older source archives may keep MIT only at the repository root: copy that `LICENSE` into the skill folder before installing.
3. Follow the host locations in that skill's README. The destination must end in `{skill-name}/SKILL.md`, without a doubled folder. Preserve an existing installation and compare versions before replacing it.
4. Run the linked first-use example. Check the expected output and the validation limits before using personal or important data.

Only the skill folder is installed. Validation records, answer keys and method article snapshots stay in `docs/`; README links to them use GitHub URLs so they remain accessible from an installed copy with web access.

## Layout

| Folder | Contents | Installed? |
|---|---|---|
| `skills/{name}/` | The skill and its README | Yes, copy this folder |
| `docs/{name}/` | References, test records, answer keys, article snapshots | No |
| `tests/{name}/` | Repository tests for a skill, where it has them | No |

## Versions

Each skill has its own versions. Tags have the form `{skill}-v{version}`, for example `red-team-gate-v0.1.0`. Changes are listed in [CHANGELOG.md](CHANGELOG.md). [Contribution and release guidance](CONTRIBUTING.md) describes the package layout, tests and release evidence.

## License

| Files | License | Rights holder |
|---|---|---|
| All files except article snapshots | MIT, see [LICENSE](LICENSE) | Ansel |
| Article snapshots, `docs/*/method.md` | CC BY 4.0, see [LICENSE-CONTENT](LICENSE-CONTENT) | Ansel |

## Maintenance

Maintained by Ansel. Issues are open for bug reports and questions. There is no promised response time. To report a security problem privately, see [SECURITY.md](SECURITY.md).

## Earlier repositories

`inspect-github-agent-resources` and `price-watch` were first published as separate repositories, anselbuilds/inspect-github-agent-resources and anselbuilds/safari-price-watch. Both repositories are archived. Their existing history, tags and v0.1.0 releases remain there.
