# Contributing and releasing

Use Issues for questions and reproducible problems. Include the skill name, release tag or commit, host, synthetic input, expected result and observed result. For sensitive problems, use [private vulnerability reporting](https://github.com/trigpoint-pub/agent-skills/security/advisories/new). Ansel maintains this collection; no response time is promised.

## Where each file belongs

- `skills/{name}/`: the independently installable unit, including `SKILL.md`, README, MIT `LICENSE` and any required references, scripts and examples.
- `docs/{name}/`: first-use guides, validation evidence, answer keys, source notes and dated method article snapshots. The website remains canonical for articles.
- `tests/{name}/`: repository-level tests. Existing Inspect helper tests stay beside its scripts.
- `.github/`: active repository workflows and Issue forms. The copies beneath `docs/*/.github/` are retained migration records; the shared root form replaces those per-repo templates for current reports.

Keep runnable code and skill identifiers stable during documentation cleanup. In an installable README, use relative links within that skill and public GitHub URLs for repository-only files. Release documentation should link to its tag or recorded commit; `main` links mean current guidance, not frozen release evidence.

## Existing helper tests

From the repository root:

```sh
python3 -m unittest discover -s tests/price-watch -v
node --test skills/inspect-github-agent-resources/scripts/tests/static-agent-resource-scan.test.mjs skills/inspect-github-agent-resources/scripts/tests/compare-snapshots.test.mjs
```

The GitHub Actions workflow runs these helpers on macOS and Ubuntu, using Python 3.9 and Node 24. These tests use synthetic fixtures. They do not establish skill discovery, model output quality or Safari notification delivery. Instruction-only skills retain their own explicit validation records rather than claiming coverage from these helper tests.

## Next release of a skill

Each skill versions independently as `{skill}-v{version}`. Keep the published version, prerelease status and tested scope consistent across the skill README, collection table, changelog and release notes. Record documentation/packaging changes on `main` as unreleased until included in a new version; preserve old tags and published assets. In the same change, update the release tag in the install prompt at the top of the skill README's Install section, and drop its LICENSE clause once the tagged skill folder contains `LICENSE`.

Build the next skill ZIP from a recorded commit. It should extract to one `{skill-name}/` folder containing its MIT license and runtime references. Exclude repository-only answer keys, `docs/`, personal data and runtime databases. Attach `{skill}-v{version}.zip` and `SHA256SUMS.txt`; the automatically generated source archives contain the whole collection.

Before publishing, inspect the archive contents, check its checksum, follow the README from a fresh extracted copy, check links and run the relevant tests. Record what was actually tested in `docs/{name}/VALIDATION.md`; do not turn a documentation check into a claim of agent or platform effectiveness. The release notes should link to installation, the shortest example and the version-specific validation record.

Historical releases without standalone ZIPs remain usable via their source archive. For an older archive whose skill folder lacks `LICENSE`, copy the root MIT license into that folder. Do not silently replace a published archive to make it match newer instructions.
