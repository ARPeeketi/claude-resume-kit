# Resume & CV Generation — Reference

> Resume/CV-specific rules. Read by `/make-resume` and `/edit-resume`.
> Companion files: `cl_reference.md` (CL rules), `critical_rules.md` (compact re-read).
> Shared rules (provenance, anti-fabrication, LaTeX notation): `CLAUDE.md`

---

## QUICK BUDGET CARD (read this FIRST)

```
RESUME (2-page, resume.cls):  ~20 variable bullets | Skills 13 lines (4-3-2-2-2) | 5 pubs | 5 awards
CV     (5-page, cv.cls):      19-21 variable bullets (45 rendered lines) | Skills 17 lines (4-4-3-3-3) | all pubs | 6 awards

Resume bullet: max 2 rendered lines | 1L: 105-111 chars | 2L: 189-205 chars (target ~200)
CV bullet:     max 3 rendered lines | 2L: 168-182 chars | 3L: 250-268 chars (target ~175/~260)

Cover letter: Resume = 1 page (250-300 words) | CV = 1-2 pages (350-450 words)
Full package: Resume + CL = 3 pages | CV + CL = 6-7 pages
```

**If your bullet count doesn't match the budget above, STOP and fix before generating.**

---

## Section-by-Section Specs

### Resume (resume.cls)

1. **Summary** (bundle Section 2): 4-5 sentences, exactly 5 body lines. 500-555 rendered chars (HARD MAX 570, floor ~490). Orphan: last line >= 78 chars.
   - **Headline Tagline:** 80-95 rendered chars, exactly 1 line.
2. **Technical Skills** (bundle Section 4 + skills_taxonomy.md): Format C — 5 groups, default 4-3-2-2-2 (13 lines). Each dash = exactly 1 rendered line. Bold penalty: 119 - (0.5 x bold_chars).
3. **Research Experience** (experience files + achievement_reframing_guide.md): Write bullets FRESH per Experience Bullet Writing Protocol (below). Max 2 rendered lines per bullet. Run char_count.py after each position.
   - resume.cls: Args 3+4 on SAME italic line
   - **After all positions: verify total variable bullet count matches budget**
4. **Education**: FIXED — copy from template
5. **Selected Publications** (pub_metadata.md): 5 publications scored per JD. Copy FIXED author+journal blocks, GENERATE JD-shortened title + tags. 2 rendered lines hard limit per entry.
6. **Honors & Awards**: FIXED — items from template
7. **Immigration notice**: FIXED for USA JDs. Delete for non-USA JDs.

### CV (cv.cls)

1. **Research Summary** (bundle Section 2): Exactly 6 body lines. 500-540 rendered chars (HARD MAX 545, floor ~490). Orphan: last line >= 62 chars. Technical identity, not narrative.
2. **Education**: FIXED — copy verbatim from cv_template.tex
3. **Technical Expertise** (bundle Section 4 + skills_taxonomy.md): 4-4-3-3-3 ALWAYS (17 body lines). Bold penalty: 91 - (0.25 x bold_chars).
4. **Research Experience**: Exactly 45 rendered bullet lines across 19-21 bullets, plus sub-theme lines.
   - cv.cls: Args 3+4 on SEPARATE italic lines
   - Max 3 rendered lines per bullet. CV-2L <= 190, CV-3L <= 280 (target ~175/~260)
   - **Running total must reach exactly 45 rendered lines**
5. **Fellowships & Honors**: FIXED — items from cv_template.tex
6. **Publications**: FIXED — full list from cv_template.tex
7-10. **Presentations, Mentorship, Collaborations, Computing**: All FIXED from cv_template.tex

---

## Character Limits (HARD STOPS — ZERO TOLERANCE)

**MANDATORY: Count rendered characters for EVERY bullet BEFORE writing it.** Do not write a bullet and check afterward — pre-calculate the count. If a bullet exceeds the limit, rewrite it BEFORE moving to the next bullet. This is not a post-generation check; it is a per-bullet gate.

