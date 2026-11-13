# Validation

What has been tested, what has not, and the checks used.

**Status:** 0.3.0 experimental prerelease, 2026-11-07. In its acceptance run (section 2c), eight of nine requests passed every applicable check; the failure is explained there. This is not a quality benchmark or a guarantee of downstream results. Earlier releases: 0.2.0, 2026-11-01; 0.1.0, 2026-10-26.

## 1. Private predecessor, October 2026

The private version of this method was checked on five requests: four task types (review, summarize, generate, classify) and three vendors (Claude, OpenAI, Gemini). Each request went to a fresh sub-agent that read only the method, with no web access. All five results passed checks 1 to 5 below.

This does not carry over to this skill. The private version carried a hand-maintained table of vendor conventions; this skill replaces that table with reading the vendors' pages at run time (Step 5), which is the part most likely to fail and was not exercised. The runs were also all on one vendor's models (Claude), and the results were scored by the method's author, not blind.

## 2. Acceptance run of the first release candidate, October 2026

**Setup**

- Host: one desktop agent (Codex) on macOS, arm64. The skill folder was copied to the agent's personal skill folder (`~/.codex/skills/prompt-architect/`) and appeared in each new sub-agent's skill list.
- Requests R1 to R6 (§3). Each went to a fresh sub-agent with no earlier conversation, answers, or checks, given only "Use prompt-architect to handle this request:" and the request. Sub-agents could read public web pages. All six ran on one model at one effort setting; no other vendor's model was used, and no generated prompt was run on its target platform.
- The sub-agents also inherited the host's own instructions, which affected R5 (below).
- The coordinating agent scored the results against §4. This was one run per request, not blind.

**Results**

| Request | Result | Note |
|---|---|---|
| R1 (review, Claude) | fail | Check 6: the reason given for the assumed model cited a page that does not contain it; the page that does was read but not cited |
| R2 (summarize, Codex) | pass | |
| R3 (generate, Gemini) | pass | |
| R4 (classify, ChatGPT) | pass | The answer said the exact model could not be verified instead of naming one; the request note asked for a named default, which the pages read could not settle (see §3) |
| R5 (no platform) | fail | Check 8: it asked one question but added an explanation, partly required by the host's own rule for announcing a skill |
| R6 (no vendor guide) | pass | |

- All 26 links in the source list opened on the day. Four redirected. Two refused a plain HTTP client (403 and 308) but were read with another tool.
- Time per request: 13 to 90 seconds. Token counts were not available.

**Revisions after this run**: Step 5 now separates products from APIs and requires a cited reason for the assumed model or "model unknown"; the usage notes now cover the assumed model and the conventions used, each with a page; the Input section states that a missing-platform question is the whole answer; the Limits note how to tell a refused fetch from a missing page.

**Re-run after the revisions** (same host and procedure, one fresh sub-agent per request, same day): R1, R4 and R5 only.

| Request | Result | Note |
|---|---|---|
| R1 | pass | The assumed model now cites the vendor's models overview, which supports it |
| R4 | pass | States "model unknown" and uses only guidance that does not depend on the model |
| R5 | pass | The skill's answer was one question; the host's own notice that it was using a skill was recorded separately (check 8) |

At this stage, R2, R3 and R6 had not been re-run on this host and the link check had not been repeated. The later Codex follow-up below closes those gaps. No refused or missing page occurred in this earlier run.

**Run on a second host after the revisions** (October 2026)

- Host: Claude Code desktop app on macOS. The skill was not installed: each sub-agent was given the path to the skill folder, told to read `SKILL.md` and follow it, and told not to read any other file in the repository. Installation and discovery were therefore not exercised.
- Requests R2, R3 and R6 (§3), one fresh sub-agent each, given only the skill path and the request. All ran on one model (Claude Opus 5.5) at one effort setting. Sub-agents could read public web pages; the host's own rules blocked a plain HTTP client, so page status comes from the reading tool only.
- Missing-page check: a copy of the skill with one Anthropic link in the source list changed to an address that does not exist, run with request R1. This is a constructed case. It exercises the "page is gone" branch of the Limits text, not the "fetch refused" branch.
- The coordinating agent scored the results against §4. One run per request, not blind.

