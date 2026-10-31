# OpenAI: where to read

Covers ChatGPT, Codex, and the OpenAI API. This file lists pages to read. It does not say what they contain; read the pages themselves.

## Where to start

1. The general prompting guides below.
2. The latest model guide, with `?model=<model id>` once you know the model.
3. The models catalog entry for that model, for the settings it accepts.
4. For Codex, the three Codex pages as well.

## Which page to check for each point

The first six rows are the points Step 5 asks for; any later row covers a specific case. Start with the page named here; if it does not cover the point, check the other general guides before saying the point was not covered. The pairing follows the page titles and is a starting point, not a summary of the pages.

| Point (Step 5) | Start with |
|---|---|
| Which model a product uses | Model release notes; for Codex, Codex Models |
| How to structure the prompt | Prompt engineering · Prompt guidance; for Codex, Codex Prompting |
| Reasoning or effort controls | Reasoning models · Models catalog; for Codex, Codex Models |
| Instructions to remove or avoid for this model | Latest model guide for that model |
| Output formatting | Prompt guidance · Latest model guide |
| Preview, beta, or legacy status | Models catalog · Model release notes |
| Repository instructions for a coding agent | Custom instructions with AGENTS.md |

## Pages

General guides

- Prompt engineering: https://developers.openai.com/api/docs/guides/prompt-engineering
- Prompt guidance: https://developers.openai.com/api/docs/guides/prompt-guidance
- Reasoning models: https://developers.openai.com/api/docs/guides/reasoning
- Latest model guide (add `?model=<model id>` for a specific model): https://developers.openai.com/api/docs/guides/latest-model
- Models catalog (settings each model accepts, such as reasoning effort levels): https://developers.openai.com/api/docs/models
- Model release notes: https://help.openai.com/en/articles/9624314-model-release-notes

Codex (the old `developers.openai.com/codex/` addresses redirect to these)

- Prompting: https://learn.chatgpt.com/docs/prompting
- Models (recommended models, choosing reasoning effort): https://learn.chatgpt.com/docs/models
- Custom instructions with AGENTS.md: https://learn.chatgpt.com/docs/agent-configuration/agents-md

Model pages, examples of the pattern

- https://developers.openai.com/api/docs/guides/latest-model?model=gpt-6.1-sol
- https://developers.openai.com/api/docs/models/gpt-6.1-sol
