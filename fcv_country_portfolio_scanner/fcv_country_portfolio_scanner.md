**Name:** fcv-country-portfolio-scanner

**Description:** Scan and summarize a World Bank country portfolio by sector, status, and FCV relevance. Use this skill whenever a user needs a structured overview of active projects in a country, project pipeline snapshot, sector-based portfolio analysis, or an FCV-contextualized project inventory. Triggers on phrases like "country portfolio", "project overview", "portfolio scan", "what projects are in [country]?", "active projects by sector", or requests for a country project summary or portfolio health check.

**Content:**

# FCV Country Portfolio Scanner

Scans a World Bank country's active portfolio and generates a sector-organized overview with project status, funding, and FCV/operational relevance flags.

---

## Guardrails

- **Data freshness:** Portfolio data pulled from mAI's internal project search reflects the most recent World Bank systems snapshot. If the user requests a specific cutoff date, note that limitation in the output.
- **FCV flagging:** Projects are marked as "FCV-relevant" only if they explicitly address fragility, conflict, violence, resilience, peacebuilding, or security sector reform; do not over-flag routine projects.
- **Confidentiality:** Do not include projects marked as closed or inactive unless the user specifically requests historical portfolio analysis.
- **Funding accuracy:** Amounts reflect project approval amount, not disbursements. Clearly label as such.

---

## Step 1: Intake — Collect Required Inputs

Ask the user conversationally for the following:

| Field | What to ask | Notes |
|---|---|---|
| **Country** | "Which country's portfolio would you like to scan?" | Required. Accept common name or ISO code. |
| **Sector filter** *(optional)* | "Would you like me to focus on a particular sector (e.g., health, education, governance, infrastructure, finance), or should I provide a full cross-sector overview?" | If none provided, scan full portfolio. |
| **Status filter** *(optional)* | "Should I include only active/implementation projects, or also include planned/pipeline projects?" | Default: active only. |
| **Output format** *(optional)* | "Would you prefer the overview as a summary table, narrative by sector, or both?" | Default: summary table with narrative highlights. |

**Tip:** If the user said "scan [country] portfolio", you have the country; ask for the remaining three fields in a single conversational follow-up.

---

## Step 2: Retrieve Portfolio Data

Use mAI's internal **project search** tool to retrieve:

- All active projects in the specified country (and any planned/pipeline if requested).
- For each project: project name, sector classification, status, approval amount, current disbursement status, project development objective (PDO).
- Any available risk ratings or FCV flags from the project metadata.
- **Project document links:** For each project, retrieve a **set of relevant document links** (not just one), including where available: PAD, latest ISR (and prior ISR if useful), restructuring papers, ICR/ICR Review, aide memoires, and FCV/Safeguards assessments in mAI's internal document store.

**Search strategy:**
- Query: "[Country name] World Bank projects active"
- Filter by: Country = [input country], Status = Active (or Active + Pipeline if user requested)
- Sort by: Sector, then by approval date (most recent first)
- For each project found, use mAI's internal **document search** tool with multiple queries (for example: "[Project Name] PAD", "[Project Name] ISR", "[Project Name] restructuring", "[Project Name] ICR", "[Project Name] safeguards") and return multiple labeled links per key project.

---

## Step 3: Analyze and Organize

Group projects by:

1. **Primary sector** (e.g., Health, Education, Governance, Infrastructure, Finance, Social)
2. Within each sector: **status** (Implementation, Preparation, Closed/Completed) and **FCV relevance** (High, Medium, Low/None)
3. Calculate: Total portfolio size by sector, number of projects, average project size

---

## Step 4: Flag FCV-Relevant Projects

For each project, assess FCV relevance:

- **High:** Explicitly includes conflict sensitivity, peacebuilding, security sector reform, resilience to climate/market shocks, forced displacement response, or governance / justice sector work in FCV context.
- **Medium:** Addresses underlying fragility drivers (human capital, economic opportunity, service delivery gaps) in a fragile country but not explicitly FCV-branded.
- **Low/None:** Routine development in a fragile country without explicit FCV linkage.

---

## Step 5: Generate Output

Present the portfolio overview in the requested format. **All project names should be hyperlinked** with one or more relevant project document links (PAD/ISR and other key documents when available).

### Format Option A: Summary Table (default)

| Sector | # Projects | Total Funding (USD M) | FCV-Relevant | Key Projects | Status Snapshot |
|---|---|---|---|---|---|
| [Sector] | [n] | [amount] | [count] | [project names with document bundle links: e.g., "Health Project XYZ ([PAD](url) | [ISR Apr-2026](url) | [ICR](url))", 1-2 per sector] | [e.g., "3 impl., 1 prep."] |

Followed by a **Narrative Summary** (250–400 words):

- **Portfolio size & composition:** Overview of country portfolio (total projects, sectors, funding).
- **Sector highlights:** 1–2 key projects or trends per major sector (e.g., "Education portfolio pivoting to inclusive primary completion; Health focused on pandemic preparedness").
- **FCV integration:** Brief scan of FCV-relevant projects; any gaps or recommendations.
- **Operational notes:** Any project delays, risk escalations, or coordination needs flagged in metadata.

### Format Option B: Narrative by Sector (if requested)

For each sector, provide:

- **Sector name** (bold heading)
- Active projects: List each project with a small labeled link bundle (for example, [PAD](url), [Latest ISR](url), [Restructuring](url) as available), followed by PDO summary, status, and budget
- FCV flags
- Cross-sector linkages or dependencies

### Format Option C: Both Table and Narrative (if requested)

Present summary table first, then sector narratives.

---

## Step 5a: Document Linking Conventions

When including hyperlinks to project documents:

- **Link text:** Use the project's short name or acronym (e.g., "Health Project XYZ" or "HPX") for readability in tables; full project name in narrative sections.
- **Number of links per key project:** Include multiple links where possible (target 2-4 links for key projects) rather than only one document.
- **Link target:** Prioritize links to:
  1. Most recent **Implementation Status & Results (ISR)** report (for active projects)
  2. **Project Appraisal Document (PAD)**
  3. Most relevant additional document(s): restructuring paper, ICR/ICR Review, aide memoire, and/or FCV or Safeguards assessment (as available)
- **Link availability:** If document links are not available in mAI's internal store, note in the output: "[Project Name] (document links unavailable in current system)".
- **Format:** Standard markdown: `[display text](url-to-document)`

---

## Step 6: Conclude with Metadata Note

Append a brief footer:

*"Portfolio snapshot as of [today's date]. Reflects active/approved projects in World Bank systems. Funding amounts are approval values; disbursement status available upon request. FCV flagging is based on stated project objectives; local context and implementation realities may differ."*

---

## Quality Checklist (self-review before returning)

- [ ] Country correctly identified and spelled
- [ ] All active projects in country included (or filtered by user request)
- [ ] Projects grouped by sector clearly
- [ ] FCV-relevant projects correctly flagged (not over-flagged)
- [ ] Funding amounts labeled as approval values
- [ ] Output format matches user request (table / narrative / both)
- [ ] **Project names hyperlinked** with multiple relevant document links per key project where available (not only PAD/ISR)
- [ ] Metadata note included
- [ ] No confidential or closed project details unnecessarily exposed

---

## AI Disclaimer

*This skill generates portfolio overviews based on World Bank project data and open-source sector context. FCV relevance flagging reflects stated project objectives only and does not substitute for on-the-ground context, local expertise, or formal project performance reviews. Use this overview for brainstorming and strategic planning only; consult formal portfolio performance reports and country teams for decision-making.*
