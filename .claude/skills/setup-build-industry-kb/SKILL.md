---
name: setup-build-industry-kb
description: Synthesize completed extractions into the knowledge base files needed for resume generation
user-invocable: true
disable-model-invocation: true
---

# /setup-build-kb

**User input:** `$ARGUMENTS`

Parse `$ARGUMENTS`:
- Empty → full build (all phases)
- Phase number (e.g., `3`) → resume from that phase
- "experience" / "bundles" / "skills" / "pubs" / "reframing" / "significance" → run only that component
- "status" → show what's built and what's missing

---

## Startup

1. Read `CLAUDE.md` — check KB Corrections Log
2. Read `config.md` — load:
   - Personal Info
   - Document Preferences
3. Read `knowledge_base/extractions/_INVENTORY_INDUSTRY.md` — verify extractions exist
4. Read the latest `knowledge_base/extractions/resume_context` based on the dates at the end of filename, this is called `resume context` for this skill
4. Scan `resume_builder/` to see what's already built

**Pre-flight check:**
- If `_INVENTORY_INDUSTRY.md` is empty or has no entries: "No extractions found. Run `/setup-extract` first." Stop.
- If fewer than 2 extractions: warn "Only [N] extraction(s) found. KB quality improves with more papers. Continue anyway?"

Progress: "Found [N] extractions across [M] positions. Config has [K] role types defined."

---

## Phase 1: Build Experience Files

**Goal:** Create one experience file per position, containing all achievements organized for resume generation.

**Read:** `resume context`

**For each position** (from the latest `knowledge_base/extractions/resume_context`):

1. Group extractions by the position they belong to (based on dates, institution, or user clarification)
2. Ask the user to confirm grouping if ambiguous: Correct?"

**Experience file format** (`resume_builder/experience/experience_<position_key>.md`):

```markdown
# Experience: [Position Title] — [Company]
## [Date Range]

### Cross-Position Section
[Brief narrative connecting this position's work to the user's broader trajectory]
[CL framing content — how this position fits the career arc]

---

### Achievement [ID]: [Short Title]
**Source:** [extraction filename]
**User's role:** [sole developer / Senior Developer / Developer]

**Context:** [1-2 sentences — what problem, why it matters]

**Bullet variants:**
- **2L:** [Full 2-line bullet text — STAR format, ~180-210 rendered characters]
- **3L:** [Full 3-line bullet text — for CV use, ~270-310 rendered characters]
- **1L:** [Condensed 1-line version — ~90-110 rendered characters, for tight budgets]

**Key skills:** [comma-separated list of skills this achievement demonstrates]
**ATS keywords:** [domain-specific terms an ATS might scan for]
**Reframing notes:** [how to emphasize different aspects for different role types]

---
[Repeat for each achievement]
```

### >>>>>> MANDATORY STOP — DO NOT PROCEED <<<<<<
Present the experience file(s) — show achievement count per position, total bullet variants.
Ask user to review: "Are the groupings correct? Any achievements missing or misattributed?"
**You MUST wait for the user's explicit text response before continuing.**

---

## Phase 2: Build Skills Taxonomy

**Goal:** Create a categorized inventory of all technical skills from extractions.

**Read:** All Methods & Tools sections + `resume context`

**Build** `resume_builder/support/skills_taxonomy.md`:

```markdown
# Skills Taxonomy

## Summary Stats
- Total unique skills: [N]
- Publications: [N] ([breakdown by status])
- Top methods: [ranked list]

## Categories

### [Category 1: e.g., Computational Methods]
| Skill | Proficiency | Evidence | Resume Weight |
|-------|-----------|----------|---------------|
| [skill] | [expert/proficient/familiar] | [Short description linking to reason] | [HIGH/MED/LOW] |

### [Category 2: e.g., Programming & Software]
[same table format]

### [Category 3: e.g., Machine Learning]
[same table format]

[Continue for all categories]
```

**Proficiency levels:**
- **Expert:** Lead, created, Developed custom tools
- **Proficient:** Used extensively in work, comfortable teaching, mentored
- **Familiar:** Used in one project, or contributed to someone else's implementation

Progress: "Built taxonomy — [N] skills across [M] categories"

---

## Phase 3: Build Achievement Reframing Guide

**Goal:** Per-achievement significance lines + framing directives for each role type.

**Read:** Experience files + Role Types in `resume context`

**Build** `resume_builder/support/achievement_reframing_guide.md`:

```markdown
# Achievement Reframing Guide

## How to Use
For each achievement, `Significance:` provides a one-line framing cue.
The role-type table shows how to emphasize/de-emphasize for each target audience.

---

### [Achievement ID]: [Title]
**Significance:** [One sentence — why this matters broadly]

| Role Type | Emphasis | Lead Verb | Framing Angle |
|-----------|----------|-----------|---------------|
| [role 1] | HIGH | Developed | [emphasize X aspect] |
| [role 2] | MEDIUM | Applied | [bridge to Y domain] |
| [role 3] | LOW | -- | [omit or condense] |

**Overclaiming warning:** [if applicable — e.g., "Do not claim sole credit for sections where "helped" generate results"]
---
[Repeat for each achievement]
```