| Request | Result | Note |
|---|---|---|
| R2 (summarize, Codex) | pass | Named the assumed model and cited the Codex models page. The source list has no Codex pages; the sub-agent found them under `developers.openai.com/codex/`, which redirects to `learn.chatgpt.com` |
| R3 (generate, Gemini) | pass | Stated "model unknown" because no page read names the Gemini app's default; a source-list page marked deprecated was read and not used |
| R6 (no vendor guide) | pass | Opened no vendor pages; generic structure, answers must cite the user's documents, usage notes say no platform guidance was checked |
| R1 with an edited link | pass | The edited link returned 404. The answer named it, used the vendor's current prompting page instead, and said so in the usage notes |

- 17 of the 26 source-list links were opened by these runs and all 17 opened. One of them, the Gemini 3 developer guide, is marked deprecated on the page. The other 9 were not opened, so check 9 was not run.
- Time per request: 83 to 344 seconds. Sub-agent token totals as reported by the host: about 101,000 to 188,000.

**Codex follow-up, 2026-10-24**

- Host: Codex desktop on macOS 27.0.1, arm64. Three installed files matched the revised candidate byte-for-byte at `~/.codex/skills/prompt-architect/`.
- Four fresh sub-agents had no earlier conversation, answer keys or other runs' outputs. Each saw the skill in its initial list and read its installed instructions and source list. They still inherited host instructions. All used GPT-6 Astra at high effort; the coordinator scored the outputs, not blind.
- R2, R3 and R6 passed every applicable check. R6 had no vendor guidance, so vendor-specific checks were not applicable; its tool record showed no web call.
- A fourth run used a naturally refused page: the OpenAI model-release-notes URL returned HTTP 403 to the first plain HTTP fetch, then the agent read the same page with a web reader. It distinguished a refused fetch from a missing page, changed tools and recorded the URL it read. This was not a fabricated error or an edited link. The first tool was specified (a plain curl request), so this does not show that an agent choosing its own first tool would meet the same refusal.
- All 28 source-list URLs were checked: 27 returned HTTP 200 after redirects; one returned 403 to the HTTP client and was readable with the other tool. The full-list check was performed by the coordinator; it does not mean every sub-agent read all 28 pages.
- One non-blocking wording observation remains: an API model's documented effort default is not evidence of the setting currently selected in the Codex interface. Any example using that output must identify the API scope or keep the product setting unspecified.

**Release packaging, 2026-10-26**

All 28 source-list URLs were rechecked for this release: 27 returned HTTP 200 with matching page content; the OpenAI model-release-notes page returned HTTP 403 to the plain HTTP client and was readable with a web reader. This verifies reachability, not every claim on those pages.

The instruction body is unchanged from the revised candidate used in the follow-up. Changes finish release metadata, reconcile this record, add a bilingual first-use tutorial and a skill-folder MIT license, and make documentation links work from an installed copy. A strict YAML check also found an unquoted colon in the description; the scalar is now quoted, with the decoded description and instruction body unchanged. No new agent-behavior run is claimed for these packaging changes. The tutorial's fixture and expected results are synthetic teaching material, not a measured target-platform result.

## 2b. Acceptance run of 0.2.0 (per-vendor source files)

Host: Codex desktop 0.166.0-alpha.5.1 on macOS arm64, with the skill installed at `~/.codex/skills/prompt-architect/` and the installed files byte-identical to the candidate. Each request ran once in a fresh sub-agent with no thread history, given only "Use prompt-architect to handle this request:" and the request. The coordinating agent scored the results; this was not a blind evaluation, and no generated prompt was run on its target platform.

**First run, 2026-11-01 (gpt-6-astra, medium effort).** R1 to R6 against checks 1 to 10: all passed. Each run with a platform opened only `official-sources.md` and the target vendor's file; R5 and R6 opened no vendor file. R1 to R4 name only a product, and all four answered "model unknown", so no run read a model's own pages and check 7 had nothing to check.

**Second run, 2026-11-01 (gpt-6-astra, high effort),** to cover that gap:

