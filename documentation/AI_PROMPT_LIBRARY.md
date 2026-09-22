# AI Prompt Library — AI Research Agent

This document contains the actual prompts used by the **Research Agent** node in the workflow, taken directly from `workflow/AI_Research_Agent.json`.

---

## 1. System Prompt (as implemented)

```
You are an expert research analyst. You are given a research topic and a set of web search sources.
Analyze and synthesize the sources into an original, well-structured research report. Never simply copy or paste source text.

Produce the report in clean Markdown using EXACTLY these sections and headings, in this order:
# <Research Title>
## Executive Summary
## Introduction
## Key Findings (use a bulleted list)
## Detailed Analysis
## Important Facts (use a bulleted list)
## Sources / References (list each source title with its URL)
## Conclusion

Be factual, cite sources where relevant, and keep the writing professional and objective.
```

## 2. User Prompt (as implemented)

```
Research topic: {{ $json.topic }}

Tavily quick answer: {{ $json.answer }}

Web search sources:
{{ $json.sourcesText }}

Using ONLY the information in these sources, write a complete structured research report on the topic. Do not copy the sources verbatim — synthesize and analyze them.
```

## 3. Input Variables

| Variable | Source | Description |
|---|---|---|
| `$json.topic` | Extract Topic node, passed through Process Search Results | The user's research topic, trimmed |
| `$json.answer` | Tavily API response, field `answer` | Tavily's own synthesized quick answer for the query (may be empty) |
| `$json.sourcesText` | Built in Process Search Results (Code node) | Numbered plain-text block of up to 8 sources, each with title, URL, and content excerpt |

## 4. Output Structure

The agent is required to return Markdown with exactly these headings, in this order:

1. `# <Research Title>`
2. `## Executive Summary`
3. `## Introduction`
4. `## Key Findings` (bulleted list)
5. `## Detailed Analysis`
6. `## Important Facts` (bulleted list)
7. `## Sources / References` (title + URL per source)
8. `## Conclusion`

This output is consumed directly by the `Generate HTML Report` Code node, which parses these exact heading levels and list markers into HTML.

## 5. Why This Prompt Is Effective

- **Role framing** ("expert research analyst") sets tone and depth expectations.
- **Explicit anti-copying instruction** reduces the risk of the report being a near-verbatim reproduction of source text.
- **A fixed, ordered heading structure** removes ambiguity about report format, which both improves readability for a human and makes the output reliably parseable by the downstream HTML-generation code — without that code needing a full Markdown-parsing library.
- **Grounding instruction** ("Using ONLY the information in these sources") reduces hallucination by anchoring the model's answer to the retrieved Tavily results rather than unconstrained prior knowledge.
- **Low temperature (0.3)** on the Groq model complements the prompt by favoring consistent, factual phrasing over creative variation.

## 6. How Prompt Engineering Improves Consistency

Because the heading text, order, and list formatting are specified exactly (rather than left to the model's judgment), every report — regardless of topic — arrives in the same predictable shape. This is what allows a simple, hand-written Code node (rather than a general Markdown library or a second LLM call) to reliably convert the output into valid HTML every time, which is a meaningful engineering advantage for a workflow that needs to run unattended.

---

## 7. Optional Improved Version *(Not implemented — suggestion only)*

The following is **not** present in the current workflow. It is offered only as an optional enhancement idea:

```
System Prompt (Optional Improved Version):

You are an expert research analyst producing a report for an academic/professional audience.
Follow the exact heading structure specified below. For every claim in "Key Findings" and
"Important Facts", include an inline citation marker like [1], [2] that corresponds to the
numbered source list. If sources conflict, note the disagreement explicitly rather than
silently picking one. If the provided sources are insufficient to answer part of the topic,
state that clearly instead of guessing.
```

This optional version adds inline citation markers and explicit handling of conflicting or insufficient sources — improvements that could increase academic rigor, but they are **not part of the current, working implementation** and would require corresponding changes to the HTML-generation code to render citation markers correctly.
