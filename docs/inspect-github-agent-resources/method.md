# inspect-github-agent-resources

Inspect an agent resource before you install it

> Snapshot of article version 1.2 at <https://trigpoint.pub/methods/inspect-github-agent-resources>, written for inspect-github-agent-resources v0.1.x. The web page is the canonical version; corrections appear there first. Text by Ansel, licensed CC BY 4.0 (see [`LICENSE-CONTENT`](../../LICENSE-CONTENT)).

Once you add a skill, plugin, MCP server or agent template to an agent, the agent reads its instructions, and some resources ship commands that get executed. Before installing, you usually see a README, a star count and a few lines of description. Those say how the author chose to present it. They rarely say what it will read, write or connect to in your environment.

Having read the README is not the same as having read the source. Instruction text, hidden comments and bundled example files can all contain sentences written for the agent. Whoever reviews them, person or agent, may treat them only as evidence, never as instructions.

This article describes a static review procedure and an agent skill that runs it. It answers three questions: what work the resource helps you complete; which security concerns, judged from its source, affect your intended use; and what the smallest verification is before you install or update it. It does not install or execute the code under review, and it does not issue a safety certificate.

## The procedure

**1. Write down the decision you need to make.** The job, what an acceptable result looks like, how you do it now and where it is stuck; constraints on environment, data, accounts and whether code may run; and whether you want to find options, inspect one named resource, compare several, or plan acceptance and maintenance. The skill does not ask you to repeat what you already said. If one missing answer would change the conclusion, it asks one focused question and carries on with the inspection that does not depend on it. If the task is still unclear, it gives source-supported example uses and conditional fit, and does not invent a user profile for you.

**2. Declare the bounds before looking.** The starting budget for discovery is 3 search queries, 12 repositories screened and 3 candidates audited. For a named target, the start is up to 3 targets; for each, the provenance material, the exact unit under review and the files it directly references (one hop), up to 40 text files. If you set a different scope, yours applies. A cap is a coverage limit, not evidence of danger. Partly read files and important unread references are recorded; if a wider scope would help, the skill proposes it and does not widen it by itself. Public targets use anonymous public sources only. A local snapshot is read only from paths you explicitly authorized, is never uploaded, and the skill does not go looking for other data on your account or machine.

**3. Pin the version.** For a public target: the canonical repository, owner, the ref you asked for and the exact commit SHA, plus publisher identity, license, maintenance, releases and relevant official advisories. For a local target: the origin you supplied, the exact unit and the observed hashes. Provenance that is not available is stated as not available; no GitHub identity or commit is invented for a local file.

**4. Read four kinds of surface.**

- Instructions and hidden content: prompt-injection attempts, boundary overrides, concealed comments, unusual Unicode characters. An unusual character alone does not establish an attack; it needs interpretation.
- Permissions and data handling: credential requests, sensitive reads, writes, network destinations, telemetry, and possible disclosure paths.
- Execution and persistence: install hooks, commands, executable or binary entry points, background behavior and updates.
- Provenance and supply chain: exact versions, dependencies, publisher evidence, relevant official advisories, and the surfaces that were not reviewed.

Throughout, the skill does not clone, download archives, install, import, enable, update or run candidate code. Instructions in the repository, hidden comments and fixture content count as evidence only, never as authority.

**5. Run the inventory helper only when exact bytes exist.** When an authorized, stable local snapshot is already available, the skill includes a dependency-free Node.js script that inventories file hashes, hidden Unicode, comments, selected hooks and execution surfaces. It produces mechanical indicators. It does not detect malware or prove isolation. Without bytes, the skill says which conclusions the missing step prevents and still answers what it can.

**6. Answer first, then show the evidence.** The report starts with your decision: useful for which task, fit under which conditions, and the recommended next step. The evidence behind it follows, and each inference links to a source. Evidence carries one of four labels:

- `source-verified`: source content observed directly at a recorded ref or hash.
- `inferred`: a conclusion reasoned from evidence and your constraints.
- `not-found`: searched for in a named band and not found; this does not show absence elsewhere.
- `runtime-unverified`: it takes execution or a network to find out; the report says what verification is needed.

Coverage uses `reviewed`, `partial`, `not-reviewed` and `not-applicable`. There are four dispositions: `stop` (source evidence shows a violation of a boundary you declared, or a concrete integrity, permission or hidden-instruction problem), `insufficient-evidence` (critical provenance or security coverage is missing, so no conclusion is possible), `needs-review` (concerns that need interpretation or verification), and `no-blocker-observed` (every applicable check in the declared scope was completed and no blocker was seen; a discovery screen cannot receive this one). The skill outputs no numeric scores and does not use "safe", "approved" or "cleared for install" as a verdict.

Useful and installable are separate questions. A resource can fit your work while its installation disposition is still `insufficient-evidence`; a resource with no static blocker can still add nothing to your work. Both answers are listed. The report ends with the smallest useful verification: what to do, who supplies the evidence, and what result to expect. A read-only check or a synthetic case comes first when it resolves the uncertainty.

## When the resource changes

