**Name:** fcv-portfolio-risk-impact-assessment

**Description:** Cross-analyze a country's FCV risk landscape with its active World Bank portfolio to assess project vulnerability and operational implications. Use this skill whenever a user needs to understand how identified fragility, conflict, or violence risks could affect project implementation, disbursement, or outcomes. Triggers on phrases like "portfolio risk impact", "how will risks affect projects", "risk impact assessment", "portfolio vulnerability analysis", "risk-adjusted portfolio brief", or requests for a synthesis of country risks and project realities.

**Content:**

# FCV Portfolio Risk Impact Assessment

Synthesizes country-level FCV risks with an active World Bank portfolio to produce a vulnerability briefing showing how identified risks threaten specific projects, sectors, and implementation timelines.

---

## Guardrails

- **Risk-project nexus:** Link only risks that have direct or plausible operational consequences for projects (e.g., insecurity blocking field access, governance breakdown disrupting counterpart capacity, displacement affecting service demand). Do not over-connect risks to projects.
- **Specificity:** Do not generalize. Identify specific projects vulnerable to specific risks; avoid blanket statements like "all health projects are at risk".
- **Contingency vs. impact:** Distinguish between projects that could absorb minor disruptions (low contingency risk) and those with brittle timelines or dependent partners (high contingency risk).
- **Probability vs. severity:** Flag both high-probability/low-severity risks and low-probability/high-severity "tail risks" that could derail projects.
- **Project documentation links:** Every project mentioned in the brief must include at least one hyperlink to a relevant project document (PAD, ISR, restructuring paper, or safeguards assessment). Do not discuss projects without direct links to supporting documentation.

---

## Skill Integration Note

**This skill combines two prerequisite skills:**
1. **fcv-country-risk-scan** — generates the country FCV risk briefing
2. **fcv-country-portfolio-scanner** — generates the active portfolio overview

**Preferred workflow:** If the user has not already run these skills, **activate both skills first** to generate their outputs, then proceed with this risk-impact analysis. Do not re-run risk scanning or portfolio retrieval here; consume the outputs from those skills and focus this skill's effort on cross-linking risks to projects and generating adaptive recommendations.

---

## Step 1: Intake & Prerequisites

Ask the user:

| Field | What to ask | Notes |
|---|---|---|
| **Country** | "Which country are we assessing?" | Required. Must match country in risk scan + portfolio scanner. |
| **Risk scan ready?** | "Do you have a completed FCV country risk scan for this country, or should I generate one first?" | Can proceed with existing risk scan or generate new one. |
| **Portfolio ready?** | "Do you have a portfolio scanner output for this country, or should I pull the current portfolio?" | Can proceed with existing portfolio or generate new one. |
| **Sector focus** *(optional)* | "Would you like me to focus on particular sectors, or assess the full portfolio?" | Default: full portfolio. |
| **Output preference** | "Would you prefer a cross-matrix (risks × projects), narrative by risk, or narrative by sector?" | Default: both matrix and narrative. |

**Tip:** If the user says "assess [country]'s portfolio against risks", you have the country; generate the risk scan and portfolio from Steps 2–3 if not already available, then proceed to analysis.

---

## Step 2: Verify or Generate FCV Risk Scan

If the user has not provided a risk scan:

- **ACTIVATE the fcv-country-risk-scan skill** to generate a structured brief covering:
  - Institutional fragility and political tensions
  - Conflict and violence dynamics
  - Displacement and refugee movements
  - Government–development actor relations

If the user has provided a risk scan or indicated one exists, **parse and extract key risk themes** (specific risks, actors, timelines, geographic scope).

---

## Step 3: Verify or Retrieve Country Portfolio

If the user has not provided a portfolio:

- **ACTIVATE the fcv-country-portfolio-scanner skill** to generate a sector-organized portfolio overview with:
  - Project names, PDOs, status, and funding
  - Sector groupings
  - FCV relevance flags

If the user has provided a portfolio output, **parse and extract project details** (name, sector, status, key dependencies, partners/counterparts).

---

## Step 4: Map Risk–Project Vulnerabilities

Create a **risk-project nexus analysis** by cross-checking each key risk against each project:

| Risk Identified | Affected Sectors | Affected Projects | Vulnerability Type | Severity | Mitigation Strategy |
|---|---|---|---|---|---|
| [Risk name] | [sectors most exposed] | [specific projects] | [e.g., "field access", "counterpart capacity", "demand shock"] | High/Medium/Low | [brief mitigation option] |

