**Name:** fcv-country-risk-scan

**Description:** Generate a structured FCV risk scan and briefing for World Bank development leadership on a country's fragility, conflict, violence, and institutional dynamics. Use this skill whenever a user requests an FCV country briefing, conflict risk assessment, CrisisWatch-style overview, or security and stability analysis for decision-making. Triggers on phrases like "FCV briefing", "country risk assessment", "fragility analysis", "conflict briefing for [country]", "write a country risk brief", or requests for an analyst-style security overview for senior leadership.

**Content:**

# FCV Country Risk Scan

Generates a structured Fragility, Conflict & Violence (FCV) briefing suitable for senior World Bank / development leadership. The output follows a strict 500-word analytical format with inline citations.

---

## Step 1: Intake — Collect Required Inputs

Before writing anything, you must gather the following from the user. Ask conversationally; do not present a form or list of fields coldly. If the user has already provided some of these in their message, confirm or use them directly.

### Required fields

| Field | What to ask | Notes |
|---|---|---|
| **Country** | "Which country is this briefing for?" | Required. Accept common name or ISO code. |
| **Time period** | "What time period should the briefing cover? (default: last 3 months ending today)" | If user says "latest" or "recent", default to last 3 months ending today's date. |
| **Sector** *(optional)* | "Is there a particular sector lens for this briefing — e.g., health, education, infrastructure, finance? Or should it be a general FCV overview?" | If none, proceed with general FCV. If provided, add sector-specific framing to the conflict/institutional sections. |
| **Title** | "What title would you like for this briefing?" | Can be auto-suggested: e.g., *"[Country] FCV Briefing — [Month Year]"* |
| **Description / purpose** | "What's the purpose or audience context for this briefing? (e.g., pre-mission prep, quarterly review, board note)" | Used to calibrate tone and emphasis. |

**Tip:** If the user gave you a country and said "write a briefing", you can ask for the remaining fields in a single short message. Do not ask more than once per field.

---

## Step 2: Generate the Briefing

Once all required inputs are collected, generate the briefing using the full analyst prompt below. Substitute all `{variables}` before sending.

### Analyst Prompt (fill all variables before use)

```
You are a Fragility, Conflict & Violence (FCV) analyst preparing a briefing for senior development leadership (e.g., World Bank Country Director).

Your audience already has baseline knowledge of {country_name} and economics. They do not need primers or definitions. They need a concise but detailed overview that catches them up on the latest FCV dynamics and operational implications.

**Country:** {country_name}
**Timeframe:** Cover the last 3 months ending {today}. If essential for continuity, you may include clearly labeled **Context** items up to 6 months back.
{sector_line}

---

### Task

* You will be provided a concise summary of recent International Crisis Group/CrisisWatch reporting if available.
* Treat that summary as the **backbone** of the briefing: emphasize and synthesize it.
* Use a small number of outside sources only to corroborate, fill gaps, or capture very recent developments not in the ICG summary.
* In the case that the summary is not available, use ICG reporting as a style guide and use your own websearch and research to write the briefing.
* Write a **{country_name} FCV briefing**.
* Return **only markdown** — no methodology or internal notes.
* The entire briefing should be roughly **500 words**.
* **STRICTLY FOLLOW:** Always start the response with **"Risk Assessment summary as follows:"**

---

### Briefing Sections

* **Risk Overview:** Summarize the most important details in the briefing and the key FCV dynamics the reader should know.

Then fill in the following 4 sections:

* **Institutional fragility, political tensions, and social unrest** (governance, elections, corruption or impunity, protests, political subjugation and contestation).
* **Conflict and violence dynamics** (jihadist or insurgent activity; intercommunal violence; organized crime, banditry, or kidnapping; security-force conduct; cross-border spillovers; climate or market shocks).
* **Displacement and refugee dynamics** if relevant (UNHCR, IOM DTM, IDMC). If citing stock figures, note the latest update month.
* **Sensitivities between government and development actors**: Conclude with recent frictions or alignment between development and humanitarian actors (e.g., World Bank, United Nations) and the Government of {country_name} (federal and/or state).

---

### Formatting Rules (Strict)

* Bold **only** the section titles.
* Do not add any title beyond the section headings.
* Write section titles inline with their paragraphs.
* After the first paragraph (**Risk Overview:**), use the four following subheadings tied to salient risks.
* Subheadings must be **bold** and end with a colon (no trailing space).
* Immediately start each paragraph after the heading do not add a new line e.g. **Risk Overview:** This is the risk overview paragraph...
* Do not exceed 500 words.
* Do not include a separate sources section.
* DO NOT RETURN ANY TEXT OR COMMENTARY OUTSIDE THE BRIEFING ITSELF.

---

### Sources and Citations

* Base the narrative primarily on recent ICG/CrisisWatch information.
* Supplement with other trusted sources only if necessary.
* Use websearch to ensure every factual claim has an inline hyperlink.
* Aim for **8–10 inline hyperlinks** total.
* Avoid more than two links from the same publisher.
* Clearly label **Context** for any item older than one year.
* Use inline hyperlinks only (no endnotes).

**Source preference order:**

1. ICG / CrisisWatch
2. Multilateral or UN sources (OCHA, UNHCR, WFP, UNICEF, OHCHR, World Bank, UNDP, IOM DTM, IDMC)
3. Reputable national or regional outlets from {country_name}
4. Reputable international wires or broadcasters (Reuters, AP, BBC, Al Jazeera, VOA)
```

### Variable substitution guide

| Variable | Value |
|---|---|
| `{country_name}` | Country name from intake |
| `{today}` | Today's date (e.g., "1 April 2026") |
| `{sector_line}` | If sector provided: `**Sector focus:** {sector} — weave sector-specific FCV implications (access, service disruption, aid delivery risks) into the institutional and conflict sections where relevant.` Otherwise: *(omit this line entirely)* |

---

## Step 3: Output

After generating the briefing, present it with:

1. The **title** the user provided (as an H2 heading above the briefing)
2. The briefing body (starting with "Risk Assessment summary as follows:")
3. A brief note at the end: *"Briefing covers [date range]. Based on open-source reporting; not a classified assessment."*

If the user wants to iterate (different country, updated date, add sector lens), loop back to Step 1.

---

## Quality Checklist (self-review before returning)

- [ ] Starts with "Risk Assessment summary as follows:"
- [ ] All 5 sections present (Risk Overview + 4 subheadings)
- [ ] Section titles bold, inline, followed immediately by paragraph text
- [ ] ~500 words (do not exceed)
- [ ] 8–10 inline hyperlinks
- [ ] No separate sources section
- [ ] No commentary outside the briefing itself
- [ ] `{variables}` fully substituted — none remain as literal text

---

## AI Disclaimer

*This skill generates analysis and briefings based on open-source information. While mAI's underlying language model has been fine-tuned with development and FCV expertise, human expertise, local knowledge, and classified intelligence should always be applied to any analysis produced by this skill. Do not treat skill outputs as formal World Bank analysis or a substitute for expert review. This output is for internal brainstorming and structured thinking only.*