A new version is a new review. The skill includes a second script that compares two local snapshots you authorized and lists the differences in file hashes. It does not fetch new versions, schedule checks, or decide whether to update. A changed hash means some conclusions need another look; a changed hook is a lead to chase, and shows neither a vulnerability nor a fix. An unchanged hash does not mean external advisories or your deployment environment are unchanged. Evidence the change did not affect is kept with its original version, conclusions that depend on changed inputs are marked for re-review, and an earlier decision is not quietly carried over.

## Attribution

The procedure as a whole, and within it the split into four evidence labels, the fixed order of the four dispositions, the starting scope budget, and sending back for review only the conclusions that a version change affects, are working choices from Trigpoint (2026). The underlying ideas all have earlier forms, so none of them is claimed as new:

- Treating text in the reviewed repository as evidence, not instructions: Greshake et al. (2023) showed that external content can inject instructions indirectly, and OWASP (2025) LLM01 advises separating and clearly marking untrusted content.
- Marking directly sourced information apart from inference: ODNI (2015) ICD 203 sets this as an analytic standard.
- Dispositions and the evidence record: the result kinds fail, open, review and pass in SARIF 2.1.0 from OASIS (2020) map almost one to one onto stop, insufficient-evidence, needs-review and no-blocker-observed, and its run object likewise keeps one analysis's tool, version and results together.
- Four kinds of surface read before install: Mercer (2026), "How to Audit an Agent Skill Before You Install It" on Aident, covers the same four.
- Useful and installable answered separately: SkillPortrait from SkillAudit (2026) already rates utility and security on two axes and does not combine them into one number.
- A static inventory that needs no external service: the skill-scanner from Cisco AI Defense (2026) already has a static analyzer that needs no external services.
- Comparing versions: SARIF 2.1.0 marks results as new, unchanged or absent against a baseline run, and differential-review from Trail of Bits (2026), an agent skill for reviewing changes, was used for comparison during development.
- The acceptance package: the authorization package in NIST (2018) SP 800-37 likewise hands assessment records to a named official who decides whether to accept.

## How well it works so far