- N1 to N3 name the model. Each run opened that model's own pages, and none of the three prompts or usage notes contained an instruction or setting that those pages say to remove or avoid. Where a model page listed no such item, the result was recorded as "none on the page", not as a pass. All three passed checks 1 to 10.
- R1 and R4 again, at high effort: both still answered "model unknown" and cited the same pages as the medium-effort run. In 0.1.0, R1 had assumed a model. See section 5.

Check 9, both runs: 27 links opened over plain HTTP; the OpenAI model-release-notes page refused the plain HTTP client and was read with a web reader.

## 2c. Acceptance run of 0.3.0 (Step 2 breaks the task down)

0.3.0 changes Step 2 from "Write the reasoning steps" to "Break down the task": the prompt states the task's sub-tasks, the decisions they call for and what each decision rests on. Whether to ask for step-by-step reasoning or a closing self-check moves to Step 5, where it is answered from the vendor's pages. Check 1 changed with it (section 4). Sections 1, 2 and 2b used the earlier check 1, "The prompt contains real reasoning steps for the task type, not just a heading." Their results describe 0.1.0 and 0.2.0, not this version.

**Run, 2026-11-07**

- Host: Claude Code desktop app on macOS. The skill was not installed: each sub-agent was given the path to a copy of the candidate skill folder, told to read `SKILL.md` and follow it, and told not to read any other local file. Its `SKILL.md` and `references/` files match this release byte for byte; only the README's version, release-link and tested-on lines were changed afterwards, and no run opened the README. Installation and discovery were not exercised; they were last tested on Codex for 0.2.0, and the folder's layout has not changed.
- Requests R1 to R6 and N1 to N3 (section 3), one fresh sub-agent each, given only "Use prompt-architect to handle this request:", the request and the skill path. All ran on one model (Claude Opus 5.5) at one effort setting. Sub-agents could read public web pages. They also inherited the host's own instructions and stored notes, which affected R2 (below).
- The coordinating agent scored the results against section 4. For each run it checked the cited pages for the model choice, for the decision on step-by-step reasoning or a closing self-check, and for a sample of the other points. Files read (check 10) come from each run's tool record. One run per request, not blind; no generated prompt was run on its target platform.

| Request | Result | Note |
|---|---|---|
| R1 (review, Claude) | pass | Assumed Claude Opus 5.5, citing the models overview, which says to start with that model when unsure. No "think carefully" line, which the Opus 5.5 prompting page suggests removing from chat system prompts |
| R2 (summarize, Codex) | fail | Check 6: one usage note, about typing `@` with an input method, cited the Codex prompting page, which does not say it. The note came from the host's stored notes, not from the skill or a vendor page. The rest of the answer passed, including a closing check that the same page recommends |
| R3 (generate, Gemini) | pass | Model unknown for the Gemini app. No step-by-step or self-check instruction, citing Google's prompting page |
| R4 (classify, ChatGPT) | pass | Assumed the GPT-6 family in ChatGPT, exact version unknown, citing the model release notes, and used only guidance that applies to the whole family |
| R5 (no platform) | pass | One clarifying question, nothing else |
| R6 (no vendor guide) | pass | Opened no vendor file; generic structure, answers cite the user's documents, usage notes say no platform guidance was checked |
| N1 (Claude Opus 5.5) | pass | No "think carefully" line and no request to write out reasoning, which the model's page says may be declined. Uses that page's note for pasted text |
| N2 (GPT-6.1 Sol in Codex) | pass | Closing check traced to the Codex prompting page; no step-by-step instruction, citing the reasoning guide |
| N3 (Gemini 3.8 Flash) | pass | No step-by-step instruction, citing Google's prompting page. Sampling settings left unset, as the model's release notes say |

