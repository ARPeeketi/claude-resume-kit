# Critique Framework — Consolidated Multi-Perspective Protocol

**Purpose:** Single-pass comprehensive critique that catches what would otherwise take multiple passes. Run AFTER generation but BEFORE presenting to user.

**Key insight:** 85% of score improvement typically comes from ONE thing — domain reframing. The Achievement Reframing Guide handles this during generation. The critique's job is to catch what leaked through, identify remaining gaps, and assess interview likelihood from multiple reader perspectives.

---

## Part 0: Domain-Specialist Lens (generate BEFORE the five perspectives)

Before running the five-perspective read-through, construct a domain-specialist lens for THIS specific JD + company. The lens is not a static lookup — it is generated fresh each time by analyzing the JD, the company, and the hiring context.

### Build the Lens

**If a session file exists** (`output/session_<name>.md`) with JD Analysis and Company Context sections, use those as the foundation for the lens instead of re-researching from scratch. Supplement only the elements not already covered (competitive landscape, methodology transfer test, reviewer persona details).

**If no session file exists,** research THIS company + THIS JD from scratch. No pre-built templates. No reference lenses.

**For each critique, produce these 7 elements:**

1. **Reviewer persona construction:** Who actually reads this resume? Construct from the JD's reporting line, department name, level, and company context.
   - Their job title and seniority
   - What they do daily (what tools they use, what problems they solve)
   - How many CVs they've read for this posting (estimate from company size + role level)
   - What they've seen 100 times before that makes them roll their eyes
   - What would genuinely surprise or impress them

2. **Company research:** What does this company MAKE, SELL, or RESEARCH?
   - Core business and revenue model
   - R&D culture: academic-leaning? patent-driven? product-shipping? mission-driven?
   - Recent news, strategic priorities, or technology bets (if known)
   - What vocabulary signals "insider who understands our business" vs "outsider applying generically"?
   - Note any assumptions and flag uncertainty

3. **JD deep read — vocabulary extraction:**
   - Read the JD 3 times. First for requirements, second for culture signals, third for vocabulary.
   - Extract the 8-10 most important terms/phrases (ranked by: frequency in JD, placement in title/header vs body, and whether they represent binary capabilities vs spectrum skills)
   - For each: what does THIS company mean by this term? (e.g., "emerging computing paradigms" at a given company might mean quantum/neuromorphic — not just "we use ML")
   - Identify the JD's implicit hierarchy: what's the #1 thing they need vs nice-to-haves?

4. **Domain vocabulary map:** For this specific JD, what are the 5-8 vocabulary swaps that separate "outsider applying" from "insider who gets it"? Generate these purely from the JD's language and the company context you just researched.

   Format:
   | Resume currently says | Should say for THIS JD | Why |
   |---|---|---|
   | [term] | [replacement] | [JD uses this language because...] |

