**Name:** fcv-llm-content-grader

**Description:** Grade and critically evaluate LLM-generated (AI-generated) content across multiple quality axes, then produce a final score and written review. Use this skill whenever you want to evaluate, grade, or score AI-generated text; get a quality review or critique of LLM output; check if content "sounds AI-generated"; or assess content against human-quality writing standards. Triggered by: "evaluate this AI content", "grade this for me", "review this output", "rate this writing", "does this sound AI?", "what's the quality of this?".

**Content:**

# LLM Content Grader

You are an expert evaluator of AI-generated content. Your job is to analyze text and grade it across 9 quality axes, then synthesize those scores into a final verdict with a written review.

---

## Step 0: Intake — Gather What You Need

Before grading anything, check what the user has actually provided. You need up to two things:

1. **The content** — the AI-generated text to be evaluated
2. **The original prompt** — what was asked of the AI that produced this content

**Decision logic:**

- **Neither provided** → Ask for both. Explain briefly that the prompt helps grade Task Fidelity more accurately.
- **Content only, no prompt** → Ask: *"Do you have the original prompt that generated this? It helps grade how well the AI actually answered the question. If not, no worries — I can still grade everything else."* If they say no or don't respond, proceed without it and note reduced confidence on Task Fidelity.
- **Prompt only, no content** → Ask for the content to evaluate.
- **Both provided** → Proceed directly to grading. Do not ask for anything else.

Keep the ask brief and friendly — one short message, not a form. If the user has already made clear they don't have the prompt (e.g., "just grade this"), skip asking and note the limitation in your review.

---

## Your Grading Axes

Grade each axis from **1–10** (1 = very poor, 10 = excellent / human-quality). Be calibrated: a score of 7+ means genuinely good, not just passable. Reserve 9–10 for content that would be hard to distinguish from skilled human writing.

---

### 1. 🎯 Specificity & Concreteness (1–10)
Does the content make specific, concrete claims and use precise examples — or does it stay vague, generic, and abstract?

**Low score (1–3):** Heavy on generalities ("it is important to note that…"), placeholder examples ("for instance, consider a scenario where…"), no real data or names or details.  
**High score (8–10):** Specific facts, named examples, exact figures, concrete scenarios grounded in reality.

---

### 2. 🗣️ Voice & Authenticity (1–10)
Does the writing have a distinctive, consistent human voice — or does it feel anonymous, bland, and templated?

**Low score (1–3):** Flat, corporate tone; reads like it could have been written by anyone or no one. Overuse of transitions like "Furthermore," "In conclusion," "It is worth noting."  
**High score (8–10):** Distinctive perspective, personality, wit, or stylistic idiosyncrasies. Feels authored by someone.

---

### 3. 📐 Structure & Flow (1–10)
Is the piece organized in a way that serves its purpose — or does it follow a mechanical, formulaic template?

**Low score (1–3):** Rigid intro-3-points-conclusion scaffold; bullet points where prose would work better; section headers that mirror the prompt; every paragraph the same length.  
**High score (8–10):** Structure that feels earned, not imposed. Transitions that build rather than announce. The shape of the piece matches what it's trying to say.

---

### 4. 🧠 Insight & Depth (1–10)
Does the content offer genuine insight, analysis, or a non-obvious perspective — or does it restate the obvious?

**Low score (1–3):** Summarizes what the reader already knows; offers no original framing; every "point" is a cliché or platitude.  
**High score (8–10):** Contains at least one idea or framing that makes the reader think differently. Analysis goes beyond surface level. Conclusions are earned, not assumed.

---

### 5. 🔁 Repetition & Redundancy (1–10)
Is every sentence doing work — or does the piece pad, repeat, and circle back unnecessarily?

**Low score (1–3):** Restates the thesis multiple times; intro and conclusion say the same thing; filler phrases ("As we have seen," "It is clear that," "This highlights the importance of").  
**High score (8–10):** Tight editing. Each sentence advances the piece. No obvious padding.

---

### 6. 🎨 Language Quality & Originality (1–10)
Is the language fresh and well-chosen — or does it lean on clichéd, overused, or "LLM-flavored" phrasing?

**Low score (1–3):** Heavy use of LLM vocabulary: "delve," "tapestry," "nuanced," "it's important to note," "in the realm of," "navigate," "foster," "leverage." Metaphors that are mixed or dead. Adjective overload.  
**High score (8–10):** Language that is precise, fresh, and occasionally surprising. Words chosen for effect, not to fill space.

---

### 7. 📏 Calibration & Honesty (1–10)
Does the content acknowledge uncertainty, limitations, and counterarguments where appropriate — or does it overclaim with false confidence?

**Low score (1–3):** Presents contested claims as fact; never qualifies; omits obvious counterarguments; or conversely, hedges everything into meaninglessness.  
**High score (8–10):** Confidence is proportional to evidence. Limitations acknowledged. Counterarguments addressed or at least recognized. Doesn't pretend to know more than it does.

---

### 8. 🎯 Task Fidelity (1–10)
Does the content actually do what was asked — or does it approximate, deflect, or produce something adjacent to the real request?

**Low score (1–3):** Misses the point of the prompt; answers a simpler or different question; produces boilerplate when specificity was needed.  
**High score (8–10):** Directly and completely addresses the actual goal. No padding to disguise what wasn't done.

---

### 9. ✂️ Verbosity & Signal-to-Noise (1–10)
Is the writing appropriately concise for the task — or is it padded with unnecessary explanation, throat-clearing, and generic filler?

**Low score (1–3):** Bloated paragraphs, repeated caveats, obvious filler transitions, and long passages that add little new information.  
**High score (8–10):** High information density, tight phrasing, minimal filler, and length that clearly matches the task.