**Vulnerability types to flag:**
- **Field access:** Insecurity, displacement, or infrastructure disruption blocking implementation team or beneficiary access
- **Counterpart capacity:** Political instability, executive turnover, or governance breakdown weakening government partner ability to co-implement
- **Demand shock:** Displaced populations, market collapse, or crisis migration altering project target populations or service demand
- **Supply chain:** Cross-border conflict, trade disruption, or commodity price shocks affecting project input or service delivery
- **Fiduciary risk:** Corruption, informal taxation, or security-linked extortion eroding project budget or oversight
- **Staff safety:** Deteriorating security threatening project or partner staff presence in-country

---

## Step 5: Generate Output — Narrative Briefing

Structure the output as a **Portfolio Risk Impact Brief** (800–1,200 words):

### Section 1: Executive Summary

- Overall portfolio exposure: % of portfolio in high-risk sectors; # of high-vulnerability projects
- Key tail risks: 1–2 low-probability but high-impact scenarios that could derail multiple projects
- Recommended immediate actions: Pause points, contingency reviews, or priority reallocations

### Section 2: Risk-by-Risk Portfolio Impact

For each **critical risk identified in the country risk scan**:
- Risk description (1–2 sentences)
- Affected projects (list with hyperlinks to PAD/ISR or other project documents; note $ exposure)
- Specific vulnerability pathways
- Probability and severity
- Recommended adjustments (e.g., accelerate disbursement, shift implementation modality, increase monitoring)

### Section 3: Sector-by-Sector Resilience Assessment

For each **major sector** in the portfolio:
- Sector overview (# projects, total funding, FCV relevance)
- Risk exposure summary (which risks most threaten this sector)
- Green/yellow/red status indicator
- Sector-level adaptive management recommendations

### Section 4: High-Vulnerability Projects (Deep Dive)

Highlight **top 3–5 highest-vulnerability projects** (by combined risk × disbursement exposure):
- Project name (with hyperlinks to relevant project documents: PAD, latest ISR, restructuring, or safeguards assessment as available)
- Risk profile (specific risks + vulnerability types)
- Current status & disbursement timeline
- Recommended contingencies (scenario planning options)

### Section 5: Portfolio Adaptive Management Recommendations

Synthesize cross-cutting recommendations:
- **Pipeline adjustments:** New projects to fast-track, pause, or redesign
- **Implementation modality shifts:** Move from in-person to remote monitoring; shift from community-based to nationally-managed components
- **Contingency planning:** Trigger points for portfolio pause/rebalance; communication protocols with Government
- **Monitoring escalation:** Indicator thresholds that trigger portfolio review or contingency activation

---

## Step 6: Output Formats

### Format Option A: Cross-Matrix + Narrative (recommended)

1. **Risk–Project Vulnerability Matrix** (table as in Step 4)
2. **Narrative Brief** (Sections 1–5 as above)

### Format Option B: Narrative Only

Integrate matrix insights into flowing narrative (Sections 1–5); omit separate table.

### Format Option C: Sector-Focused Narrative

Reorder as: Executive Summary → Sector Resilience → Risk Deep-Dive by Sector → Adaptive Management Recommendations (instead of risk-by-risk).

---

## Step 7: Metadata & Caveats

Conclude with:

*"Risk-impact assessment as of [today's date]. Based on [country] FCV Country Risk Scan ([risk scan date]) and active portfolio as of [portfolio snapshot date]. This brief synthesizes open-source country risk reporting with internal project data. Portfolio exposure and mitigation options reflect stated project objectives and current implementation status; ground-truth verification and partner consultation required before activating contingencies. Not a formal World Bank portfolio rebalance or policy document."*

---

## Quality Checklist (self-review before returning)

- [ ] Country correctly linked between risk scan and portfolio scanner outputs
- [ ] All critical risks from risk scan assessed for portfolio impact (no missed risks)
- [ ] All vulnerable projects explicitly named with at least one project document hyperlink per project
- [ ] Vulnerability types clearly categorized (field access, counterpart capacity, etc.)
- [ ] Mitigations are specific and actionable, not generic
- [ ] Sector-level summaries clearly distinguish high, medium, and low exposure
- [ ] Output format matches user request (matrix + narrative / narrative only / sector-focused)
- [ ] Probability and severity clearly distinguished
- [ ] No confidential or supersensitive government data exposed
- [ ] Metadata note and caveats included
- [ ] All references to news and projects must have accurate hyperlinks to those sources
---

## AI Disclaimer

*This skill synthesizes country risk analysis with portfolio data to highlight plausible vulnerability pathways. It does not constitute a formal portfolio rebalancing recommendation or World Bank policy guidance. Risk-impact assessments depend heavily on implementation context and local partnership dynamics not captured in remote analysis. Always consult with Country Teams, Regional management, and Government partners before implementing contingencies or pausing projects. This output is for internal strategic dialogue and scenario planning only.*