5. **Fatal vs cosmetic gap ranking:** Which missing JD keywords would cause immediate rejection vs which are nice-to-have?
   - **Fatal gaps:** Binary capabilities the JD requires (e.g., "CFD" — you either do it or you don't), terms in the JD title, or phrases repeated 3+ times
   - **Serious gaps:** Preferred qualifications that multiple competitive candidates will have
   - **Cosmetic gaps:** Terms buried in preferred quals that most candidates also won't have
   - For each gap: can it be bridged truthfully? Or is it a hard limitation of the candidate's background?

6. **Methodology transfer test:** For each of the candidate's top 5 resume achievements, write one sentence explaining how a domain expert at THIS company would see it mapping to THEIR work.
   - If you CAN write that sentence naturally: the resume has bridged the gap
   - If you STRUGGLE to write it: the resume hasn't made the transfer explicit enough
   - If you CAN'T write it honestly: this is a hard gap, not a reframing problem

7. **Competitive landscape intuition:** Who else is applying for this role?
   - What background does the "obvious fit" candidate have?
   - What does THIS candidate offer that the obvious fit doesn't? (e.g., high-venue publication, cross-scale breadth, platform building)
   - What does the obvious fit offer that this candidate doesn't? (e.g., domain-specific publications, direct tool experience)
   - This determines what the resume must EMPHASIZE (unique strengths) and what it must BRIDGE (gaps relative to the obvious fit)

### Output and persist the lens

Write out all 7 elements as a structured section at the top of the critique file. This lens then informs EVERY subsequent perspective in Parts 1-6. The five readers (ATS, Recruiter, HR, HM, Technical) all read through this lens — they are people at THIS company, not generic archetypes.

**Persistence rule:** The lens is built ONCE per JD, during the first critique. If the resume is revised and critiqued again (multi-pass), reuse the same lens — do NOT re-research. The lens lives in the critique output file (`output/critique_[name].md`) and is carried forward across passes. Only rebuild the lens if the JD itself changes.

---

## Part 1: Five-Perspective Read-Through

Read the resume/CV from five different personas, in order. Each persona sees only what they'd actually read in their time window. Flag issues per persona.

### Perspective 1: ATS Robot (0 seconds — keyword scan)

**What it does:** Pattern-matches JD keywords against resume text. No context, no synonyms (unless configured), no reading comprehension.

**Check:**
- Extract top 20 JD keywords/phrases (tools, methods, domain terms, soft skills)
- For each: verbatim match? Semantic match? Absent?
- Count match rate: >=70% = PASS, 60-69% = MARGINAL, <60% = FAIL
- Flag any JD keyword that appears 3+ times in JD but 0 times in resume (high-priority gap)
- Check domain bridges — do they appear enough to pass a domain-specific ATS filter?

**Output:** Keyword match table + match rate + top 3 missing keywords that could be added truthfully.

### Perspective 2: Recruiter Glance (10 seconds)

**What they read:** Name, current title/employer, education line, header tagline, first 2 lines of summary. Nothing else.

**What they decide:** "Forward to hiring manager or reject?"

**Check:**
- Does the header tagline use target-domain language (not source-domain)?
- Does the current employer signal credibility for this role type?
- Does the education line clear the bar? If pedigree gap exists, does the summary compensate in the first 2 lines?
- Is there a prestige signal in the first 2 lines (top venue, major metric)?
- Would a non-technical recruiter understand what this person does?

**Output:** "Forward" / "Maybe" / "Reject" + one-sentence reasoning.

### Perspective 3: HR Screen (30 seconds)

**What they read:** Full summary + skills section headers + first bullet per position + education.

**What they decide:** "Does this person meet the basic qualifications? Schedule phone screen?"

**Check:**
- Does the summary bridge from actual domain to target domain? (The bridge sentence is the single most important sentence in the document)
- Do skills group NAMES (not just content) signal target-domain relevance?
- Does the first bullet under each position deliver the strongest JD-relevant achievement?
- Are years of experience consistent with JD requirements?
- Immigration status present if required?

**Output:** "Phone screen" / "Borderline" / "Pass" + one-sentence reasoning.

### Perspective 4: Hiring Manager Read (2 minutes)

**What they read:** Everything on the resume/CV. They're a domain expert.

**What they decide:** "Interview or not? What would I ask?"

**Check:**
- **Methodology transfer:** For each major bullet, can the HM see how this applies to THEIR work? Or do they have to imagine the transfer themselves? (If the HM has to do the translation, you've lost points)
- **Narrative arc:** Does the story progress logically? (Typical good arc: deep science → engineering discipline → leadership → tools/platforms)
- **Red flags:** Any overclaiming? Any "this person doesn't know what we do" signals? Any keyword stuffing that feels forced?
- **Differentiation:** What makes this candidate different from other applicants? Is that differentiator visible?
- **Domain gap honesty:** Does the resume acknowledge what it ISN'T (transparent about actual domain) while showing what transfers? Honest reframing beats pretend expertise.

**Output:** "Interview" / "Maybe" / "No" + top 3 things HM would notice + predicted first interview question.

### Perspective 5: Deep Technical Reviewer (10 minutes)

**What they do:** Read every bullet carefully. Check publications. Assess truthfulness. Look for inconsistencies.

**Check:**
- **Truthfulness audit:** For each quantitative claim, is it verified against extractions/experience files?
- **Provenance flags:** All works-in-progress or under-review items properly flagged?
- **Verb discipline:** Contributing-author bullets use hedged verbs? Full-ownership verbs only where justified?
- **Publication coherence:** Do pub tags match the resume's domain framing? Do paper titles (which can't be changed) create cognitive dissonance with the reframed bullets?
- **Internal consistency:** Does the summary match the bullets? Does the cover letter match the resume?
- **Over-saturation:** Any keyword repeated >8 times? (Borderline at 6-8, concern at 9+)

**Output:** Truthfulness table (claim → verified? → source) + any inconsistencies found.

---

## Part 2: Eight-Dimension Scoring

Score each dimension independently, then compute weighted total.

| # | Dimension | Weight | What to Assess |
|---|-----------|--------|---------------|
| 1 | ATS Keyword Match | 15% | JD keyword coverage rate, verbatim vs semantic, missing high-value terms |
| 2 | Summary | 10% | Bridge sentence, target-domain language, prestige signals, forward-looking intent |
| 3 | Skills Section | 10% | Group names (domain signal), content relevance, bold accuracy, no wasted entries |
| 4 | Bullet Quality | 25% | Per-bullet JD alignment (HIGH/MEDIUM/LOW), reframing quality, quantification, action verbs |
| 5 | Publication Selection | 10% | Venue prestige, tag relevance, first-author ratio, domain gap acknowledgment |
| 6 | Narrative Coherence | 15% | Header-to-footer story, domain thread count, first-impression timing |
| 7 | Page Fill & Visual | 5% | Budget compliance, orphan check, compile clean, slack acceptable |
| 8 | Credibility Signals | 10% | Venue quality, metrics (papers, citations, awards), platform adoption, leadership evidence |

**Scoring rubric per dimension:**
- 9-10: Essentially optimal for this candidate-JD pairing
- 8-8.5: Strong, minor improvements possible but diminishing returns
- 7-7.5: Good but identifiable gaps that reframing could close
- 6-6.5: Significant gaps — missing domain bridge, wrong vocabulary, weak bullets
- <6: Major problems — wrong role framing, overclaiming, format violations

**Overall score interpretation:**
- 85+: At or near ceiling. Submit.
- 80-84: Strong. 1-2 targeted improvements could push to ceiling.
- 75-79: Good foundation but missing domain reframing or key bullets.
- 70-74: First-draft quality. Needs systematic reframing pass.
- <70: Fundamental issues (wrong role type, missing sections, accuracy problems).

---

## Part 3: Interview Likelihood Assessment

After scoring, assess interview probability from each reader's perspective.

### Assessment Matrix

| Reader | Time | Question They Ask | Likely Outcome |
|--------|------|-------------------|----------------|
| ATS | 0 sec | "Do keywords match?" | PASS / FAIL |
| Recruiter | 10 sec | "Credible for this level?" | FORWARD / REJECT |
| HR | 30 sec | "Meets basic quals?" | PHONE SCREEN / PASS |
| Hiring Manager | 2 min | "Would I learn something in an interview?" | INTERVIEW / MAYBE / NO |
| Technical Panel | 10 min | "Can this person do the work?" | STRONG YES / YES / CONCERNS |

For each reader, give a probability estimate (e.g., "80% forward") and the single factor that most influences their decision.

### Ceiling Analysis

| Scenario | Estimated Score |
|----------|----------------|
| Current resume | [X] |
| + Top 3 improvements applied | [X + delta] |
| Theoretical max (this candidate + this JD) | [X_max] |
| Hard ceiling (structural background gap) | [X_ceiling] |
| What would close the gap | [e.g., "1 domain publication → +3 pts"] |

---

## Part 4: Actionable Improvements (Ranked)

List ALL identified improvements in three tiers:

### Tier 1: HIGH IMPACT (each worth >= 1 point)
These are the improvements that move the score meaningfully. Typically:
- Domain reframing that was missed during generation
- Missing JD keyword that can be added truthfully
- Bullet swap (weak bullet → stronger unused achievement)
- Summary bridge sentence missing or weak

For each: Current text → Proposed text → Why → Expected point impact.

### Tier 2: MEDIUM IMPACT (each worth 0.3-0.9 points)
- Minor reframing (vocabulary swap)
- Publication tag refinements
- Skills group name adjustments
- One additional keyword insertion

### Tier 3: COSMETIC / DIMINISHING RETURNS (each worth < 0.3 points)
- Keyword saturation reduction
- Minor wording polish
- Alternative pub selection

### Verdict
State clearly: "Apply Tier 1 changes. Tier 2 are optional. Tier 3 are not worth the edit."

---

## Part 5: Interview Bridge Points

For each major resume topic, provide the verbal bridge the candidate should use if asked in an interview. Format:

| Resume Topic | Target Domain Equivalent | Opening Line for Interview |
|---|---|---|
| [Achievement X] | [How it maps to target] | "The same methodology I used for X applies directly to Y because..." |

This section converts resume claims into interview talking points. Include 5-7 bridges covering highlights from all positions.

---

## Part 6: Cover Letter Critique (Context-Aware)

If a cover letter was generated in the same session, run all checks below. Detect institution type first: Industry / National Lab / Academic.

### 6A. Anti-Pattern Checklist
- [ ] Does NOT open with "I am writing to express my interest" or similar generic opener
- [ ] Does NOT rehash CV bullet points in prose (adds narrative context instead)
- [ ] Names a specific PI/group/product/paper from the target institution
- [ ] Has a clear "why THIS position at THIS institution" sentence (not generic)
- [ ] Strongest qualification appears in paragraph 1, not buried in P3/P4
- [ ] No defensive/apologetic language about background gaps ("Although my background is not in...")
- [ ] Closing has active call to action, not passive "Thank you for your consideration"
- [ ] Credentials (pubs, awards) woven into body paragraphs, not dumped in closing

### 6B. Tailoring Signal Checklist
- [ ] Names specific PI/group/program (academic/lab) or product/technology (industry)
- [ ] Uses at least 3 JD terms that supplement (not just duplicate) resume keywords
- [ ] References institution's mission, culture, or recent work
- [ ] Proposes specific connection between candidate's method and their need
- [ ] Correctly identifies institutional type and adjusts tone/emphasis accordingly

### 6C. Context-Specific Checks

**Industry:**
- [ ] Business value translation present for each achievement? ("enabling X, reducing Y")
- [ ] "Why industry" addressed positively? (not "leaving academia")
- [ ] Jargon minimized for HR/recruiter first reader?

**National Lab:**
- [ ] Mission alignment in P1? (specific programmatic thrust, not generic "clean energy")
- [ ] HPC/collaboration signals present?
- [ ] Lab vocabulary used? ("thrust area," "programmatic direction," "capability development")

**Academic:**
- [ ] PI named with specific research connection?
- [ ] Future research direction included? (mandatory even for postdoc, 1-2 sentences minimum)
- [ ] Departmental fit articulated? ("Your department's strength in X...")

### 6D. CL ATS Keyword Check
- Extract 10 high-priority JD keywords
- Check how many appear in CL (target: 5-8 that supplement resume keywords)
- Industry/lab: keywords matter (~60% of large employers use ATS/AI on CLs). Academic: less critical.

### 6E. Structural Checks
- [ ] **Consistency:** Key claims match resume bullets (no contradictions, no unsupported new claims)
- [ ] **Complementarity:** Adds narrative context the resume cannot (motivation, "why this company," research vision)
- [ ] **Word count:** Industry 250-300, Lab 350-450, Academic postdoc 350-450, Academic faculty 450-650
- [ ] **Tone match:** Industry = results-driven, Lab = mission-aligned, Academic = scholarly/forward-looking
- [ ] **Quantification:** 3-5 quantified claims (more = fact sheet, fewer = vague)
- [ ] **Domain pivot:** If pivoting, leads with methodology in P1, not apologetic framing

### 6F. Package Cohesion Check
- [ ] **Resume/CV stands alone:** If CL were deleted, does the resume/CV independently earn an interview? No critical context only in CL.
- [ ] **CL deepens, not introduces:** Every major CL claim is traceable to a resume/CV bullet. CL adds context/significance, not new achievements.
- [ ] **No contradictions:** Dates, metrics, claims, and framing consistent across both documents.
- [ ] **Complement, not repeat:** CL is NOT a prose restatement of resume bullets. It adds motivation, "why this institution," research vision, methodology arc.
- [ ] **Page budget:** Resume+CL = 3pp, CV+CL = 6-7pp. If CV CL is 2 pages, page 2 >= half filled before signature.

---

## Critique Output Template

```markdown
# Critique: [Company] [Role Title] ([Job ID])

**Resume/CV File:** `output/[filename].tex`
**Date:** [date]

---

## Domain-Specialist Lens (researched for this JD)

### Reviewer Persona
[Constructed persona — who reads this, what they do daily, what they've seen before]

### Company Context
[What they make/do, R&D culture, strategic priorities]

### JD Vocabulary Extraction (top 8-10 terms, ranked)
| # | JD Term | Frequency | Meaning at THIS Company | Resume Match? |
|---|---|---|---|---|
| 1 | [term] | [N times] | [what they mean by it] | YES/PARTIAL/NO |

### Domain Vocabulary Map
| Resume Currently Says | Should Say for This JD | Why |
|---|---|---|
| [term] | [replacement] | [reasoning] |

### Gap Ranking
- **Fatal:** [gaps that cause rejection]
- **Serious:** [gaps competitive candidates won't have]
- **Cosmetic:** [nice-to-have, most candidates also miss]

### Methodology Transfer Test
| Achievement | How THIS Company's Expert Sees It |
|---|---|
| [achievement] | "[one sentence transfer explanation]" |

### Competitive Landscape
- **Obvious fit candidate:** [description]
- **Our advantage:** [what we offer they don't]
- **Their advantage:** [what they offer we don't]

---

## Five-Perspective Read-Through

### ATS Robot (keyword scan)
[Keyword match table]
**Match rate:** X/20 = Y%

### Recruiter Glance (10 seconds)
**Verdict:** [Forward/Maybe/Reject]
[Reasoning]

### HR Screen (30 seconds)
**Verdict:** [Phone screen/Borderline/Pass]
[Reasoning]

### Hiring Manager (2 minutes)
**Verdict:** [Interview/Maybe/No]
**Top 3 observations:**
1. [What they notice first]
2. [What impresses or concerns them]
3. [What they'd ask about]
**Predicted first interview question:** "[question]"

### Technical Reviewer (10 minutes)
**Truthfulness:** [All verified / N concerns]
**Consistency:** [Clean / N issues]

---

## Eight-Dimension Scoring

| Dimension | Score | Weight | Weighted | Notes |
|---|---|---|---|---|
| ATS Keywords | X/10 | 15% | X.XX | [1-line note] |
| Summary | X/10 | 10% | X.XX | |
| Skills Section | X/10 | 10% | X.XX | |
| Bullet Quality | X/10 | 25% | X.XX | |
| Publications | X/10 | 10% | X.XX | |
| Narrative Coherence | X/10 | 15% | X.XX | |
| Page Fill & Visual | X/10 | 5% | X.XX | |
| Credibility Signals | X/10 | 10% | X.XX | |
| **Total** | | **100%** | **XX.X** | |

---

## Interview Likelihood

| Reader | Probability | Key Factor |
|--------|------------|------------|
| ATS | X% | [factor] |
| Recruiter (10s) | X% | [factor] |
| HR (30s) | X% | [factor] |
| Hiring Manager (2m) | X% | [factor] |
| Technical Panel (10m) | X% | [factor] |

**Ceiling:** Current [X] → Max achievable [Y] → Hard ceiling [Z]

---

## Actionable Improvements

### Tier 1 (HIGH — do these)
1. [Change] — [+N pts]

### Tier 2 (MEDIUM — optional)
1. [Change] — [+N pts]

### Tier 3 (COSMETIC — skip)
1. [Change]

---

## Interview Bridge Points

| Resume Topic | Target Equivalent | Opening Line |
|---|---|---|
| [topic] | [equivalent] | "[bridge statement]" |

---

*End of critique.*
```

---

## Part 6G: AI Fingerprint Scan

Run the 12-item checklist from `resume_builder/support/ai_fingerprint_rules.md` Section 6. Key scans:
- Count em-dashes (`---`) in full document — flag if >2
- Scan all bullet endings for -ing analysis phrases (the #1 structural AI marker)
- Search for any Tier 1 banned word (delve, tapestry, multifaceted, pivotal, etc.)
- Check CL for generic opener and uniform sentence length

Any failure is a Tier 1 fix in Part 4.

---

## Part 7: Post-Generation Verification

Final mechanical checklist. Run AFTER all other critique parts. These are pass/fail checks, not scored dimensions.

### Mechanical Checks
- [ ] All bullets within char limits (no OVER violations from char_count.py)
- [ ] All multi-line bullets pass orphan check (last line >= 70% fill)
- [ ] Page fill within budget (resume: <= 3 lines white space on page 2; CV: 45 rendered bullet lines)
- [ ] No ordering errors in bullet sequencing

### Content Checks
- [ ] ATS keywords present (>= 70% match rate)
- [ ] All provenance flags correct (see CLAUDE.md for project-specific flags)
- [ ] No forbidden terms (see CLAUDE.md for project-specific corrections)
- [ ] No inflation (contributing-author verbs hedged, no false claims)
- [ ] Publication entries match pub_metadata.md (titles, journals, years)
- [ ] Cover letter claims traceable to resume/CV bullets

### Structural Checks
- [ ] Company/institution name spelled correctly throughout
- [ ] .tex file has complete preamble (will compile standalone)
- [ ] Date format consistent (Mon YYYY -- Mon YYYY)
- [ ] Email address is correct (see CLAUDE.md for configured email)
- [ ] Page count correct after compile (resume=2, CV=5)

**If any check fails, flag it as a Tier 1 fix in Part 4.**

---

## When to Use Multi-Pass vs Single-Pass

**Single pass (this framework):** Use for ALL new generations going forward. The Achievement Reframing Guide ensures the first draft is already reframed, so one comprehensive critique should catch remaining issues.

**Multi-pass (iterative refinement):** Only needed when:
- Score is below 80 after first critique (indicates systematic reframing failure)
- User requests specific changes and wants re-evaluation
- A fundamentally new approach is tried (e.g., switching role-type framing mid-stream)

When doing multi-pass, each subsequent critique should:
1. State "Changes Since Pass N" at the top
2. Only re-score dimensions that changed
3. Track score trajectory (Pass 1 → Pass 2 → ...)
4. Declare ceiling when score stops moving (typically after 2-3 passes with the reframing guide)