**How to count rendered characters:**
Strip all LaTeX markup before counting: `\textbf{X}` -> X, `\textit{X}` -> X, `\ce{X}` -> X, `$\beta$` -> 1 char, `\sim` -> 1 char, `$<$` -> 1 char, `$^\dagger$` -> 1 char, `--` -> 1 char (en-dash), `\underline{X}` -> X, `\href{url}{text}` -> text only.
Count: all remaining characters including spaces.

**Resume (10pt, textwidth=7.5in):**

| Target Lines | Rendered Char Range | HARD MAX | Orphan Threshold |
|-------|---------------|---------|------------------|
| 1 line | 105-111 chars | 117 | -- |
| 2 lines | 189-205 chars | 218 | Last line >= 78 chars |

**CV (11pt, textwidth=7.5in):**

| Target Lines | Rendered Char Range | HARD MAX | Orphan Threshold |
|-------|---------------|---------|------------------|
| 1 line | 88-93 chars | 101 | -- |
| 2 lines | 168-182 chars | 190 | Last line >= 65 chars |
| 3 lines | 250-268 chars | 280 | Last line >= 65 chars |

> **WARNING: AIM FOR THE MIDDLE OF THE TARGET RANGE — NOT THE HARD MAX.**
> A Resume-2L bullet should target ~200 chars, not 218. A CV-2L should target ~175, not 190.
> The hard max exists as a safety valve, not a target. Proportional fonts have variable char widths —
> a bullet at the hard max WILL overflow if it contains wide characters (m, w, W, capitals, em-dashes).
> Em-dash (---) counts as 1 char but renders ~2x wide. Budget 2 extra chars per em-dash in the bullet.

### Variant Naming

| Variant | Document | Lines | Target Range | HARD MAX | Orphan | Word Target |
|---------|----------|-------|-------------|----------|--------|-------------|
| Resume-1L | 1/2-page resume | 1 | 105-111 | 117 | -- | ~13 words |
| Resume-2L | 2-page resume | 2 | 189-205 | 218 | >= 78 | ~23-25 words |
| CV-2L | 5-page CV | 2 | 168-182 | 190 | >= 65 | ~21-22 words |
| CV-3L | 5-page CV | 3 | 250-268 | 280 | >= 65 | ~31-32 words |

> **Word targets** are approximate first-draft heuristics for prose bullets (~7.9 chars/word). After drafting, always verify with precise char count. Skills dashes: NO word proxy -- use iterative char count only (technical tool lists average ~11 chars/word).

### Bold Width Penalty (COMPILE-VERIFIED)

Bold characters render wider than normal text. Adjust effective char limits accordingly.

**Resume (10pt):** Effective limit = 119 - (0.5 x bold_char_count)
- 0 bold: safe up to 119 chars/line
- 2-4 bold tools (~10-25 bold chars): 107-112 effective --> use 105-111 as default
- 5+ bold tools (~28+ bold chars): ~105 effective --> tighten to 99-105

**CV (11pt):** Effective limit = 91 - (0.25 x bold_char_count)
- 0 bold: safe up to 91 chars/line (HARD MAX 93)
- 2-3 bold tools (~10-18 bold chars): 85-88 effective --> use 83-88 as default
- 5+ bold tools (~28+ bold chars): 83-85 effective --> tighten to 80-85

Practical rule: count bold characters, subtract half (resume) or quarter (CV) from base limit.

**Per-bullet enforcement protocol:**
1. Write the bullet text (LaTeX source)
2. Strip all markup mentally → count rendered chars
3. If count > HARD MAX → rewrite immediately (do NOT proceed)
4. If multi-line and last line < orphan threshold → rewrite to fill or shorten
5. **Aim for the middle of the range**, not the max. A bullet at 220 rendered chars (resume 2L) is risky — target ~200.

