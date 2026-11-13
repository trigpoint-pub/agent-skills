# prompt-architect

Architect a prompt before you write it

> Snapshot of article version 1.4 at <https://trigpoint.pub/methods/prompt-architect>, written for prompt-architect v0.3.x. The web page is the canonical version; corrections appear there first. Text by Ansel, licensed CC BY 4.0 (see [`LICENSE-CONTENT`](../../LICENSE-CONTENT)).

Hand-written prompts tend to fail in one of two places. The first is a prompt that names a role and a task but never says how the task should be done: which judgments to make along the way, what counts as done well, which fields the answer should have. The model fills those gaps itself, and fills them differently each time.

The second is a prompt written in conventions meant for an older model. Vendors revise their prompting guides as models change, and the pages themselves move. In one of our test runs we met two cases: a Gemini guide page that marked itself deprecated, and Codex documentation that now redirects to a new domain. A remembered rule such as “this vendor wants this format” may already be out of date.

This article describes a procedure that handles the two problems separately: settle the task method first, then write it in the target platform's current official conventions. It also covers the agent skill that runs the procedure.

## The procedure

The procedure has two layers. Steps 1 to 4 do not depend on the platform, and their components follow the vendors' own guidance; arranging them in this order, kept apart from platform conventions, is Trigpoint's (2026). It is a working method, not a research result, and has not been compared against other prompting methods. Step 5 is looked up again on every run.

**1. Classify the task.** Common types: summarize or extract, generate or write, review or evaluate, classify or route, converse or support, transform or translate. The type shapes the next three steps. If the purpose mixes types, name the main one and note the second.

**2. Break down the task.** Write down what the task consists of, specific to the task type: its sub-tasks, the decisions it calls for along the way, and what each decision rests on. For a review: which dimensions to evaluate; for each, what counts as evidence and what would count against it; and which judgment the answer must reach, such as a risk rating for each clause. For a summary: what has to be found (the core thesis, how the parts relate) and what has to be selected, by which rule (the points with the most value or the most direct use). Where order matters, for instance when a judgment must rest on the evidence, say so. This step describes the task only; it does not script how the model should think. Whether the prompt should also ask for step-by-step reasoning or a closing self-check depends on whether the target model reasons on its own. That is a platform question, left to step 5 and the vendor's pages.

**3. Set success criteria someone could check.** Write criteria that another person could verify item by item, not adjectives. For a summary: every point states its supporting argument and where it applies; numbers and formulas are kept exactly; no core claim is left out. Words like “high quality”, “clear” or “engaging” stay out unless you say what would show them.

**4. Fix the output fields.** Decide which fields the answer has, in what order, and what goes in each. For a summary: the principle, then two or three supporting details, then how to apply it, then the key takeaways.

**5. Read the platform's current official guidance.** Start from the vendor's general prompting guide and its latest-model or model-overview page, and follow them to the page for the specific model when one exists. Look for: how the vendor recommends structuring a prompt, reasoning or effort settings (including whether the prompt should ask for step-by-step reasoning or a self-check), instructions the vendor says to remove or avoid for this model, output formatting conventions, and whether the model is marked preview, beta or legacy. Record the URL and the date read for each point. What the pages do not say stays out of the prompt; remembered tips do not fill the gap.

When only a product is named, there is one more step. A chat product is not the same as an API: the model behind a product can depend on the plan, the client and the user's settings. State which model you are assuming and cite a page that supports the choice. If no page you read settles it, write “model unknown” and use only guidance that does not depend on the model.

**6. Write one ready-to-paste prompt.** The method decides the substance; the platform decides the form. Use one vendor's conventions only. Write out the actual breakdown, criteria and fields, not just the headings “Role / Task / Constraints / Output”. State limits as measured targets where you can, such as “at most 200 words”. The prompt must work when pasted alone, with no source numbers and no mention of this method. Unless the purpose is casual or social, do not use emoji or decorative symbols as section markers.

The result comes in three parts: a one-line summary of the purpose, the platform and model, and the task type; the prompt itself, which is the only part you paste; and usage notes listing the model assumed and why, the vendor conventions used, and any settings to change outside the prompt, each with its source URL and the date read, plus anything the pages did not cover.

## Why there is no table of vendor rules

Vendors' prompting conventions change with every model release. A table of conventions compiled in advance can be out of date by the next release, and the vendors' own pages are the authority and are already public. So the skill does not carry such a table.

The skill carries only a list of where each vendor publishes its prompting guidance, and the agent reads the original pages each time. The list ages too. When a link fails, the skill asks the agent to tell a page that is gone from a fetching tool that was refused; if the page is gone, the agent looks for the vendor's current equivalent and says so in the usage notes.

If the agent cannot open web pages, the skill says so and asks you to paste the relevant guide text; or you can have it write from steps 1 to 4 alone, in a generic structure (role, context, task, constraints, output format), with a usage note that no platform guidance was checked. For a platform with no official prompting guide, such as a tool built on another company's model: if you know the underlying model, the agent uses that vendor's guidance; if not, the generic structure. For a tool that answers from documents you upload, the prompt requires answers to cite those documents and to say when the documents do not cover a question.

## The notebook and the skill

