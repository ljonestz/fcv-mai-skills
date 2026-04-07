**Name:** fcv-citation-verifier

**Description:** Verifies citations in an RRA draft or any FCV document by re-retrieving each source and checking it matches the claim made. Designed to run after fcv-rra-section-drafter. Triggered by: "check the citations in this RRA draft", "verify citations", "citation check", "check my sources", "verify the references", "are these citations real", or any request to verify sources in a draft.

**Content:**

## FCV Citation Verifier

Mechanically verifies citations in a document by re-retrieving each cited source and comparing it against the claim made. Returns a revised draft with failed citations corrected and a verification summary.

Designed as a companion to the RRA Section Drafter, but works on any sourced FCV document.

---

### Guardrails

- **Re-retrieve, don't guess.** For every citation you check, search for the exact source (title + author + year). Do not rely on your own knowledge to confirm or deny a citation — search for it.
- **Do not fabricate verification results.** If you cannot find a source after searching, classify it as Unverified. Do not claim it is verified or fabricated based on reasoning alone.
- **Do not add new citations.** Your job is to check existing citations, not to introduce new sources.
- **Do not rewrite beyond affected passages.** When a citation fails, rewrite only the sentence or clause that referenced it. Do not restructure paragraphs or alter analytical conclusions.
- **Preserve the analytical point.** When removing a failed citation, keep the underlying argument as uncited analytical narrative wherever the point is analytically sound. Change the attribution, not the substance.

---

### Step 1 — Intake

Ask the user to paste or upload the document. If they have already provided it, proceed directly.

Scan the document for:
- All inline citations (Chicago author-date format)
- The references table (if present)
- Citation tags: `[User-Provided]`, `[Model-Sourced: Internal]`, `[Model-Sourced: External]`

**If tags are present** (output from fcv-rra-section-drafter):
- **Skip** all `[User-Provided]` citations — these are authoritative and require no verification.
- **Check** all `[Model-Sourced: External]` citations first — these carry the highest hallucination risk.
- **Then check** all `[Model-Sourced: Internal]` citations — lower risk but still worth confirming.

**If no tags are present** (standalone use on any document):
- Check all citations.

Tell the user: *"I found [X] citations to verify ([Y] external, [Z] internal). I'll check each one now."*

---

### Step 2 — Build Verification Checklist

For each citation to verify, extract:
- The specific claim being made in the text
- The source cited: author/organisation, title, year
- The passage context (the sentence containing the citation)

---

### Step 3 — Re-Retrieve and Verify

For each citation on the checklist:

**3a. Search for the source**
- Web search for the exact title + author/organisation + year
- If it is a WBG document, also search internally
- Make two search attempts before classifying as Unverified

**3b. Compare the source against the claim**
- If found: does the source support the specific claim made in the text?
- If found but says something different: classify as Mismatched
- If not found after two attempts: classify as Unverified

---

### Step 4 — Classify and Correct

For each citation, apply one of three actions:

| Classification | Criteria | Action |
|---|---|---|
| Verified | Source re-found; content supports the claim | Keep as-is |
| Mismatched | Source re-found; content differs from the claim | Rewrite the sentence to accurately reflect what the source says, OR remove the citation and rewrite as uncited analytical narrative |
| Unverified | Source not found after two search attempts | Remove the citation; rewrite the passage as uncited analytical narrative (e.g., "Analysts have noted that..." or "Evidence suggests...") |

**Rewrite rules:**
- Change only the sentence or clause affected by the failed citation
- Preserve the analytical argument wherever the underlying point is sound
- Do not restructure surrounding paragraphs
- Do not introduce new citations as replacements

---

### Step 5 — Output

Return two things:

**1. The revised draft** with all corrections applied. Preserve all original formatting, headings, and structure.

**2. A verification summary table:**

| # | Citation | Status | Action Taken |
|---|---|---|---|
| 1 | (World Bank 2023) | Verified | — |
| 2 | (ACLED 2025) | Verified | — |
| 3 | (ICG 2024) | Mismatched | Rewritten to reflect actual source content |
| 4 | (Smith & Jones 2023) | Unverified | Citation removed; passage rewritten as uncited narrative |

**Result:** [X] verified, [Y] corrected, [Z] removed.

If all citations verified: *"All [X] citations checked out. The draft is ready for circulation."*

If corrections were made: *"I corrected [Y] citations and removed [Z]. Please review the changes — the analytical points are preserved but some sourcing has been adjusted. The corrected passages are noted in the table above."*

---

### AI Disclaimer

*This skill verifies citations by re-searching for cited sources, but verification is constrained by search coverage and link accessibility. A Verified result means the source was re-found and appears to match — it is not a guarantee of accuracy. Always apply subject-matter judgement before operational use.*

---

### Skills Used Footer

*Skills used: fcv-citation-verifier | Also referenced: [list any other fcv- skills mentioned in the output]*

If no other FCV skills were referenced, use: *Skills used: fcv-citation-verifier*
