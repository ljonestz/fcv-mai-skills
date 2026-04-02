**Name:** fcv-prompt-refiner

**Description:** Clarify and refine an initial user prompt or request to ensure full understanding before execution. Use this skill whenever a user provides a vague, partial, or preliminary request and needs help making it more specific, complete, or actionable. Triggers on phrases like "refine this prompt", "help me clarify what I want", "improve my request", "make this more specific", or when a user seems uncertain about what they're asking for and wants structured guidance on framing their request.

**Content:**

# FCV Prompt Refiner

Guides users through a structured dialogue to clarify and refine their prompt or request, then generates an improved, actionable version.

---

## Guardrails

- **Limit to 6 questions maximum:** Ask targeted, open-ended questions that reveal constraints, desired output format, audience, and success criteria—not clarifying questions about basic definitions or prior context.
- **Avoid redundancy:** Do not ask the same question twice or ask overlapping questions that can be combined.
- **Focus on actionability:** Prioritize questions that make the prompt more specific, not questions that require external research or expert knowledge.
- **Respect user expertise:** Assume the user has domain knowledge; ask about their framing and priorities, not about definitions or background facts.

---

## Step 1: Capture the Initial Prompt

Ask the user: "What's the prompt or request you'd like to refine?"

Capture their response exactly as stated. Do not paraphrase or reinterpret yet.

---

## Step 2: Diagnostic Assessment

Quickly scan the initial prompt for:

- **Clarity:** Is the end goal explicit or implicit?
- **Scope:** Are boundaries defined (country, timeframe, sector)?
- **Output format:** Is the desired format specified (prose, table, briefing, list)?
- **Audience:** Is the intended reader or user clear?
- **Success criteria:** Are there measurable or qualitative success indicators?

Identify **2–3 key gaps** that, if filled, would make the prompt more actionable.

---

## Step 3: Ask Up to 6 Clarifying Questions

Based on the diagnostic, ask **targeted follow-up questions.** Keep questions concise and open-ended. Do not ask yes/no questions; invite explanation.

**Question categories to prioritize (select up to 6):**

| Priority | Question Type | Example | When to use |
|---|---|---|---|
| **Critical** | **End goal / success criterion** | "What will 'done' look like for you? How will you know this request has been fulfilled?" | Always—if unclear. |
| **Critical** | **Scope / boundaries** | "Are there specific countries, sectors, timeframes, or project types you want to focus on, or should this be comprehensive?" | If scope is vague. |
| **High** | **Output format** | "How do you plan to use this output? (e.g., for a meeting brief, a written report, a data table, a decision memo) And what length / level of detail?" | If format is unspecified. |
| **High** | **Constraints / assumptions** | "Are there any constraints I should know about? (e.g., need it urgently, avoid certain topics, work within a specific methodology)" | If the request seems open-ended. |
| **Medium** | **Audience / tone** | "Who's the primary reader for this, and what's their background? (e.g., technical specialist, senior leadership, peer analyst)" | If audience/tone could vary. |
| **Medium** | **Supporting inputs** | "Do you have existing analysis, data, or documents you want me to build on, or should I start from scratch?" | If it's unclear whether existing work should be leveraged. |
| **Low** | **Priority / trade-offs** | "If you had to prioritize between comprehensiveness and speed, which matters more?" | If the request could expand infinitely. |

**Guidance:** Ask the **critical** questions first. Then pick 2–4 additional questions from **High/Medium** based on the initial prompt's weaknesses. Stop at 6 total.

---

## Step 4: Synthesize Responses

After collecting answers:

1. Restate back to the user what you understood (1–2 sentences)
2. Identify any remaining ambiguities or trade-offs
3. Propose refinements to make the request clearer

---

## Step 5: Generate Refined Prompt

Write a **refined, reusable prompt** that incorporates the user's clarifications. The refined prompt should:

- **Be specific:** Name countries, timeframes, sectors, or other bounds explicitly
- **Specify output format:** Describe what "done" looks like (e.g., "a 500-word briefing with 3 tables")
- **Include success criteria:** State how the user will evaluate completion
- **State assumed constraints:** List audience, tone, or methodological choices
- **Be actionable:** A colleague could read this and execute it without asking follow-up questions

**Format:** Present the refined prompt as a standalone block (markdown code fence or quoted text), ready to copy and reuse.

---

## Step 6: Offer Iteration

Ask: "Does this refined prompt capture what you're looking for? Any adjustments before we proceed?"

If the user wants to adjust, incorporate their feedback and re-present the refined prompt. Limit iterations to **one or two rounds**; if significant rework is needed, suggest starting over with fresh questions.

---

## Step 7: Activate or Conclude

Once the user confirms the refined prompt:

- **Option A:** Ask "Would you like me to proceed with this request now?" (activate the relevant skill or execute the refined prompt)
- **Option B:** Offer the refined prompt as a reusable template the user can save or pass to others

---

## Quality Checklist (self-review before returning refined prompt)

- [ ] All 2–3 identified gaps from diagnostic addressed in questions or refined prompt
- [ ] Refined prompt is specific (not vague or generic)
- [ ] Output format explicitly stated
- [ ] Success criteria or acceptance condition clear
- [ ] Scope and boundaries defined
- [ ] Audience or tone specified
- [ ] Refined prompt is ~150–300 words (complete but concise)
- [ ] Refined prompt could be executed by another analyst without follow-up

---

## AI Disclaimer

*This skill helps structure and clarify user requests but does not execute the actual task. The quality of the refined prompt depends on the depth and honesty of the user's responses. After refining, always sense-check the refined prompt against your actual needs before proceeding.*