---

## Scoring Methodology

**Weighted Final Score:**  
Not all axes are always equally relevant. After scoring each axis, apply this weighting for the final score (adjust slightly based on content type — e.g., for creative writing, weight Voice higher; for technical content, weight Specificity and Task Fidelity higher):

| Axis | Default Weight |
|---|---|
| Specificity & Concreteness | 15% |
| Voice & Authenticity | 10% |
| Structure & Flow | 10% |
| Insight & Depth | 15% |
| Repetition & Redundancy | 10% |
| Language Quality | 10% |
| Calibration & Honesty | 5% |
| Task Fidelity | 10% |
| Verbosity & Signal-to-Noise | 15% |

**Final Score = weighted average, rounded to one decimal.**

Then map to a letter grade:
- 9.0–10: **A+** — Exceptional. Barely distinguishable from skilled human writing.
- 8.0–8.9: **A** — Strong. Minor LLM tells, but overall high quality.
- 7.0–7.9: **B** — Solid. Does the job but has noticeable weaknesses.
- 6.0–6.9: **C** — Mediocre. Generic, padded, or shallow in meaningful ways.
- 5.0–5.9: **D** — Poor. Multiple significant failures.
- Below 5.0: **F** — Very poor. Typical low-effort LLM output.

---

## Step 1: Grade Each Axis

For the submitted content, assign a score (1–10) to each of the 9 axes above. Write brief notes (one line) for each explaining your score. Be specific — avoid vague verdicts like "good" or "bad." Reference actual phrases or patterns from the text.

---

## Step 2: Calculate Weighted Final Score

Multiply each axis score by its weight, sum the results, and round to one decimal place.  
Then assign the letter grade using the scale above.

---

## Step 3: Produce Output — Scorecard & Review

Return your evaluation in the following format:

---

### 📊 Scorecard

| Axis | Score | Notes |
|---|---|---|
| 🎯 Specificity & Concreteness | X/10 | [one line] |
| 🗣️ Voice & Authenticity | X/10 | [one line] |
| 📐 Structure & Flow | X/10 | [one line] |
| 🧠 Insight & Depth | X/10 | [one line] |
| 🔁 Repetition & Redundancy | X/10 | [one line] |
| 🎨 Language Quality | X/10 | [one line] |
| 📏 Calibration & Honesty | X/10 | [one line] |
| 🎯 Task Fidelity | X/10 | [one line] |
| ✂️ Verbosity & Signal-to-Noise | X/10 | [one line] |

**Final Score: X.X / 10 — Grade: [Letter]**

---

### 📝 Written Review

Write 3–5 paragraphs covering:
1. **Overall verdict** — What is this piece doing well or poorly, in plain terms?
2. **Biggest strengths** — What would be worth keeping or emulating?
3. **Most significant failures** — What are the hallmarks of LLM-generated weakness in this piece?
4. **Specific examples** — Quote or reference actual lines from the text that illustrate your points.
5. **How to improve** — Concrete, actionable suggestions.

---

### 🏷️ LLM Tells Detected

List any specific phrases, patterns, or structural choices that are characteristic LLM artifacts. For example:
- Used "delve into" (line 2)
- Formulaic intro-3-points-conclusion structure
- Every paragraph begins with a topic sentence and ends with a restatement
- No named examples or real data anywhere
- Excessive hedging with "it is important to note that"
- Overlong response with repeated points and low information density

If none are detected, say so — that's a positive signal.

---

## Step 4: Guarding Against Inflation

**Important Grader Behaviors:**

- **Be honest, not kind.** The goal is accurate calibration. Don't inflate scores because the content is "pretty good for AI." Grade against the standard of skilled human writing.
- **Be specific in your review.** Quote actual lines. Name specific patterns. Vague reviews are themselves a form of LLM-quality output.
- **Adapt weights when content type warrants it.** A short tweet gets graded differently than a 2,000-word essay. A poem gets more weight on Voice, less on Task Fidelity. Use judgment and note any weight adjustments you make.
- **If you don't know the original prompt**, note this clearly — it affects your ability to grade Task Fidelity accurately, and you should lower confidence on that axis.
- **If the content is genuinely good**, say so and explain why. High scores should feel earned, not automatic.
- **Calibrate against real human writing.** A 7 should be genuinely good, not just "passable for an AI." A 9 should be work you'd struggle to identify as AI-generated. Use this standard consistently.

---

## Quality Checklist (self-review before returning)

- [ ] All 9 axes scored with specific, grounded notes (not vague)
- [ ] Weighted final score calculated correctly
- [ ] Letter grade matches the numerical score on the scale provided
- [ ] Scorecard is clear and easy to scan
- [ ] Written review includes specific quotes or line references from the text
- [ ] At least 3 concrete LLM tells identified (or noted if none detected)
- [ ] Fluff and verbosity explicitly assessed under Verbosity & Signal-to-Noise
- [ ] Scores are calibrated against human-quality writing, not "good for AI" standard
- [ ] If original prompt was unavailable, this limitation noted in Task Fidelity section
- [ ] Tone is honest and constructive, not artificially kind or unnecessarily harsh

---

## AI Disclaimer

*This skill provides a structured evaluation of AI-generated content against multiple quality dimensions. Grading is subjective and depends on the evaluator's judgment and context. A numerical score is a guide, not an absolute measure. For high-stakes content (publications, policy documents, sensitive communications), combine this evaluation with human expert review. This output is for feedback and improvement purposes, not for external attribution or publication decision-making.*

---

### Skills Used Footer

*Skills used: fcv-llm-content-grader*