**Orphan rule:** For any multi-line bullet, the last rendered line must fill at least 70% of the line width. If it doesn't, rewrite to either fill the line or shorten to one fewer line.

### Char Verification Protocol (EVERY written element)

For each element you write from scratch or modify (summary, skills dash, tagline, any edited bullet):

1. **DRAFT** -- Use word-count target as initial guess (prose only, NOT skills dashes)
2. **STRIP** -- Remove LaTeX markup (\textbf{}, \ce{}, $..$) to get rendered text
3. **COUNT** -- Count rendered characters precisely. In Claude Code, use the helper: `python3 resume_builder/helpers/char_count.py "bullet text"` or verify a full .tex file: `python3 resume_builder/helpers/char_count.py -f [resume|cv] output/file.tex`
4. **CHECK** -- Compare against target range (use tighter targets from Variant Naming table, not HARD MAX)
5. **FIX** -- If OVER and attempts < 3: rewrite/trim, go to step 2
6. **FLAG** -- If OVER after 3 attempts: add `% OVER LIMIT: [N] chars, target [M]` LaTeX comment, move on
7. **PASS** -- If within range: move to next element

**RULE: Never move to the next section with a violation in the current one. Fix first, then proceed.**

---

## Page Fill Budgets

**2-Page Resume (resume.cls, 10pt):**

Technical Skills uses Format C (categorized dash sub-items, 5 groups).
Any internship/fixed position is ALWAYS present (FIXED bullets, not counted in variable budget).

**Variable Bullet Budget (Format C):**

The exact variable bullet count depends on your skills configuration and whether a USA immigration line is present. Typical range: **20-21 variable bullets** across all research positions. Count your FIXED bullets separately — they are set in the template.

**Adjustments:**
- Adding a skills line (e.g., 4-4-2-2-2 instead of 4-3-2-2-2): -1 variable bullet
- Removing immigration line (non-USA JD): +1 variable bullet in some configurations

**5-Page CV (cv.cls, 11pt) — LOCKED:**

Total: **~209 rendered text lines** across 5 pages. 1-2 lines slack at bottom of page 5 is acceptable.

The exact line budget depends on your template's FIXED sections (publications, presentations, awards, etc.). Count the FIXED lines in your template, then allocate the remainder to JD-dependent content. The key constraints:

| Category | Status |
|----------|--------|
| Header, Education, Honors, Pubs, Presentations, etc. | FIXED (count from template) |
| Research Summary | JD-DEPENDENT (typically 7 lines: 1 heading + 6 body) |
| Technical Expertise | JD-DEPENDENT (typically 18 lines: 1 heading + 17 body) |
| Experience bullets | JD-DEPENDENT (**target 45 rendered lines**, 19-21 bullets, 2L/3L mix) |
| Sub-theme names | JD-DEPENDENT (varies by position count) |

**Experience bullet mix options (45 rendered lines):**
- 18x2L + 3x3L = 21 bullets | 15x2L + 5x3L = 20 | 12x2L + 7x3L = 19
- Allocate more bullets to JD-relevant positions, fewer to tangential ones

**Sub-theme rebalancing:** To shift bullet weight toward a more JD-relevant sub-theme: (a) drop the weakest bullet from a less-relevant sub-theme (-2L), (b) split a high-content 3L achievement into two 2L bullets (method + finding, +1L). Net = -1L saved while adding a bullet where it matters. Both split bullets must stay within char limits. Never split a 2L bullet — it becomes two 1L fragments that look thin.

**Position header rule:** The position title + date must fit on ONE line. If the title is too long, shorten the title so the date doesn't wrap to a second line. Wrapped dates waste a full vertical line and break visual alignment. Test by compiling — if the date wraps, trim the title.

