# AI Research Agent — Presentation Structure (15 Slides)

---

### Slide 1 — Title
**Bullets:**
- AI Research Agent
- Shreesh | B.Tech CSE

**Speaker Notes:** Introduce yourself and the project name. Mention this is built using n8n workflow automation as part of Assignment 13.5.

**Visual suggestion:** Project title, your name, maybe the n8n logo.

---

### Slide 2 — Introduction
**Bullets:**
- Automates web research using AI
- Built entirely on n8n (workflow automation)
- Combines search + AI reasoning + report generation

**Speaker Notes:** Briefly explain what the project does in one sentence before diving into details.

**Visual suggestion:** A simple icon row: search → AI → report.

---

### Slide 3 — Problem Statement
**Bullets:**
- Manual research is slow and repetitive
- Requires visiting many sites and compiling notes
- No consistent report format

**Speaker Notes:** Describe the pain point this project solves, based on your own research experience.

**Visual suggestion:** Before/after comparison graphic.

---

### Slide 4 — Objectives
**Bullets:**
- Accept a topic via chat
- Search the web in real time
- Synthesize sources using AI
- Generate a structured HTML report
- Handle errors gracefully

**Speaker Notes:** Walk through each objective quickly; these map directly to assignment requirements.

**Visual suggestion:** Numbered checklist graphic.

---

### Slide 5 — Proposed Solution
**Bullets:**
- Single n8n workflow: Chat → Search → AI Agent → HTML
- Tavily for live web search
- Groq LLM for analysis
- Automatic HTML formatting

**Speaker Notes:** Summarize the end-to-end solution in one breath before the architecture slide.

**Visual suggestion:** Simple horizontal pipeline diagram.

---

### Slide 6 — Technology Stack
**Bullets:**
- n8n (automation engine)
- Tavily Search API
- Groq (LLM inference)
- JavaScript (Code nodes)
- HTML/CSS output

**Speaker Notes:** Mention why each tool was chosen — e.g., Groq for fast inference, Tavily for AI-optimized search results.

**Visual suggestion:** Logo grid of the tools used.

---

### Slide 7 — System Architecture
**Bullets:**
- Chat Trigger → Extract Topic → Validation
- Tavily Search → Process Results
- Research Agent (Groq) → HTML Generation
- Three error-handling branches

**Speaker Notes:** Use this slide to show the full node diagram from ARCHITECTURE.md.

**Visual suggestion:** Insert the Mermaid architecture diagram or a screenshot of the n8n canvas.

---

### Slide 8 — Workflow
**Bullets:**
- 11 nodes, 3 functional groups
- Validate topic → Search the web → Generate report
- Modular, easy to extend

**Speaker Notes:** Explain the grouping used in the actual JSON (`nodeGroups`), and why modularity matters.

**Visual suggestion:** Screenshot of the n8n canvas showing the grouped nodes.

---

### Slide 9 — Tavily Search API
**Bullets:**
- Advanced search depth
- Up to 8 results per query
- Includes a quick-answer summary
- Returns title, URL, and content excerpt per result

**Speaker Notes:** Explain why Tavily specifically (AI-optimized search) rather than a general search engine.

**Visual suggestion:** Sample Tavily JSON response snippet.

---

### Slide 10 — AI Research Agent + Groq
**Bullets:**
- LangChain Agent node performs the reasoning
- Groq model: openai/gpt-oss-120b, temperature 0.3
- System prompt enforces synthesis, not copying
- Fixed report structure (7 sections)

**Speaker Notes:** This is the core AI slide — explain the system prompt design briefly.

**Visual suggestion:** Diagram showing prompt → LLM → structured Markdown output.

---

### Slide 11 — HTML Report Generation
**Bullets:**
- Custom JavaScript Markdown-to-HTML converter
- Embedded CSS, no external dependencies
- Fully self-contained, browser-ready file

**Speaker Notes:** Mention that no external libraries are used — the parser is hand-written for this exact report format.

**Visual suggestion:** Screenshot of the final HTML report rendered in a browser.

---

### Slide 12 — Error Handling
**Bullets:**
- Missing Topic Error
- Search Error (Tavily failure)
- AI Error (Groq/Agent failure)
- Each returns a clear, user-friendly message

**Speaker Notes:** Emphasize that failures are handled explicitly, not left to crash the workflow.

**Visual suggestion:** Simple flowchart of the three error branches.

---

### Slide 13 — Testing & Results
**Bullets:**
- Tested live with real Tavily and Groq credentials
- Confirmed real API responses (request ID, response time)
- Full HTML report generated with all required sections

**Speaker Notes:** Reference the execution screenshot as evidence of a successful live test run.

**Visual suggestion:** Insert the execution screenshot.

---

### Slide 14 — Advantages & Future Scope
**Bullets:**
- Advantage: fully automated, consistent, fast
- Future Scope: PDF export, database storage, citation management, scheduled runs

**Speaker Notes:** Be clear that the Future Scope items are not implemented yet — they are proposed improvements.

**Visual suggestion:** Two-column layout: "Today" vs. "Future Scope."

---

### Slide 15 — Conclusion / Thank You
**Bullets:**
- Successfully automated end-to-end research
- Meets all core assignment requirements
- Thank you — questions welcome

**Speaker Notes:** Close by restating the core value: turning one chat message into a complete, structured research report.

**Visual suggestion:** Thank-you slide with your name and contact/GitHub link.
