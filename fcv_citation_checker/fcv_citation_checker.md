**Name:** fcv-citation-checker

**Description:** Verify citations, catch hallucinated sources, and flag unsourced claims in any written document. Use this skill whenever a user asks to fact-check a document, verify citations, check for hallucinations, audit sources, or review a briefing or report for accuracy. Triggered by phrases like "check my citations", "are these sources real?", "fact-check this", "verify the links", "flag hallucinations", or "audit this briefing".

**Content:**

# FCV Citation Checker

Audits a document for citation accuracy and unsourced factual claims. Returns an **annotated version** of the original text with inline flags. Designed primarily for FCV briefings and policy documents, but works on any sourced writing.

---

## Flag Legend

| Flag | Meaning |
|------|---------|
| ✅ | **Verified** — Claim matches the linked source; URL live and accessible |
| ⚠️ | **Unverifiable** — URL inaccessible or behind paywall; claim plausible but cannot confirm |
| 🔶 | **Misrepresented** — Source exists and is live, but the claim distorts, overstates, or misattributes what it actually says |
| ❌ | **Hallucinated / Dead** — URL returns 404, source doesn't exist, or claim is directly contradicted by the source |
| 📌 | **Unsourced claim** — Specific factual assertion (statistic, event, attribution) with no citation that likely needs one |

---

## Guardrails

- **Verify the exact claim, not just the source:** Mark a citation as verified only if the linked or cited source supports the specific statement it appears to substantiate.
- **Treat non-specific or wrong destination links as citation problems:** A live link to a generic homepage or broad site section (for example, `crisisgroup.org`) is not sufficient when the claim requires a specific report/page.
- **Preserve the user's text:** Do not rewrite, paraphrase, or clean up the original document. Only insert flags and brief explanatory notes inline.
- **Separate inaccessible from fabricated:** Use **Unverifiable** for plausible but inaccessible sources; reserve **Hallucinated / Dead** for fabricated, malformed, dead, or clearly contradictory citations.
- **Flag concrete factual assertions:** Mark unsourced claims when they involve statistics, dates, named events, attributed statements, or other checkable facts. Do not over-flag general framing or analytical judgment.
- **Work in scoped chunks if needed:** If the document is too long to check reliably in one pass, propose section-by-section review rather than rushing or skipping items.

---

## Step 1: Intake

Ask the user to paste or upload the document. If they have already provided it, proceed directly.

Confirm:
- **Document type** (briefing, report, article, note, slide text, etc.) — this affects what counts as a claim that needs a citation.
- **Scope** — full document, or a specific section.

If the user wants only a subset checked, note it clearly in the output header.

---

## Step 2: Parse the Document

Systematically identify every:

1. **Inline hyperlink** — extract the anchor text, the URL, and the specific claim it is meant to support.
2. **Footnote or endnote citation** — extract reference details and the claim.
3. **Unsourced factual claim** — any specific statistic, event date, casualty figure, named actor's action, or attributed quote that carries no citation.

Build an internal checklist before verifying anything. Do not start verification until you have catalogued all items.

---

## Step 3: Verify Each Citation

For every citation, follow this decision tree in order:

### 3a. Fetch the URL or source

- Attempt to retrieve the linked page or cited source using available search and document tools.
- If live and accessible, read enough to verify the specific claim.
- If 404 or domain error, mark ❌ Dead link.
- If paywalled, login-gated, or otherwise inaccessible, mark ⚠️ Unverifiable and note the publisher or source type.

### 3b. Check claim accuracy

If the page or source loaded:
- Does the source actually support the specific claim made? Mark ✅ Verified.
- Does the source exist but say something materially different, weaker, or unrelated? Mark 🔶 Misrepresented and note the discrepancy in one sentence.
- Is the link live but too generic to locate the cited evidence (for example, a homepage, topic hub, or wrong page)? Mark 🔶 Misrepresented and note that a direct source link is required.
- Is the source absent or does it contradict the claim? Mark ❌ Hallucinated.

### 3c. Fallback to reasoning if retrieval fails or is inconclusive

- If the source appears to come from a well-known, verifiable institution (for example, UNHCR, World Bank, Reuters) and the URL pattern looks plausible, use ⚠️ Unverifiable rather than ❌.
- If the URL is malformed, the publisher is implausible, or the claim is highly specific in a suspicious way, use ❌ likely hallucinated and note the reasoning briefly.

### 3d. Unsourced claims

For each 📌 item, note:
- What type of source would normally be expected (for example, "UN OCHA situation report", "national statistics office", or "Reuters reporting").
- Whether you can identify a plausible source via search. If so, suggest it briefly.

---

## Step 4: Produce Annotated Output

Start the response with the **Flag Legend** (same five symbols and definitions) so users can interpret inline flags before reading the annotated document.

Next, return the **full original text**, with flags inserted **immediately after** each claim or citation they apply to.


### Formatting rules

- Insert flags inline using this pattern: `[✅]`, `[⚠️]`, `[🔶]`, `[❌]`, `[📌]`.
- After the flag, add a **brief parenthetical note** in italics explaining the verdict. Keep it to one sentence.
- Do not rewrite the original text; only insert flags and notes.
- Preserve all original formatting, including headings, bold text, tables, and paragraph breaks.

### Example inline annotation

> Displacement has surged to 3.2 million IDPs as of February 2025, according to [IDMC](https://www.internal-displacement.org/countries/nigeria) [✅] *(Source confirmed: IDMC Nigeria profile matches figure and date.)* Security forces have conducted over 400 operations since January [❌] *(Link returns 404; claim unverifiable from any accessible source.)* The government has rejected international monitoring mechanisms [📌] *(No citation; consider linking to a UN OHCHR or ICG report.)*

---

## Step 5: Summary Block

After the annotated document, append a **Citation Audit Summary**:

```text
## Citation Audit Summary

- ✅ Verified: N
- ⚠️ Unverifiable: N
- 🔶 Misrepresented: N
- ❌ Hallucinated / Dead: N
- 📌 Unsourced claims flagged: N

**Overall reliability:** [High / Medium / Low / Critical concerns]
**Key issues:** [1-3 sentence plain-language summary of the most important problems found]
```

Use this reliability scale:
- **High** — All or nearly all citations verified; 1 or fewer minor issues.
- **Medium** — Some unverifiable links; no outright hallucinations; a few unsourced claims.
- **Low** — Multiple misrepresented or unverifiable citations; several unsourced claims.
- **Critical concerns** — One or more hallucinated sources or fabricated statistics detected.

---

## Quality Checklist (self-review before returning)

- [ ] Every hyperlink in the original document has been checked
- [ ] Every unsourced factual claim (statistic, event, attribution) has been flagged 📌
- [ ] Flags are inserted inline immediately after the relevant text
- [ ] Each flag has a one-sentence parenthetical explanation
- [ ] Original text is otherwise unchanged
- [ ] Summary block is present and accurate
- [ ] No flag has been left as "pending" — every item resolved to one of the five categories

---

## AI Disclaimer

*This skill provides a structured citation and sourcing audit, but citation verification remains constrained by link accessibility, search coverage, and the quality of the underlying document. Treat any flagged issues as a review aid, not as a substitute for subject-matter validation or formal clearance. Always verify consequential factual corrections against primary sources before external or operational use.*

---

### Skills Used Footer

After the AI Disclaimer, append an italicised footer listing the primary skill and any other FCV skills referenced or recommended in the output:

*Skills used: fcv-citation-checker | Also referenced: [list any other fcv- skills mentioned in the output]*

If no other FCV skills were referenced, use: *Skills used: fcv-citation-checker*