### >>>>>> MANDATORY STOP — DO NOT PROCEED <<<<<<
Present the reframing guide summary — show which achievements are HIGH for which role types.
Ask user: "Does this priority mapping look right for your target roles?"
**You MUST wait for the user's explicit text response before continuing.**

---

## Phase 4: Build Bundles

**Goal:** One bundle per role type from `resume context`, with 5 sections each.

**Read:** Experience files + Skills Taxonomy + Reframing Guide + `resume context` Role Types

**For each role type**, create `resume_builder/bundles/bundle_<role_type>.md`:

```markdown
# Bundle: [Role Type Name]

> Target employers: [from `resume context`]
> Tier: [from `resume context`]

---

## S1: Role Profile & Priority Matrix

**Positioning:** [1-2 sentences — how to position the user for this role type]

### Priority Matrix
| Priority | Achievement IDs | Rationale |
|----------|----------------|-----------|
| HIGH | [IDs] | [why these lead for this role type] |
| MEDIUM | [IDs] | [supporting evidence, bridge topics] |
| LOW | [IDs] | [omit unless budget allows or JD specifically asks] |

---

## S2: Summary Guide

**Headline pattern:** [Role-appropriate headline template]
**Building blocks:** [3-5 phrases that should appear in summaries for this role type]
**Avoid:** [terms/framings that don't fit this audience]

---

## S3: Achievement Reframing Map

[For each HIGH/MEDIUM achievement: which angle to use, which metrics to lead with]

| ID | Default Framing | This Role's Framing | Key Metric |
|----|----------------|--------------------|-----------| 
| [ID] | [generic] | [role-specific angle] | [number to highlight] |

---

## S4: Skills Guide

**Bold tools (resume):** [3-5 tools to bold in Technical Skills for this role type]
**Must-include skills:** [skills that MUST appear for ATS match]
**Nice-to-have:** [skills to include if budget allows]
**Omit:** [skills irrelevant to this audience]

---

## S5: Cover Letter Guide

**Opening hook pattern:** [template for first paragraph opener]
**Key narrative thread:** [what story to tell across paragraphs]
**"Why them" angle:** [what to research about target employer]
**Avoid:** [CL anti-patterns for this role type]
```

Progress: "Building bundle for [role type] — [N] HIGH priority achievements, [M] bold tools"

---

## Phase 5: Build Significance Research Files

**Goal:** Field context for cover letters — NOT for resume bullets.

**For each position**, create `resume_builder/support/significance_<position_key>.md`:

```markdown
# Significance Research: [Position]

> Use in cover letters and summaries — NOT in resume bullet text.
> These provide field context that demonstrates the user understands the landscape.

---

### [Achievement ID]: Field Context
**The problem:** [What challenge does this address? Industry/scientific context]
**Competing approaches:** [What else exists? What are the limitations?]
**Why this matters:** [Market size, industry need]
**Differentiation:** [What makes the user's approach unique or better?]

---
[Repeat for each major achievement worth cover-letter depth]

### Field Overview: [Broad Topic]
[2-3 paragraphs of field context that multiple achievements contribute to]
[Useful for cover letter opening hooks and "why this matters" framing]
```

Progress: "Significance research — [N] achievements with field context, [M] field overviews"

---

## Final: Status Report

After all phases complete (or after the requested subset), present:

### KB Build Status
| Component | File | Status | Items |
|-----------|------|--------|-------|
| Experience files | `experience/*.md` | [DONE/MISSING] | [N achievements] |
| Skills taxonomy | `support/skills_taxonomy.md` | [DONE/MISSING] | [N skills] |
| Reframing guide | `support/achievement_reframing_guide.md` | [DONE/MISSING] | [N entries] |
| Bundles | `bundles/bundle_*.md` | [DONE/MISSING] | [N bundles] |
| Significance | `support/significance_*.md` | [DONE/MISSING] | [N files] |

### Ready for Generation?
- [ ] At least 1 experience file with 5+ achievements
- [ ] Skills taxonomy with 20+ skills
- [ ] At least 1 bundle matching a target role type
- [ ] Reframing guide covers all achievements
- [ ] Significance files for cover letter depth

If all checked: "Knowledge base is ready. Save a JD to `JDs/` and run `/make-resume JDs/<filename>.txt`"
If gaps: "[List what's missing and which phase to re-run]"

### >>>>>> MANDATORY STOP <<<<<<
Present status report. Wait for user confirmation.
**You MUST wait for the user's explicit text response before continuing.**