This site also has a public NotebookLM notebook, Platform-Aware Prompt Architect, listed on the [Notebooks page](https://trigpoint.pub/notebooks). You state a purpose and a target platform, and it returns a prompt you can paste in. The notebook and the skill come from the same method, but they are different things:

- The notebook runs inside NotebookLM, with nothing to install. It answers from the vendors' official documents imported into the notebook, and those sources are updated when the notebook gets a new version. The notebook has its own version number, unrelated to the skill's.
- The skill runs in your own agent. It carries no pre-summarized vendor rules; on every run it reads the vendors' current official pages and cites each one, with URL and date read, in the usage notes.

To try the method first, the notebook is the easier start. To use it repeatedly in your own agent workflow, with every platform recommendation traceable to a page read that day, use the skill.

This method appeared earlier in Chinese on Substack, in two articles: the first in March 2026 and a version 2.0 in June. The notebook and the skill on this site now replace the setup prompts and the notebook those articles offered, which are no longer provided separately.

## How well it works so far

The skill's first public release candidate (0.1.0) was tested on six practice requests: four task types and three vendors, plus one request with no platform and one for a tool with no official guide. The checks: the prompt contains real reasoning steps, checkable criteria and output fields; it works when pasted alone; every platform setting traces to an official page read in that run, cited with URL and date; instructions a vendor page says to remove do not appear; and with no platform given, the answer is a single question.

- First run, on the Codex desktop app: four of six passed. Two failed: one cited, for its assumed model, a page that did not mention that model; the other asked the missing-platform question but added an explanation. After revisions to the skill, three of the requests were run again and all passed.
- Second run, on another host (Claude Code), with the skill path given instead of installing it: three requests passed. In a constructed case with one broken link, the agent named the failure, read the vendor's current page instead and said so in the usage notes.
- After the source list was updated, back on the Codex host: three requests passed. In a case where the first fetch was refused (a plain HTTP request was specified first), the agent read the same page with another tool and said the request was refused, not that the page was gone. All 28 links in the list opened that day.
- Version 0.2.0, again on the Codex desktop app: the original six requests and three new ones that name the model all passed, including a new check that each run opens only the target vendor's source file. When a request names a product but not a model, the skill answers “model unknown” and uses only guidance that does not depend on the model; to get guidance for a specific model, name it.
- Version 0.3.0 changed step 2 from “write the reasoning steps” to “break down the task”, and the first check now reads “the prompt contains a real breakdown of the task”. After the change the same nine requests were run again on Claude Code, with the skill path given instead of installing it: eight passed. The one failure was a summary request for Codex: a usage note was credited to Codex's official prompting page, which does not say it; the note came from the test host's own stored notes, not from the skill or a vendor page. None of the generated prompts scripted the model's reasoning; whether to ask for step-by-step reasoning or a closing self-check was decided from the target model's official pages. The two product-only requests that answered “model unknown” in 0.2.0 this time named an assumed model with a cited reason, which step 5 allows; which answer a product-only request gets can differ between runs and hosts.

These checks look at whether the prompt was built by the method and whether its platform advice traces to official pages. They do not look at how well the prompt works. The generated prompts have not been run on their target platforms with real inputs; installation has not been tested on hosts other than Codex; working without web access and repeated runs of the same request have not been tested. Each test ran one request once and was scored by the agent coordinating the test, not blind. In the 0.1.0 runs, each request took 13 to 344 seconds; in the two runs with readings, each request used about 84,000 to 407,000 tokens (the Codex host's figures count cached input repeatedly).

## When to use it

Use it for prompts you will reuse: system prompts, custom instructions, a task you will run on the same platform for a long time. The quality of the prompt depends on how clearly the purpose is stated; the more specific the purpose, the more steps 1 to 4 have to work with. If the purpose is still vague, write down three things before handing it to the skill: what decision or action the result should support; what must be kept and what must not appear; and what the result must not turn into. For a one-off simple question, just ask it; reading several vendors' pages for it is not worth the cost. The skill also does not test the prompt it writes: before relying on it, try it a few times on the target platform with real inputs.

## Get the skill

The skill is on GitHub: [skills/prompt-architect in github.com/trigpoint-pub/agent-skills](https://github.com/trigpoint-pub/agent-skills/tree/main/skills/prompt-architect). The current version is 0.3.0, released on 2026-11-07 as an experimental prerelease ([release page](https://github.com/trigpoint-pub/agent-skills/releases/tag/prompt-architect-v0.3.0)). You need an agent that can load skills in the `SKILL.md` format, and web access so it can read the vendors' pages. Installation was last verified for 0.2.0, on the Codex desktop app on macOS, and the skill folder's layout has not changed since; 0.3.0 was tested on Claude Code with the skill path given, not installed.

Once it is installed, you can start with:

> Use prompt-architect: write a prompt for reviewing supplier contracts for risky clauses, to run in Claude.

The answer should come in three parts: summary, prompt, usage notes. Read the usage notes first: every platform recommendation should carry an official page URL and the date read, and no platform recommendation should appear without one. A full first-use walkthrough, in Chinese and English with a synthetic set of meeting notes, is in [FIRST-USE.md](https://github.com/trigpoint-pub/agent-skills/blob/main/docs/prompt-architect/FIRST-USE.md).

The test record is in [VALIDATION.md](https://github.com/trigpoint-pub/agent-skills/blob/main/docs/prompt-architect/VALIDATION.md), and where the method comes from and how the source list is kept is in [`docs/prompt-architect/SOURCES.md`](SOURCES.md); neither is installed with the skill. The official sources are listed in one file per vendor. Start at [references/official-sources.md](https://github.com/trigpoint-pub/agent-skills/blob/main/skills/prompt-architect/references/official-sources.md), which says which file to open and has the date of the last check at the top. Report problems through [GitHub Issues](https://github.com/trigpoint-pub/agent-skills/issues); no response time is promised.
