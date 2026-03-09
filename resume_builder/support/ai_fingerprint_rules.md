# AI Fingerprint Avoidance Rules

> **Architecture note:** The primary defense against AI detection is the generation protocol — specific facts from experience files, char limits, JD-specific vocabulary, named entities. This file is a secondary safety net for word/phrase/structural patterns.

---

## 1. Banned Words

**Tier 1 — Dead Giveaways (NEVER use in any output):**
delve, tapestry, multifaceted, pivotal, realm, synergy, paradigm, holistic, nuanced, foster, embark, leverage (as verb), utilize, harness, spearhead, cornerstone, landscape (metaphorical), journey (metaphorical), cutting-edge, novel, innovative (unless quoting a JD), groundbreaking

**Banned Adjectives (use replacement):**

| Banned | Replacement |
|--------|-------------|
| robust | strong, reliable |
| comprehensive | thorough, broad |
| innovative | new, original (or omit) |
| pivotal | key, central |
| meticulous | careful, precise |
| diverse | varied, wide-ranging |
| extensive | broad, deep, 10+ years of |

**Banned Verbs (use replacement):**

| Banned | Replacement |
|--------|-------------|
| leverage | use, apply, draw on |
| utilize | use |
| harness | apply, use, draw on |
| spearhead | lead, start, launch |
| foster | support, build, grow |
| facilitate | run, lead, coordinate, enable |
| showcase | show, demonstrate |
| underscore | show, highlight |
| bolster | strengthen, support |

**Banned Adverbs:** meticulously, notably, subsequently (use "then" or "later"), remarkably, seamlessly, thereby

**Banned Nouns (metaphorical use):** tapestry, landscape, journey, realm, synergy, paradigm, cornerstone

**Technical exceptions:** "landscape" is fine when literal (e.g., "free energy landscape," "threat landscape"). "Novel" is fine when quoting a JD verbatim. Judge by context.

---

## 2. Banned Phrases

**Opening / transition phrases:**
- "In today's rapidly evolving..."
- "At the forefront of..."
- "It is worth noting that..."
- "This experience has taught me..."
- "I am uniquely positioned to..."
- "In an era of..."

**Resume / CL specific:**
- "proven track record"
- "passionate about" (use specific interest instead)
- "I am excited to apply" (use concrete reason instead)
- "demonstrated ability to" (just state what you did)
- "strong foundation in"
- "well-versed in"
- "adept at"

**Academic / research:**
- "groundbreaking research"
- "cutting-edge methodology"
- "novel approach" (say what is new about it)
- "significant contributions to the field"
- "at the intersection of X and Y" (name the specific intersection)

---

## 3. Structural Rules

### Sentence-Level
- **No reframe pattern:** Never use "It's not X — it's Y" constructions
- **No rhetorical Q+A:** Never ask a question then answer it ("What makes this unique? The answer is...")
- **No gerund fragment stacking:** Avoid sequences of 3+ "-ing" phrases ("developing, testing, and deploying...")
- **No -ing analysis endings on bullets:** This is the **#1 structural AI marker**. Bullets must NOT end with "-ing" phrases like "...advancing the field," "...contributing to improved Y," "...enabling new Z." Fix: restructure so the bullet ends with a concrete result, metric, or object. Example: "...contributing to a 15% reduction" is fine (ends with metric); "...contributing to improved efficiency" is not (vague -ing ending).
- **Max 2 em-dashes per document:** Count all `---` in the full .tex file (resume or CL). If more than 2, replace extras with commas, semicolons, or parentheses. Fellowships/Honors items use `. ` not `---`.
- **Post-gen scan:** After generating any document, scan all bullets for -ing endings. Flag and fix any found.

### Prose-Level
- **Vary sentence length:** Mix short (8-12 words) with long (20-30 words). Three consecutive same-length sentences flag as AI.
- **No same-structure paragraph starts:** If P1 opens "My research...", P2 must NOT open "My experience..." P3 must NOT open "My approach..."
- **No constant triplet structures:** Avoid "X, Y, and Z" in more than 2 sentences per document. Use pairs, single items, or lists of 4+.

---

## 4. Positive Markers (signals of human writing)

1. **Specific details:** "Ran 847 MD simulations on protein variants" not "Conducted extensive simulations"
2. **Front-loaded specifics:** Lead with the concrete thing, not the framing
3. **Named entities:** Tool names, method names, journal names, institution names
4. **Audience-appropriate jargon:** Use the JD's vocabulary, not generic synonyms
5. **Short connecting words:** "so," "but," "and," "then" — not "consequently," "however," "additionally," "subsequently"
6. **First-person specificity in CLs:** "I built" not "Was responsible for building"
7. **Inside knowledge:** Reference specific group names, facility names, programmatic areas
8. **Sentence length variety:** Deliberate mix of 8-word and 25-word sentences
9. **Occasional "And"/"But" sentence openers** in CLs (1-2 per page max)
10. **Contractions in CLs:** "I've" and "didn't" are acceptable in industry CLs (not academic)
11. **One human detail per CL page:** A specific lab memory, a conference conversation, a problem that kept you up — concrete and brief

---

## 5. CL-Specific Note

Cover letters are the most vulnerable document to AI detection because they are prose-heavy and readers have strong intuitions about "how people write." All rules above apply with extra weight in CLs. Pay special attention to:
- Opening sentence (must be specific to the company, not generic)
- Sentence length variety (CLs with uniform 15-20 word sentences read as AI)
- Em-dash usage (CLs accumulate em-dashes fastest — max 2 for the entire letter)

---

## 6. Post-Generation Critique Scan Checklist

Run this 12-item scan on every generated document before presenting to the user:

1. [ ] Any Tier 1 banned word present? (Search for each)
2. [ ] Any banned phrase from Section 2?
3. [ ] More than 2 em-dashes (`---`) in the document?
4. [ ] Any bullet ending with an -ing analysis phrase?
5. [ ] Three or more consecutive sentences of similar length?
6. [ ] Paragraph starts repeat the same structure (e.g., "My research...", "My experience...")?
7. [ ] More than 2 "X, Y, and Z" triplet structures in the document?
8. [ ] CL opens with a generic phrase instead of a company-specific reference?
9. [ ] Any metaphorical use of "landscape," "journey," "realm," or "tapestry"?
10. [ ] Passive voice in more than 20% of bullet verbs?
11. [ ] Fellowships/Honors items use `---` instead of `. `?
12. [ ] Any adverb from the banned list (meticulously, notably, subsequently, etc.)?

**If any item fails:** Fix before presenting. These are not optional polish — they are detectable AI patterns.
