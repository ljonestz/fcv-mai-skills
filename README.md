# FCV mAI Skills Package

A set of **18 AI-assisted workflow skills** for the **FCV (Fragility, Conflict & Violence) Group**, built for the [mAI platform](https://ai.worldbank.org/mai). Skills support FCV Country Coordinators and specialist staff in recurring analytical, review, and advisory tasks.

---

## Skill Roster

| # | Skill ID | Description |
|---|---|---|
| 1 | `fcv-project-screener` | Screen project documents for FCV sensitivity and responsiveness |
| 2 | `fcv-rra-section-drafter` | Draft sections of a Rapid Risk Assessment (RRA) |
| 3 | `fcv-cpf-peer-reviewer` | Peer-review CPF documents for FCV alignment |
| 4 | `fcv-isr-portfolio-screener` | Scan ISR portfolios for FCV flags and patterns |
| 5 | `fcv-risk-briefing-generator` | Generate country-level FCV risk briefings |
| 6 | `fcv-lessons-learned-extractor` | Extract lessons learned from project documents |
| 7 | `fcv-lens-note-drafter` | Draft FCV Lens Notes for project teams |
| 8 | `fcv-trusted-source-analyst` | Analyse trusted sources for FCV context |
| 9 | `fcv-rra-mini-update` | Generate mini-updates to existing RRAs |
| 10 | `fcv-country-risk-scan` | Generate structured FCV country risk briefings |
| 11 | `fcv-country-portfolio-scanner` | Scan active projects and group by sector with FCV flags |
| 12 | `fcv-portfolio-risk-impact-assessment` | Cross-analyze country risks with portfolio to assess project vulnerability |
| 13 | `fcv-prompt-refiner` | Clarify and refine user requests before execution |
| 14 | `fcv-citation-checker` | Verify citations, catch hallucinated sources, and flag unsourced claims in written documents |
| 15 | `fcv-citation-verifier` | Verify that citations are accurate by re-retrieving sources in RRA drafts and other FCV documents |
| 16 | `fcv-llm-content-grader` | Grade and evaluate AI-generated content across multiple quality axes with detailed scoring and review |
| 17 | `fcv-ai-disclaimer` | Append the standard FCV AI-generated output disclaimer to final, externally-facing outputs |
| 18 | `fcv-skills-overview` | Navigate the complete FCV skills package and select the right tool for your task |

**Utility:** Skills Overview, AI Disclaimer, Prompt Refiner, LLM Content Grader

**Tier 1 (core, high-frequency):** Project Screener, RRA Section Drafter, CPF Peer Reviewer, Risk Briefing Generator, FCV Lens Note Drafter, RRA Mini Update, Country Risk Scan

**Tier 2 (specialist, recurrent):** ISR Portfolio Screener, Lessons Learned Extractor, Trusted Source Analyst, Country Portfolio Scanner, Portfolio Risk Impact Assessment, Citation Checker, Citation Verifier

---

## Repository Structure

```
fcv_<skill_name>/          — One folder per skill, contains the skill .md file
fcv_skills_combined/       — Combined upload-ready package (all skills in one file)
fcv-skills-map.html        — Interactive navigation reference for the skills package
CLAUDE.md                  — Project-level instructions for Claude Code sessions
```

---

## How to Upload / Refresh Skills on mAI

The **combined upload package** is the single file used to load or refresh all skills on the mAI platform:

```
fcv_skills_combined/fcv_all_skills_upload_package.md
```

Upload this file to mAI to install or update the full skill set in one step.

To update a single skill, edit both the individual skill file (e.g. `fcv_project_screener/fcv_project_screener.md`) **and** the combined package — they must stay in sync.

---

## Navigation Reference

Open `fcv-skills-map.html` in a browser for an interactive map of the skills package, including tier classification, trigger examples, and skill dependencies.

---

## Skill File Format

Every skill file follows this structure:

```
**Name:** fcv-<skill-id>

**Description:** <trigger description — 1–3 sentences with example phrases>

**Content:**
<workflow instructions>
```

---

## Amendment History

| Date | Change |
|---|---|
| 2026-03-31 | Initial build: 11 skills written and quality-checked |
| 2026-03-31 | mAI reviewer amendments applied to 8 skills |
| 2026-04-01 | Four new skills added: Country Risk Scan, Country Portfolio Scanner, Portfolio Risk Impact Assessment, Prompt Refiner. Updated tier structure. |
| 2026-04-02 | Added Citation Checker as Tier 2 specialist skill. Total package: 16 skills. |
| 2026-04-07 | Citation integrity overhaul: added Citation Verifier skill. Total package: 17 skills. |
| 2026-04-13 | Added LLM Content Grader utility skill for evaluating AI-generated content. Total package now 18 skills. Updated hyperlink and document-link requirements across multiple skills. |

**Retired:** `fcv-isr-flag-reviewer` — replaced by `fcv-isr-portfolio-screener` (2026-03-31).

**Future skills flagged (not yet built):** Country Engagement Brief, Do No Harm Standalone, PRA Eligibility Advisory.

---
