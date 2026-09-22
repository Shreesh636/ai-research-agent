# Viva Questions — AI Research Agent

Practical, speakable answers for a viva/oral defense of this project.

---

**1. What is an AI Research Agent?**
It's an automated system that takes a research topic, searches the web for current information, uses an AI model to analyze and synthesize that information, and produces a structured report — without the user doing any manual searching or writing.

**2. Why is Tavily used instead of a normal search engine?**
Tavily is built specifically for AI applications. Instead of returning raw HTML pages like a normal search engine, it returns clean, structured results — title, URL, and content excerpt — plus an optional summarized answer, which is much easier for an AI model to consume directly.

**3. Why use an API instead of scraping websites directly?**
An API gives structured, reliable, and legal access to data with a stable format, authentication, and rate limits. Scraping websites directly would be fragile (pages change layout), potentially against terms of service, and would require a lot of extra parsing code.

**4. What is n8n?**
n8n is a visual workflow automation tool. You build workflows by connecting nodes on a canvas instead of writing a full backend application by hand. Each node does one job — like making an HTTP request, running JavaScript, or calling an AI model — and data flows between them.

**5. What is workflow automation?**
It's the practice of using software to perform a sequence of tasks automatically instead of a person doing each step manually. In this project, the whole "search, analyze, write report" process runs automatically once you provide a topic.

**6. What is an AI Agent?**
An AI Agent is a component that uses a large language model, combined with a specific role/instructions (a system prompt), to reason over given information and produce a response — in this case, analyzing search results and writing a structured report.

**7. Why use Groq specifically?**
Groq provides very fast LLM inference, which keeps the workflow responsive. It hosts open models (here, `openai/gpt-oss-120b`) that can be called through a simple API, similar to other LLM providers.

**8. What is prompt engineering?**
It's the practice of carefully designing the instructions given to an AI model so it produces the output you want, in the format you want. In this project, the system prompt tells the model exactly which headings to use and in what order, and instructs it not to copy source text directly.

**9. Why shouldn't search results simply be copied?**
Copying verbatim would just be a collection of excerpts, not a real report — it would be disorganized, potentially redundant, and could raise copyright concerns. Synthesizing forces the AI to actually understand and combine the information into original, coherent writing.

**10. What is a REST API?**
It's a way for two systems to communicate over HTTP using standard methods (GET, POST, etc.) and structured data formats like JSON. The Tavily Search node uses a REST API call (`POST` request) to get search results.

**11. What happens if Tavily fails?**
The `Tavily Search` node is configured with `continueErrorOutput`, so instead of crashing the workflow, it routes to a `Search Error` node, which returns a clear message telling the user the search failed and to check the API credential.

**12. What happens if the user doesn't provide a topic?**
The `Has Topic?` node checks whether the trimmed input is empty. If it is, the workflow routes to `Missing Topic Error`, which asks the user to provide a topic — without ever calling Tavily or Groq unnecessarily.

**13. What does the JavaScript Code node do?**
There are two Code nodes in this workflow. `Process Search Results` reformats the raw Tavily JSON into a clean text block for the AI prompt. `Generate HTML Report` converts the AI's Markdown output into a styled, self-contained HTML document.

**14. Why generate HTML instead of just showing text?**
HTML lets the report be displayed with proper formatting — headings, bullet points, clickable source links — and can be opened directly in any browser, which is much more usable and professional than plain text.

**15. What is the role of the Research Agent?**
It's the reasoning step of the workflow: it receives the topic and the search results, and is responsible for producing an accurate, well-organized, original written report following a strict structure.

**16. What are the limitations of this project?**
It depends on Tavily's search quality, doesn't retry automatically after a failure, doesn't store past reports, is limited to 8 results per search, and doesn't export to PDF yet.

**17. How could the system be improved?**
By adding retry logic, PDF export, a database to store past reports, source credibility scoring, proper citation formatting, and scheduled/automated research runs.

**18. What is the difference between the Chat Trigger and the HTTP Request node?**
The Chat Trigger starts the workflow when a user sends a chat message — it's the entry point. The HTTP Request node (used for Tavily) actively sends a request to an external API and waits for a response — it's used mid-workflow to fetch data.

**19. Why is the temperature set to 0.3 on the Groq model?**
Temperature controls randomness/creativity in the model's output. A low value like 0.3 makes the output more focused, factual, and consistent — appropriate for a research report rather than creative writing.

**20. Could this workflow be adapted for other use cases?**
Yes — the same pattern (validate input → fetch external data → AI synthesis → formatted output) could be reused for other automated reporting use cases, like market research summaries, news digests, or competitor analysis, by changing the search query and prompt.
