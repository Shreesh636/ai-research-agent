# Test Cases — AI Research Agent

| # | Test Case | Input | Expected Behavior | Actual Result / Status |
|---|---|---|---|---|
| 1 | Valid research topic | `Impact of Artificial Intelligence on Education` | Chat Trigger → Extract Topic → Has Topic? (yes) → Tavily Search succeeds → Process Search Results → Research Agent synthesizes sources → Generate HTML Report produces a complete, styled HTML report | **Tested Successfully** — confirmed via live execution with real Tavily and Groq credentials (8 real sources returned, valid HTML output with all 8 required sections). See execution screenshot. |
| 2 | Empty research topic | *(empty message / whitespace only)* | Has Topic? evaluates false → routes to Missing Topic Error → returns: "No research topic was provided. Please send a topic you would like me to research." | **Expected Behavior** — confirmed by workflow logic (`notEmpty` check on trimmed `topic`); not separately screenshotted. |
| 3 | Tavily / search API failure | Any topic, with Tavily API unreachable or credential invalid | Tavily Search node fails → `onError: continueErrorOutput` routes to Search Error → returns: "The web search request failed. Please check the Tavily API credential and try again later." | **Expected Behavior** — confirmed by node configuration (`onError: continueErrorOutput` present on Tavily Search node). |
| 4 | AI / Groq failure | Any topic, with Groq API unreachable or credential invalid | Research Agent node fails → `onError: continueErrorOutput` routes to AI Error → returns: "The AI model failed to generate the research report. Please check the Groq credential and try again." | **Expected Behavior** — confirmed by node configuration (`onError: continueErrorOutput` present on Research Agent node). |

## Notes on Test Status Terminology

- **Tested Successfully** — the scenario was actually executed and observed to work, with evidence (screenshot/output).
- **Expected Behavior** — the scenario is not independently reproduced with a screenshot here, but the outcome is guaranteed by the workflow's explicit configuration (the `IF` condition or the `onError` setting on the relevant node), inspected directly in the exported JSON.

No test results have been fabricated. Only Test Case 1 has direct screenshot evidence of a full live run; Test Cases 2–4 are validated by inspecting the workflow's own conditional logic and error-routing configuration.
