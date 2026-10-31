# Official sources

First-party documentation from the model vendors, one file per vendor. Read the pages themselves; these files only tell you where to start.

Source-list revision: 2026-10-31. Links last confirmed to open: 2026-11-01 (27 links opened with HTTP 200 using curl, including 3 redirects; the OpenAI Model Release Notes page returned HTTP 403 to curl and opened with the web reader).

## Which file to open

| The prompt will run in | Open |
|---|---|
| ChatGPT, Codex, the OpenAI API, or another OpenAI model | [openai.md](openai.md) |
| Claude, Claude Code, the Claude API, or another Anthropic model | [anthropic.md](anthropic.md) |
| Gemini, the Gemini API, Vertex AI, or another Google model | [google.md](google.md) |
| Anything else | None of these; see "If the platform has no official prompting guidance" in `SKILL.md` |

Open only the target vendor's file. The prompt uses one platform's conventions, so the other vendors' pages are not needed.

## How to use a vendor file

Start with the vendor's general guide and its latest-model or model page, then open the page for the exact model if one exists. Each file pairs the points Step 5 asks for with the page to check first. Model-specific pages are replaced when new models come out, so the ones listed under "Model pages" are examples of the pattern at the time of compiling, not a complete or permanent list.
