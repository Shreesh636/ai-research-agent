# Analysis Questions — AI Research Agent

As specified in Assignment 13.5.

---

### 1. Why is a Research Agent more effective than manual searching?

A Research Agent is more effective than manual searching because it removes the repetitive, time-consuming parts of research: opening a search engine, visiting multiple pages, reading each one individually, and manually noting key points. In this project, the Chat Trigger, Tavily Search, and Research Agent nodes together perform in seconds what would otherwise take a person many minutes — retrieving up to 8 relevant sources in one call and synthesizing them into a structured report automatically. The result is also consistent: every run produces the same report structure (Executive Summary, Key Findings, Detailed Analysis, etc.), whereas manual research quality varies from person to person and attempt to attempt.

### 2. What is the role of the Tavily Search API?

Tavily is the workflow's source of live, real-world information. The `Tavily Search` node sends the user's topic to `api.tavily.com/search` and receives back a ranked list of relevant web pages (title, URL, content excerpt) plus an optional quick-answer summary. Without Tavily, the AI Agent would be limited to whatever knowledge was in its training data, which can be outdated or incomplete. Tavily gives the agent current, topic-specific evidence to reason over, which is what makes the report reflect real, up-to-date information rather than only the model's internal knowledge.

### 3. Why should AI summarize instead of copying results?

Copying search results directly would produce a report that is really just a collection of excerpts stitched together — disorganized, potentially repetitive, and legally/ethically risky if reproduced verbatim without proper framing. Summarizing and synthesizing, as the Research Agent's system prompt explicitly requires ("Never simply copy or paste source text"), forces the AI to understand the material well enough to explain it in its own words, combine overlapping points from different sources, resolve contradictions, and present a coherent narrative. This produces a genuinely useful, readable report rather than a raw dump of scraped content.

### 4. How does prompt engineering improve report quality?

The Research Agent's system prompt is carefully engineered to fix both **behavior** (analyze and synthesize, never copy verbatim, be factual and objective) and **structure** (an exact, ordered set of Markdown headings: Executive Summary, Introduction, Key Findings, Detailed Analysis, Important Facts, Sources/References, Conclusion). This structural constraint does two things: it makes every generated report predictable and professional-looking regardless of topic, and it makes the report machine-parseable, which is exactly what the `Generate HTML Report` Code node relies on to reliably convert the Markdown into clean HTML. Without this prompt engineering, the model's output format would vary unpredictably and the downstream HTML conversion would frequently fail or produce malformed output.

### 5. What production improvements can be added?

Several improvements would move this from a working assignment prototype toward a production-grade system:

- **Retry logic** with exponential backoff for transient Tavily/Groq failures, instead of failing on the first attempt
- **Caching** of recent search results to reduce redundant API calls and cost for repeated topics
- **PDF export and downloadable report files**, not just in-chat HTML output
- **Persistent storage** (a database) of past reports so users can revisit earlier research
- **Source credibility scoring** to flag or de-prioritize low-quality sources
- **Citation formatting** (APA/MLA) for academic use cases
- **Rate limiting / usage monitoring** to control API costs at scale
- **Authentication** if exposed as a multi-user public service

(These are also listed as Future Scope items in the README and Project Report, and are not implemented in the current workflow.)
