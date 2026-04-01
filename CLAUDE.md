# CLAUDE.md — FCV Skills Project

Project-level instructions for the FCV mAI Skills package. These supplement (and where they conflict, override) the global `~/.claude/CLAUDE.md`.

---

## Project Overview

This directory contains a package of **11 mAI skills** for the World Bank FCV Group, designed to support FCV Country Coordinators and specialist staff in recurring analytical, review, and advisory workflows.

**Platform:** ai.worldbank.org/mai (mAI) — skills are plain-text markdown files with Name, Description, and Content fields.
**Users:** FCV Country Coordinators — domain experts, low-LLM-skill users. Skills must be self-explanatory with guided entry.
**Word limit:** ~2,000–3,000 words per skill (soft ceiling; do not pad to hit it).

---

## mAI Platform Constraints

**Platform:** mAI (ai.worldbank.org/mai) — skills are plain-text instruction sets, not plugins. They cannot connect to external systems or execute code.

### Skill Structure
Each skill has exactly three fields:
- **Name:** kebab-case, 2–4 words (e.g., `fcv-project-screener`)
- **Description:** 1–3 sentences — this is the trigger mAI reads to decide whether to activate the skill. Must include example trigger phrases. Too broad = false fires; too narrow = misses.
- **Content:** Plain text / markdown workflow instructions. Target under ~2,000–3,000 words. Longer skills are stored but may be unreliable in a single context window.

### What Skills Can Do
- Define structured multi-step workflows
- Specify output format (prose, tables, markdown, bullets)
- Instruct mAI to use its built-in tools: internal document search, people search, project search, web search, image generation, document creation
- Set tone, depth, and communication style
- Handle branching logic in natural language ("if X is missing, ask the user before proceeding")

### What Skills Cannot Do
- Grant access to new tools, APIs, or external systems
- Execute code or scripts
- Override mAI's security, ethics, or data policies
- Store state between conversations (skills reload fresh each time)
- Be triggered programmatically — activation is always a semantic match on the user's message

### Good vs Poor Skill Candidates
**Good:** Recurring workflows with consistent structure; complex enough that re-explaining every session is tedious; clear repeatable output format; analytical pipelines chaining mAI's built-in search/document tools.

**Poor:** One-off tasks tied to a single document; tasks mAI handles well by default; workflows requiring code execution or external integrations; vague workflows that can't be expressed as concrete steps.

---

## Directory Structure

```
fcv_<skill_name>/          — One folder per skill, contains <skill_name>.md
fcv_skills_combined/       — fcv_all_skills_upload_package.md (combined upload-ready file)
fcv_skills_overview/       — Navigation hub skill
fcv_isr_portfolio_scanner/ — FCV_Analytics_Page.md (ISR Portfolio Scanner)
fcv_ai_disclaimer/         — Standalone disclaimer skill
docs/specs/                — Design spec and implementation plan
Reference Documents/       — RRA methodology, OST Manual, FCV Playbook, etc.
mAI Skills/                — Platform documentation
```

---

## The 11 Skills

| # | Skill ID | File location |
|---|---|---|
| 1 | fcv-project-screener | `fcv_project_screener/fcv_project_screener.md` |
| 2 | fcv-rra-section-drafter | `fcv_rra_section_drafter/fcv_rra_section_drafter.md` |
| 3 | fcv-cpf-peer-reviewer | `fcv_cpf_peer_reviewer/` |
| 4 | fcv-isr-portfolio-screener | `fcv_isr_portfolio_scanner/FCV_Analytics_Page.md` |
| 5 | fcv-risk-briefing-generator | `fcv_risk_briefing_generator/fcv_risk_briefing_generator.md` |
| 6 | fcv-lessons-learned-extractor | `fcv_lessons_learned_extractor/fcv_lessons_learned_extractor.md` |
| 7 | fcv-lens-note-drafter | `fcv_lens_note_drafter/fcv_lens_note_drafter.md` |
| 8 | fcv-trusted-source-analyst | `fcv_trusted_source_analyst/fcv_trusted_source_analyst.md` |
| 9 | fcv-rra-mini-update | `fcv_rra_mini_update/fcv_rra_mini_update.md` |
| 10 | fcv-skills-overview | `fcv_skills_overview/fcv_skills_overview.md` |
| 11 | fcv-ai-disclaimer | `fcv_ai_disclaimer/` |

**Retired:** `fcv-isr-flag-reviewer` — replaced by `fcv-isr-portfolio-screener` (2026-03-31).

---

## Skill File Format

Every skill file must have exactly these three fields at the top:

```
**Name:** fcv-<skill-id>

**Description:** <one-sentence trigger description — this is what mAI uses for skill matching>

**Content:**
<skill body>
```

Every analytical skill must include:
- **Guardrails block** (anti-hallucination rules) near the top of Content
- **AI Disclaimer** block verbatim at the end of all output

---

## Combined Upload Package

`fcv_skills_combined/fcv_all_skills_upload_package.md` is the single file used to upload/refresh all 11 skills on the mAI platform. **It must be kept in sync with individual skill files.** Whenever a skill is edited, update both the individual file and the combined package.

---

## Key Conventions

- **Do not add JavaScript, APIs, or tooling** — skills are prompts only, no code execution
- **Cite sources inline** — `[Source Name, Date]` format throughout; never rely on bibliography alone
- **Guided entry pattern** — every skill asks the user for inputs before proceeding; do not assume context
- **Pause points** — multi-stage skills pause after each stage for user confirmation
- **FCV Refresh shifts** — where relevant, reference Shift A (Anticipate), B (Differentiate), C (Jobs & Private Sector), D (Enhanced Toolkit) from the January 2026 FCV Strategy update

---

## Amendment History

| Date | Change |
|---|---|
| 2026-03-31 | Initial build: 11 skills written and quality-checked |
| 2026-03-31 | mAI reviewer amendments: 8 skills updated (Quick Flag mode, fallback RRA table, Mixed label, FCV lens instruction, thematic briefing option, extended source list, optional upload, coordinator scenario language in overview). ISR Flag Reviewer replaced by ISR Portfolio Scanner. |
| 2026-04-01 | Pre-rollout refinements: Project Screener restructured (strict S/R/S+R definitions, dynamic analytical themes replacing fixed OST table, structured action cards for Stage 3, word caps 800-1000w/1200-1500w, 6-point rating scale); RRA Mini Update check-in step added (Step 3.5) and Step 2 pause strengthened; AI disclaimer scoped to final outputs only across all skills; Skills Used footer added to all 9 analytical skills; RRA Mini Update, Risk Briefing Generator, and FCV Lens Note Drafter moved from Tier 2 to Tier 1 (Tier 1 now 6 skills; Tier 2 now 3: ISR Portfolio Scanner, Lessons Learned Extractor, Trusted Source Analyst). |

**Future skills flagged (not yet built):** Country Engagement Brief, Do No Harm Standalone, PRA Eligibility Advisory.

---

## Output Rules for This Project

- All outputs (edited skill files, new skill files) go in the relevant skill subfolder or `fcv_skills_combined/`
- Do NOT save to `Claude_Outputs/` — this is not a code project but files live in the project directory
- Use the existing file naming pattern: `fcv_<skill_name>.md`
- Never overwrite without the user explicitly asking to update/replace
