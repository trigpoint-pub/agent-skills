# Sources and limits

## Where the method comes from

The skill has two layers, and they come from different places.

- **Task method (Steps 1 to 4 and the writing rules).** A working method for writing prompts whose arrangement is Trigpoint's (2026); its components follow the vendors' own guidance: classify the task, break it down into sub-tasks and decisions, set measurable success criteria, fix the output fields, then express the result in the target platform's conventions. It was developed and used privately before this release. It is a method, not a research result; it has not been compared against other prompting methods.
- **Platform conventions (Step 5).** Not included in the skill. The agent reads them at run time from the vendors' own documentation, listed in one file per vendor under `skills/prompt-architect/references/` (`official-sources.md` says which file to open).

## Why no vendor rules are included

A private version of this skill carried a table of per-vendor conventions, maintained by hand after each model release. That table is not published here, for two reasons:

1. It was a summary of the vendors' documentation. The vendors' own pages are the authority and are public; a second-hand summary adds a way to be wrong without adding information.
2. It went out of date with every release and had to be rebuilt each time. Reading the current pages avoids carrying a stale copy.

Since 0.2.0 the source list is split by vendor: the agent opens only the target vendor's file, and each file pairs the points Step 5 asks for with the page to check first. The pairing follows page titles. The files still state no conventions; the agent reads them from the pages.

## How the source list is kept

- Only first-party pages from the vendors (OpenAI, Anthropic, Google) are listed. Blogs, forums, third-party guides, and papers are not.
- General guides are listed first because they change less. Model-specific pages are listed as examples of the pattern only.
- Each release of the skill checks that every listed link opens; the date of the last check is at the top of `official-sources.md`.

## Third-party material

- The text of this skill is original writing. It names vendor documentation by title and URL; it does not reproduce passages from it.
- No third-party code, data, or images are included.

## Known limits

- Testing is limited; see `VALIDATION.md`.
- The result depends on the agent reading the right pages. If the vendor's pages are unclear or contradict each other, the prompt can inherit that.
- The skill has no code. Reading the pages, citing them, and following the steps depend on the agent following the written instructions.
