# Sources

What the skill shares with earlier work, what Trigpoint chose, and how the references were checked.

## Earlier work

Apart from the Trail of Bits comparison described in the [skill README](../../skills/inspect-github-agent-resources/README.md#sources-and-attribution), the repository records no use of these works while the skill was written. A prior-art check in November 2026 lists them as earlier forms of the same ideas, not as sources the skill was built from.

| Part of the skill | Earlier form | Reference |
|---|---|---|
| Treating text in the reviewed repository as evidence, not instructions | External content can inject instructions into an LLM-integrated application indirectly | Greshake, K., Abdelnabi, S., Mishra, S., Endres, C., Holz, T., & Fritz, M. (2023). Not what you've signed up for: Compromising real-world LLM-integrated applications with indirect prompt injection. In *Proceedings of the 16th ACM Workshop on Artificial Intelligence and Security* (pp. 79–90). ACM. https://doi.org/10.1145/3605764.3623985 (preprint: arXiv:2302.12173) |
| Same | Separate and clearly mark untrusted external content (prevention and mitigation strategy 6) | OWASP Gen AI Security Project. (2025). LLM01:2025 Prompt Injection. In *OWASP Top 10 for LLM Applications 2025*. https://genai.owasp.org/llmrisk/llm01-prompt-injection/ |
| Marking directly sourced information apart from inference | Distinguishing underlying intelligence information from analysts' assumptions and judgments, set as an analytic standard | Office of the Director of National Intelligence. (2015). *Intelligence Community Directive 203: Analytic Standards* (effective 2 January 2015). https://www.dni.gov/files/documents/ICD/ICD-203.pdf |
| The four dispositions and the evidence record | The result kinds fail, open, review and pass (§3.27.9); the run object keeps one analysis's tool, version and results together | OASIS. (2020). *Static Analysis Results Interchange Format (SARIF) Version 2.1.0* (M. C. Fanning & L. J. Golding, Eds.). OASIS Standard, 27 March 2020. https://docs.oasis-open.org/sarif/sarif/v2.1.0/os/sarif-v2.1.0-os.html |
| Four kinds of surface read before install | A pre-install audit guide that covers the same four kinds of surface | Mercer, T. (2026, July 24). How to audit an agent skill before you install it. *Aident AI Blog*. https://aident.ai/blog/audit-agent-skill-before-installing |
| Useful and installable answered separately | SkillPortrait rates utility and safety on two axes and does not combine them into one score | SkillAudit. (2026). *skillaudit: SkillPortrait, skill-centered utility and safety evaluation for agent skill packages* [Software repository]. https://github.com/SkillAudit/skillaudit/tree/349eff1e12cf6f210aa9b865a9e865b948b5a89b |
| A static inventory that needs no external service | A static analyzer that needs no external services | Cisco AI Defense. (2026). *skill-scanner: Security Scanner for Agent Skills*, static analyzer documentation [Software repository]. https://github.com/cisco-ai-defense/skill-scanner/blob/431cb58a5ac333bc0bb9aaa23f7c30ac628f59f8/docs/architecture/analyzers/static-analyzer.md |
| Comparing versions | Results marked new, unchanged or absent against a baseline run (§3.27.24) | OASIS (2020), above. |
| Same | An agent skill for reviewing changes, used for comparison during development | Trail of Bits. (2026). *differential-review* [Agent skill; CC BY-SA 4.0]. https://github.com/trailofbits/skills/tree/442fc9d6c89b1e937e6f7a477e7071ea75fcbea4/plugins/differential-review/skills/differential-review |
| The acceptance package | The authorization package hands assessment records to a named official who decides whether to accept | Joint Task Force. (2018). *Risk Management Framework for Information Systems and Organizations: A System Life Cycle Approach for Security and Privacy* (NIST Special Publication 800-37, Revision 2). National Institute of Standards and Technology. https://doi.org/10.6028/NIST.SP.800-37r2 |

## What Trigpoint chose

These are working choices from Trigpoint (2026), which wrote the skill. Each underlying idea has an earlier form in the table above, so none is claimed as new:

- **The procedure as a whole**: task fit, source-based security review and version acceptance in one inspection.
- **The four evidence labels** (`source-verified`, `inferred`, `not-found`, `runtime-unverified`) and how claims are split among them.
- **The fixed order of the four dispositions** (`stop`, `insufficient-evidence`, `needs-review`, `no-blocker-observed`).
- **The starting scope budget** for discovery and for each candidate.
- **Sending back for review only the conclusions that a version change affects.**

## How the references were checked

The prior-art check ran in November 2026, after the 0.1.0 release, and compared the skill as published with earlier work. No work was read in full: each point in the table was checked only as far as it needs, through a summarising web reader, so the points are paraphrases. None was checked word for word, and nothing is quoted. The ODNI file for ICD 203 could not be read as text, so that row rests on descriptions of the directive rather than its text. Bibliographic details were confirmed against the DOI records (Greshake et al. 2023; NIST SP 800-37 Rev. 2), the front matter and sections 3.27.9 and 3.27.24 of the OASIS standard (SARIF 2.1.0), and the publishers' pages or repositories for the others, at the revisions linked.

## Third-party material

No text, code, figures or data from these works are reproduced in the skill or in this file.
