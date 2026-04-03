**Name:** fcv-skills-overview

**Description:** Presents an overview of all available FCV skills and helps the user choose which one to launch. Triggered by: "what FCV skills do I have", "FCV skills overview", "show me FCV tools", "FCV skills", or any request for a list of FCV capabilities.

**Content:**

## FCV Skills Overview

This skill is the navigation hub for the FCV toolkit. Present the available skills and help the user launch the one they need.

### Step 1 — Present the Skills

Display this table:

| # | Skill | When to Use |
|---|---|---|
| 1 | FCV Project Screener | A TTL has sent you a PAD, PCN, or concept note to screen for FCV sensitivity and responsiveness — produces thematic analysis, Do No Harm synthesis, ratings, and structured action cards |
| 2 | RRA Section Drafter | You are writing or updating an RRA and need a structured draft for a specific section |
| 3 | CPF FCV Peer Reviewer | You have been asked to peer review a CPF package ahead of Board or a country team review |
| 4 | ISR Portfolio Scanner | You want an FCV health check across your country portfolio or a single project's ISR history |
| 5 | FCV Risk Briefing Generator | You need to brief the CMU or management on how FCV risks could affect the country portfolio |
| 6 | Lessons Learned Extractor | A TTL or mission team asks what has worked in similar FCV contexts |
| 7 | FCV Lens Note Drafter | A new TTL needs FCV framing for their sector, or you are preparing for a sector dialogue or mission |
| 8 | FCV Trusted Source Analyst | You want to check whether a document's claims hold up against trusted sources, or you need a fresh evidence summary |
| 9 | RRA Mini Update | The country RRA is more than 12-18 months old and you need an update — extracts baseline, researches developments, confirms themes with you, then drafts an analytical update note |
| 10 | Country Risk Scan | You need a structured FCV country briefing covering institutional fragility, conflict dynamics, displacement, and govt-development relations for a specific country |
| 11 | Country Portfolio Scanner | You want a sector-organized overview of a country's active World Bank projects with FCV flags, funding, and document links |
| 12 | Portfolio Risk Impact Assessment | You need to understand how identified country risks threaten specific projects in the portfolio — combines risk scan + portfolio scanner |
| 13 | Prompt Refiner | Your request is vague or preliminary and you want structured help clarifying and refining it before executing a skill |
| 14 | Citation Checker | You need to verify citations, catch hallucinated sources, or flag unsourced factual claims in a draft briefing, note, or report |

### Step 2 — Prompt the User

After the table, say:

"Pick a number to launch that skill, or ask me to tell you more about any of them. You can also just describe what you need and I'll suggest the best skill."

### Step 3 — Handle the Response

- **If the user picks a number:** Load and execute the corresponding skill immediately.
- **If the user asks for more detail on a skill:** Provide a 3-4 sentence description covering: what it does, what inputs it needs, and what output it produces. Then ask: "Would you like to launch this skill?"
- **If the user describes a task without picking a number:** Recommend the most appropriate skill based on their description, explain why, and ask if they'd like to proceed.
- **If the input is unclear:** Restate the options in plain language and ask again. Do not use coded inputs — keep everything conversational.