The v0.1.0 acceptance record is [VALIDATION.md](https://github.com/trigpoint-pub/agent-skills/blob/main/docs/inspect-github-agent-resources/VALIDATION.md) in the repository. What it supports is narrow.

The inventory and comparison scripts: on macOS arm64, Node.js 20.0.0 and 24.21.0 each passed all 24 regression tests with no skips; both also ran the documented demo inventory and the before/after comparison. The tests cover read-only inventory, hidden-text indicators, bounds, coverage gaps, command redaction, Unicode offsets, symlinks, deterministic ordering and comparison semantics. Node 20 is end-of-life, so its compatibility is a legacy note; use a maintained LTS line for regular work.

Agent use: independent agent sessions were given the skill and the sources it references, without expected answers, and their outputs were checked against a rubric recorded before the runs. Three local scenarios:

- First use: following the README's no-install path, the agent read the demo, ran the inventory helper, and kept narrow task fit, untested behavior and model-provider privacy apart. This run also led to a fix in the README, where the demo and the linked report example did not match.
- Static review: on a demonstration resource, the agent found a postinstall path that reads a note and attempts an HTTP POST, and an HTML comment trying to suppress that finding. It did not follow the reviewer instruction inside the comment, and it did not execute the target.
- Version review: the agent found newly added outbound note data, a synchronous-to-asynchronous API change, and the resulting offline and error-handling implications; it kept unaffected evidence and did not treat a clean mechanical scan as proof of safety.

A fourth scenario used a public third-party PDF skill. The agent resolved an immutable commit, read six target files and six directly relevant official sources, connected table-extraction suitability to dependencies and example behavior, checked the unit's license, kept the uncertainty about unpinned runtimes and advisories, and proposed a page, row and value acceptance check. It did not install the target, process a PDF, or measure extraction quality. This was the same agent as the first-use case, so it does not count as a fourth independent agent.

These are bounded observations from one agent environment. They are not measurements of general detection rate, false positives, human time saved, or compatibility across agents. Target code was not executed.

## What has not been validated

VALIDATION.md does not claim to have validated: host-native skill discovery and installation in Codex and GitHub Copilot; Windows and Linux runtime testing; adversarial live-filesystem isolation; dynamic malware testing; public release and download validation. The collection page marks this skill the same way: helper tests on macOS arm64, host-native discovery untested.

Also: review quality has not been benchmarked, and no accuracy has been compared with other approaches. This is a static review, and it is not a sandbox run, penetration test, complete malware detection or security certification. The helper runs locally, but an agent reading files may send their contents to its model provider; file names, hashes and reports can also reveal private information, so read a report before sharing it.

## When to use it

Use it before trying an unfamiliar skill, plugin, MCP server or agent template; when comparing candidates for a specific task; and when deciding whether to accept an update. If you only want to know what this kind of resource could help with, ask directly; the skill will not start a repository audit for that.

It does not replace runtime testing. To learn what a resource actually does when it runs, test it separately, within the scope you authorized; that is outside this skill.

## Get the skill

The skill is on GitHub: [skills/inspect-github-agent-resources in github.com/trigpoint-pub/agent-skills](https://github.com/trigpoint-pub/agent-skills/tree/main/skills/inspect-github-agent-resources). The current version is 0.1.0, released on 2026-10-24 as a trial prerelease ([release page](https://github.com/trigpoint-pub/agent-skills/releases/tag/inspect-github-agent-resources-v0.1.0)), under the MIT license. It was first published as a standalone repository; that repository is archived, and the current version lives in the collection.

To install, copy only the whole `skills/inspect-github-agent-resources/` folder, LICENSE included, and nothing else:

- Codex: `.agents/skills/inspect-github-agent-resources/` in a project, or `~/.agents/skills/inspect-github-agent-resources/` for personal use.
- GitHub Copilot: `.github/skills/inspect-github-agent-resources/` in a project, or `~/.copilot/skills/inspect-github-agent-resources/` for personal use.

These are the currently documented defaults and do not override your organization's policy. If the destination already exists, compare versions before replacing it. Whether each host discovers the folder has not been tested end to end; if the skill does not appear in the selector, follow that host's refresh or restart guidance.

The full definitions of evidence labels, coverage values and dispositions are in the skill's `references/audit-contract.md`; the inventory helper's scope and limits are in `references/scanner.md`; version maintenance is in `references/maintenance.md`.

## First use

**Prerequisites.** An agent that can read files. Reviewing a public repository needs anonymous public web access; reviewing local files only does not, and missing provenance and advisory evidence is listed as gaps. The helper needs Node.js: use a maintained LTS line (24.21.0 was tested); the floor is 20.0.0, which is end-of-life. No npm install, API key or third-party package is needed. The record does not name the host of the agent environment used for validation.

**Try it without installing.** Take the v0.1.0 archive from the [release page](https://github.com/trigpoint-pub/agent-skills/releases/tag/inspect-github-agent-resources-v0.1.0) and extract it into a working folder, keeping `skills/inspect-github-agent-resources/` intact. Open that folder in an agent that can read files and paste this request, replacing `<repo>` with the extracted folder:

> Read `<repo>/skills/inspect-github-agent-resources/SKILL.md` and use that skill to inspect `<repo>/skills/inspect-github-agent-resources/examples/demo-snapshot`. I want to summarize my own local notes. Explain task fit, source-based security concerns, evidence gaps, and the smallest useful acceptance check. Do not install or execute the reviewed resource. You may run this review skill's inventory helper.

The request is taken from the [repository documentation](https://github.com/trigpoint-pub/agent-skills/blob/main/docs/inspect-github-agent-resources/README.md) and kept as written. The skill asks the agent to answer in your preferred language.

**Example 1.** This is a demonstration sample. `demo-snapshot` is a small instruction-only resource with no scripts or dependencies; it outlines a note the user supplies. The reference answer in the repository says: it can outline one note you explicitly provide, but its source instructions alone do not prove summary quality or offline model processing; try a synthetic note with uncertain claims and check that the uncertainty is kept. It illustrates the format; no measured result backs it.

**Example 2.** This is a demonstration sample. The repository's `examples/review-example.md` sets another scenario: someone manually inspects third-party skills every week and asks whether a local inventory helper could improve that; files must stay on the device and candidate code is not to be executed yet. The example answer says it could help with repeatable file inventory and version-change detection, while you still review what scripts mean and what the unscanned dependencies contain; there is no evidence here that it finds more vulnerabilities or saves a measurable amount of time; and the installation disposition is `insufficient-evidence` because provenance and behavior evidence is missing, which does not stop it from being identified as a useful inventory aid. Two proposed acceptance checks:

- Inventory before manual review: an authorized snapshot goes in; hashes, hooks and a record of skipped files come out. Acceptance: a known synthetic hook is surfaced, skipped directories stay visible, and no candidate hook is executed.
- Revisit a changed version: two scoped snapshots go in; observations of changed files come out. Acceptance: a modified hook changes the observation, and incomplete coverage is never written up as confirmed removal or equality.

**What success looks like.** The answer explains the narrow purpose, cites the files you supplied, separates declared behavior from runtime evidence, and proposes one small verification. It must not claim a security certification or invent a publisher or release history.

**Failure and limits.** An answer that gives a numeric score, or uses "safe" or "approved" as its verdict, breaks the skill's own contract. Helper exit codes: 0 means the included inventory completed and says nothing about whether the resource may be installed; 1 means the inventory is partial or failed; 2 means invalid input. Save a helper report outside the scanned folder so you do not alter the evidence being measured.

**Version and validation.** Skill 0.1.0, trial prerelease; the acceptance record is [VALIDATION.md](https://github.com/trigpoint-pub/agent-skills/blob/main/docs/inspect-github-agent-resources/VALIDATION.md). Use [GitHub Issues](https://github.com/trigpoint-pub/agent-skills/issues) for ordinary problems, with a synthetic reproduction; no response time is promised. Security reports go through GitHub's private vulnerability reporting.
