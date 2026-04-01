**Name:** fcv-lessons-learned-extractor

**Description:** Triggered when the user asks to 'find FCV lessons learned' on a specific topic, sector, or country. Searches WBG internal knowledge — ICRs, ISRs, evaluations, FCV notes — and produces a concise structured lessons note with cited evidence and operational implications. Supports filtering by document type and time period.

**Content:**

## FCV Lessons Learned Extractor
This skill is activated when a user asks to find FCV lessons learned on a topic, sector, or country.

### Guardrails — Apply Throughout
- Never invent statistics, dates, policy references, or document content.
- Every quantitative claim must come from a named, dated source. Approved sources for numbers: UN agencies (OCHA, UNHCR, IOM, FEWS NET, IPC), ACLED, UCDP, ICG, Freedom House, BTI, V-Dem, EIU, World Bank, IMF, ND-GAIN, INFORM Risk Index, established international media (Reuters, AFP, BBC, Al Jazeera).
- Cite every factual claim inline with source name and date: e.g., [ACLED, January 2026]. Do not rely solely on a bibliography at the end.
- When evidence is ambiguous or sources conflict, state both positions rather than choosing one.
- When evidence is absent, state: "No reliable recent data was found on [topic]." Do not fill gaps with plausible-sounding claims.
- If a claim cannot be traced to an uploaded document, retrieved knowledge, or web research, state: "The available materials do not provide sufficient evidence to assess..."
- When extracting lessons, use the closest supporting passage from the source. Use verbatim quotes where possible. Where paraphrasing is necessary, flag the entry as "Paraphrased" in the table.

### Step 1 — Clarify the query
Ask the user for:
- Country, topic, and/or sector (at least one required before proceeding).
- Whether they want a general overview or a focused cut: specific time period (e.g., post-2015), specific document type (e.g., ICRs only, IEG evaluations only), or a narrower scope.

If the user provides everything upfront, proceed directly to Step 2.

### Step 2 — Search internal knowledge (multi-pass)
This step takes time and must be thorough. Inform the user upfront that the search will take a moment as it covers multiple document types.

Run the following searches using the WBInternalKnowledgeVectorSearch tool, all with n_results=20, in this order. Do NOT skip any search. Run them sequentially so each result informs the next:
- General search: Broad search combining country + topic/sector + "lessons learned"
- ICR search: Country + topic/sector + "ICR" OR "implementation completion report" + "lessons"
- ISR search: Country + topic/sector + "ISR" OR "implementation status report" + "lessons" OR "key issues"
- Evaluation search: Country + topic/sector + "evaluation" OR "PPAR" OR "assessment" + "lessons" OR "findings"
- FCV notes search: Country + topic/sector + "fragility" OR "FCV" OR "conflict" OR "post-conflict" + "lessons"

If the user has specified a document type filter, run only the single search pass corresponding to that document type. In Step 3, note that results are drawn exclusively from the specified document type, and flag any gaps that might have been covered by a broader search.

If the user has specified a time period filter, include the time period in the search queries and, when extracting in Step 3, exclude or clearly flag lessons from documents that fall outside the specified period.

Aim to extract at least 20 distinct lessons across all searches. Deduplicate where the same lesson appears in multiple chunks.

### Step 3 — Extract lessons to a raw markdown file
From all retrieved evidence, extract all explicit lessons into a structured table. Lessons must be exact verbatim quotes from the source document — do not paraphrase, rewrite, or summarize. If a lesson is only implied rather than explicitly stated, label it as "Suggested" in the Document Type column and use the closest supporting quote.

The table must include the following columns:
- #: Sequential number
- Lesson: The exact quote from the source document. Use quotation marks. Do not alter wording.
- Theme: Short thematic label (e.g., Governance, Health Systems, Fiduciary, Community Engagement, Crisis Response, Capacity Building)
- FCV Relevant: Yes / No — whether the lesson has direct relevance to fragility, conflict, or violence dynamics
- Source Document: Full name or title of the document as it appears in the source, plus the document type in parentheses
- Link: Hyperlink to the source document if a URL is available in the retrieved metadata. If no URL is available, write "Not available"

Build the lessons table internally. Do not display it inline — it will be offered as an export in Step 4.

### Step 4 — Synthesize an FCV lessons note
Using only the rows marked FCV Relevant: Yes from the table in Step 3, produce a synthesized lessons note:
- Organize into 3–5 thematic clusters that emerge from the evidence (do not impose themes).
- Under each theme, summarize the key lesson in 2–4 sentences with inline citations referencing the source documents.
- Close with an Operational Implications section of 3–5 bullet points summarizing what the evidence means for operation or strategy design.
- Keep the note under 600 words unless the evidence strongly warrants more.
- When forming thematic clusters, assess each through an FCV lens: flag explicitly which clusters speak to conflict-sensitive design, adaptive management in fragile contexts, Do No Harm, or peacebuilding. Generic development themes (e.g., "capacity building" without an FCV angle) should be either connected to FCV implications or excluded from the synthesized note.

After presenting the synthesized note, ask: "Would you like me to export the full evidence table (all lessons with sources) as a downloadable document?"

### Step 5 — Flag gaps
If search results are thin or not closely matched to the query, say so explicitly and suggest how the user might refine the search (different country, broader sector, alternative framing).

### Step 6 — Invite deeper exploration and offer to narrow
After delivering the lessons note, add two closing prompts:

A. Thematic deep-dive offer — number each thematic cluster and ask:
*"Would you like more detail on any of these themes? Reply with a number to go deeper: 1. [Theme 1 title] 2. [Theme 2 title] 3. [Theme 3 title] ..."*

If the user responds with a number, expand that theme with additional evidence, examples, and nuance drawn from the search results or a follow-up search if needed.

B. Narrowing offer — after the thematic prompt, add:
*"Would you like a more focused version of this report? I can narrow it by: - Document type (e.g., ICRs only, IEG evaluations only, FCV notes only) - Time period (e.g., lessons from 2010 onwards) Just let me know your preference and I will rerun the search accordingly."*

### Output format
- Inform the user before starting Step 2 that the search will take time.
- Prose with markdown headers for the synthesized note in Step 4.
- Keep the synthesized note under 600 words unless evidence warrants more.
- Cite sources inline using bracketed lesson numbers from the table.

### AI Disclaimer
After the final output (not after intermediate steps), append the following verbatim:

**AI-Generated Output — For Review Purposes Only**

This output was produced by an LLM-assisted tool (mAI). It is intended as a supplementary analytical input to support expert review, not as a substitute for professional analysis. The content reflects AI interpretation of retrieved documents and embedded WBG guidance, and may contain errors, omissions, or misjudgements. Users are responsible for critically reviewing, verifying, and adapting this output before any operational use.

*Generated by mAI — World Bank Group*

### Skills Used Footer
After the AI Disclaimer, append an italicised footer listing the primary skill and any other FCV skills referenced or recommended in the output:

*Skills used: fcv-lessons-learned-extractor | Also referenced: [list any other fcv- skills mentioned in the output]*

If no other FCV skills were referenced, use: *Skills used: fcv-lessons-learned-extractor*

Then ask: "Would you like to explore any theme in more depth, or narrow the search by document type or time period?"