- Three cited points were worded more broadly than their pages (in R4, N2 and N3: a model's effort options, when to pause for approval, and avoiding persuasive language). Each still traced to the page and was counted under check 6.
- In 0.2.0, R1 and R4 answered "model unknown". In this run both named an assumed model with a cited reason, which Step 5 allows. Which of the two a product-only request gets can differ between runs and hosts.
- Check 10: every run with a platform opened only `official-sources.md` and the target vendor's file; R5 and R6 opened no vendor file.
- Check 9: 27 of the 28 links opened. Four Google links now redirect from `ai.google.dev` to `aistudio.google.com`; the source list still uses the old addresses. The OpenAI model-release-notes page refused the reading tool (HTTP 403) and was read in a browser.
- Time per request: 12 to 312 seconds. Sub-agent token totals as reported by the host: about 77,000 to 152,000 per request, about 1.04 million for the nine.

## 3. Practice requests

| ID | Request | What it exercises |
|---|---|---|
| R1 | Write a prompt for a contract review assistant that flags risky clauses, to run in Claude. | Review task; Anthropic pages |
| R2 | Write a prompt for a role that summarizes the key points of a book, to run in Codex. | Summarize task; OpenAI pages; coding-agent register |
| R3 | Write a prompt for a short-story writing assistant, to run in Gemini. | Generate task; Google pages; preview or legacy status if the pages say so |
| R4 | Write a prompt that classifies customer support tickets and routes them to one of five teams, to run in ChatGPT. | Classify task; product name without a model, so the answer states the model it assumed with a supporting page, or says the model is unknown |
| R5 | Write a prompt that turns meeting transcripts into action lists. | No platform given: one clarifying question, nothing else |
| R6 | Write a prompt for answering questions from uploaded policy documents, to run in a document chat tool with no published prompting guide. | No official guidance: generic structure, citations to the user's documents, stated as not checked against vendor guidance |
| N1 | Write a prompt for a contract review assistant that flags risky clauses, to run in Claude Opus 5.5. | Named model: the model's own Anthropic pages and their remove-or-avoid items |
| N2 | Write a prompt for a role that summarizes the key points of a book, to run in Codex with GPT-6.1 Sol. | Named model: the model's OpenAI pages, on a guide page that also covers other models |
| N3 | Write a prompt for a short-story writing assistant, to run in Gemini 3.8 Flash. | Named model: the model's Google pages, when a newer model is the latest |

## 4. Checks

A result passes only if every applicable check holds.

1. The prompt contains a real breakdown of the task for the task type (its sub-tasks and the decisions they call for), not just a heading. Any instruction to reason step by step or to self-check counts as platform-specific under check 6.
2. The prompt contains success criteria someone could check.
3. The prompt defines output fields and their order.
4. No emoji or decorative symbols are used as structure, unless the purpose is casual.
5. The prompt is self-contained: no source numbers, no references to the skill, no features the platform lacks.
6. Every platform-specific setting or convention in the prompt or the usage notes is traceable to a vendor page that was read in this run, cited with URL and date. Nothing vendor-specific appears without a cited page.
7. Where a page read in this run says to remove or avoid an instruction for this model, the prompt does not contain it. If the model's own pages list no such item, record "none on the page"; that is not a pass.
8. When the platform is missing, the skill's answer is one clarifying question and nothing else. A notice that the host itself requires when a skill is used is recorded separately; it is not counted as part of the answer, but anything beyond that notice is.
9. Every link in the vendor files under `skills/prompt-architect/references/` (`openai.md`, `anthropic.md`, `google.md`) opens (after redirects) on the day of the run; failures are listed.
10. For a request with a platform, the run opens only the target vendor's file under `references/` (besides `official-sources.md`); for R5 and R6, no vendor file. Shown by the run's record of files read.

## 5. Not yet tested

- Host-native rendering of documentation links across all agents. This release uses fixed-version GitHub links from the installed README instead of assuming the repository docs were copied with the skill.
- Installation and discovery on hosts other than Codex on macOS (Claude Code was run with the skill path given, not installed), and Gemini as a host. For 0.3.0, installation was not tested on any host.
- Generated prompts run on their target platforms, and the quality of their results on real contracts, books, tickets, or documents.
- Working without web access, and a broken link with no reachable replacement.
- A refused fetch when the agent chooses its own first tool. The refused case was run once, with the first tool specified; the missing page was run once, with an edited link.
- Vendor pages that contradict each other, or page content written to mislead the agent.
- Repeated runs of the same request.
- Model-specific guidance when only a product is named. In the 0.2.0 runs the skill then answered "model unknown" (R1 and R4, at medium and high effort) and used only guidance that does not depend on the model. Name the model to get model-specific guidance. In the 0.3.0 run, R1 and R4 named an assumed model with a cited reason instead.
- Guide pages that cover several models at once, such as OpenAI's latest-model guide: whether an agent always keeps to the sections for the named model.