**Budget workflow:** The line budget is pre-calculated from your template. Do NOT recalculate. Use the bullet counts above directly. After generation, verify that total bullet rendered lines = 45 (count each bullet's rendered lines and sum).

---

## Experience Bullet Writing Protocol (Experience-File-First)

**DO NOT use pre-written bullets.** Write every bullet FRESH from experience files, reframed for the target JD.

**Required files:** Experience files (all) + achievement_reframing_guide.md + bundle Section 1 (Priority Matrix) + bundle Section 3 (Reframing Map)

**Protocol:**
1. Determine document format -> look up bullet variant (Resume-1L/2L, CV-2L/3L) and budget
2. Allocate bullet count per position by JD relevance
3. For each position, consult bundle's **Priority Matrix** (Section 1) to rank achievements
4. For each achievement, consult **Achievement Reframing Guide** for role-type-specific framing directives
5. Write the bullet FRESH using target-domain vocabulary from bundle's **Reframing Map** (Section 3)
6. Verify char count per-bullet BEFORE moving to the next bullet
7. After all bullets written: run the **First-Pass Reframing Checklist** (in achievement_reframing_guide.md)

**Reframing during writing (NOT after):** Every bullet should use target-domain vocabulary from the start. Do not write in academic language and then "translate" -- write in target language directly using the Reframing Map. This is the single highest-ROI step: reframing alone moves scores from ~60 to ~85.

**Hybrid JDs (two role types):** Use primary role type's Priority Matrix for achievement ranking. Use secondary role type's Reframing Map for 1-2 bullets that bridge to the secondary domain.

---

## Position Title Format

**Resume -- FLIPPED format (JD theme as bold title, role as subtitle):**
Bold line = JD-customized domain theme (the single most powerful JD customization lever).
Italic subtitle = formal role + institution.

| Position | Bold Line (JD-customizable) | Subtitle |
|----------|-----------------------------|----------|
| Position 1 | [Theme, e.g., "First-Principles Discovery & ML-Accelerated Simulation"] | [Your Role], [Institution] |
| Position 2 | [Theme] ([Notable Award if applicable]) | [Your Role], [Institution] |
| Position 3 | [Theme] ([Fellowship if applicable]) | [Your Role], [Institution 1] & [Institution 2] |
| Internship | [Theme — FIXED] | [Your Role], [Company] | FLIPPED but FIXED |

**CV -- CONVENTIONAL format:**
Bold line = formal role title. Mentors on separate line. Sub-headers = story threads (underlined).

---

## Immutable Elements — NEVER Modify

The following elements are set in the `.cls` files and templates. **NEVER change them in generated output:**

- **`\vspace` values** between sections — these are calibrated. Do not add, remove, or adjust.
- **`\geometry` settings** (margins, textwidth, textheight) — locked per template.
- **FIXED section content** (Education, Fellowships, Publications, Presentations, Mentorship, Collaborations, Computing, Internship) — copy verbatim from template. Never rewrite, trim, or reorder.
- **`.cls` formatting** (font sizes, section rules, item separators, skill group spacing) — never override with inline LaTeX.
- **Header layout** (name, email, location, icons) — structure is template-locked. Only the email address and link URLs are configurable.

**If content spills to an extra page (orphan lines):** Fix by shortening VARIABLE content only (summary, skills dashes, experience bullets). Count rendered characters to ensure bullets actually fit their target line count (2L or 3L). A bullet that is "2L" in the budget but renders as 3L due to character overflow is the most common cause of page spill. Before declaring any output done, compile with pdflatex and verify page count matches target (resume=2, CV=5).

**When updating an existing .tex output (not generating from scratch):** Only modify VARIABLE content — summary text, skills group names/dashes, experience bullet text, sub-theme names. Never touch FIXED sections, vspaces, geometry, or cls overrides, even if a critique flags them as improvable. If a critique targets a FIXED section, note it for the next full regeneration instead.

---

## Post-Generation Verification

Run this checklist after compile gate passes, before critique. Also used as Part 7 of critique_framework.md.

Before presenting final output, verify:

- [ ] All mechanical checks pass (chars, orphans, page fill, no submitted, sequences, variants)
- [ ] Em-dash count: max 2 per document (resume or CL). Fellowships items use `. ` not `---`.
- [ ] No -ing analysis endings on bullets ("...advancing the field", "...contributing to Y"). Restructure to end with a concrete result or metric.
- [ ] All content checks pass (ATS, terms, inflation, provenance, pubs, cover letter)
- [ ] All narrative checks pass (scan test, per-position flow, cross-position arc, CV sub-headers)
- [ ] Company/institution name spelled correctly throughout
- [ ] .tex file has complete preamble (will compile standalone)
- [ ] Date format consistent (Mon YYYY -- Mon YYYY)

---

## Role-Type Decision Tree

| If JD mentions... | Primary profile | Secondary (hybrid) |
|-------------------|----------------|-------------------|
| _[your domain keywords]_ | _[your role type]_ | _[secondary or --]_ |
| _Example: national lab, DOE, postdoc_ | _National Lab_ | _--_ |
| _Example: machine learning, neural networks_ | _ML/AI_ | _National Lab_ |
| _Example: protein modeling, structural biology_ | _Computational Biology_ | _--_ |

**Hybrid resumes:** When a JD spans two role types, merge the two profiles. Primary sets priority matrix; secondary contributes supplementary bullets and keywords.

Customize the decision tree above with your own role types, tools, and domains in `CLAUDE.md`.

---

## Gap Assessment & Bridge Mappings

For each identified gap, assess:
- **Gap description:** What the JD asks for
- **Bridge framing (if available):** Use "methodology transferable to X" or "equivalent experience with Y" -- NEVER "experienced with X" unless directly demonstrated
- **Bridge confidence:** HIGH / MEDIUM / LOW
- **User decision:** Omit or bridge? (User decides per gap)

**Example bridge mappings** (customize for your own tools/methods):
- Tool A → "Custom solvers (Tool B/Tool C; computational methodology transferable to Tool A)" [HIGH]
- Framework A → "Deep learning framework expertise (Framework B; directly transferable to Framework A)" [HIGH]
- Simulation Package A → "Molecular dynamics expertise (Package B; transferable to Package A)" [HIGH]
- Language A → "Scientific computing (Language B, Language C; transferable to Language A)" [MEDIUM]

---

## Content Density Rules

| Format | Bullets | Publications | Awards | Presentations |
|--------|---------|-------------|--------|---------------|
| 1-page resume | ~6 | 3-5 | 2 | Omit |
| 2-page resume | ~12+ | 5-8 | 2-3 | May omit |
| 5-page CV | Comprehensive | All published + under review | All | All |
| Full CV | Everything | All published + under review | All | All |

---

## Files to Upload (by format)

**For resumes (1-page or 2-page):**
1. `bundle_[role_type].md` — Role-specific generation content (Sections 1-5)
2. `achievement_reframing_guide.md` — Role-type framing directives for all achievements
3. `skills_taxonomy.md` — Full skills inventory for Format C generation
4. `pub_metadata.md` — Publication database with scoring tags
5. `resume.cls` — Document class file
6. `resume_template.tex` — Structural template (contains FIXED sections)
7. Experience files from `resume_builder/experience/`

**For CVs (5-page or full):**
1. `bundle_[role_type].md` — Role-specific generation content (Sections 1-5)
2. `achievement_reframing_guide.md` — Role-type framing directives for all achievements
3. `skills_taxonomy.md` — Full skills inventory for Technical Expertise generation
4. `pub_metadata.md` — Publication database with scoring tags
5. `cv.cls` — Document class file
6. `cv_template.tex` — Structural template (contains FIXED sections)
7. Experience files from `resume_builder/experience/`

**Role type to bundle mapping:**
Bundles live in `resume_builder/bundles/`. Map each JD role type to its corresponding bundle file (e.g., `bundle_[role_type].md`).
