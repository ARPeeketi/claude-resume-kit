# claude-resume-kit

A Claude Code-powered framework for generating tailored resumes, CVs, and cover letters from structured knowledge bases.

Built for researchers, engineers, and technical professionals who apply to many positions and need each application package customized — without starting from scratch every time.

## Why This Exists

Applying to jobs as a researcher is painful. Each position needs a different framing of the same work: a national lab cares about method development, industry wants throughput metrics, academia wants publications and teaching. You end up with 15 slightly different Word docs, inconsistent formatting, and no systematic way to ensure you haven't overclaimed something.

This framework treats resume generation as a **structured pipeline** with enforced accuracy rules, not a "rewrite my resume" chat prompt. You build your knowledge base once, then generate tailored output for each JD in minutes.

**What makes it different from ChatGPT resume prompts:**
- **Anti-fabrication rules** baked into every skill — accuracy always beats impressiveness
- **Provenance tracking** — knows what's published vs. under review vs. internal
- **Role-type bundles** that frame the same work differently for different audiences
- **Mechanical enforcement** of page budgets, character limits, and formatting rules
- **Session files** that track every decision, making edits and critiques stateful
- **LaTeX output** — pixel-perfect formatting, not "close enough"

---

## How It Works

```
Your Papers ──→ /setup-extract ──→ Extractions ──→ /setup-build-kb ──→ Knowledge Base
                                                                           │
Job Description ──→ /make-resume ──→ Tailored Resume/CV (.tex)             │
                         │              ↓                                   │
                    /make-cl ──→ Cover Letter (.tex)                        │
                         │              ↓                                   │
                    /critique ──→ 8-Dimension Score + Fixes                 │
                         │              ↓                                   │
                    /edit-resume ──→ Refined Package                        │
```

**One-time setup (do once):**
1. `/setup-extract` — Run on each paper/project to create structured extraction files
2. `/setup-build-kb` — Synthesize extractions into experience files, bundles, and skills taxonomy

**Per-application (do for each JD):**
3. `/make-resume <JD>` — Analyze JD, plan bullets, generate tailored LaTeX
4. `/make-cl` — Generate a matching cover letter from the session file
5. `/critique` — Independent 8-dimension quality review
6. `/edit-resume` — Refine based on critique or your own feedback

Each step uses a **separate Claude Code session** for best quality (fresh context = less bias).

---

## Architecture

```
claude-resume-kit/
├── CLAUDE.md                          # Auto-loaded project instructions
├── config.md                          # Your personal configuration
├── .claude/skills/                    # 6 slash commands
│   ├── setup-extract/SKILL.md         # Extract from papers → structured data
│   ├── setup-build-kb/SKILL.md        # Synthesize KB from extractions
│   ├── make-resume/SKILL.md           # JD → tailored resume/CV (.tex)
│   ├── make-cl/SKILL.md               # Session → cover letter (.tex)
│   ├── edit-resume/SKILL.md           # Edit from critique/feedback
│   └── critique/SKILL.md              # Independent quality review
├── resume_builder/
│   ├── reference/                     # Generation rules and protocols
│   │   ├── shared_ops.md              # Session workflow (all skills read this)
│   │   ├── resume_reference.md        # Resume/CV formatting rules
│   │   ├── cl_reference.md            # Cover letter rules
│   │   ├── critical_rules.md          # Compact re-read for generation phase
│   │   ├── session_file_template.md   # Session file format spec
│   │   └── critique_framework.md      # 8-part critique system
│   ├── templates/                     # LaTeX .cls classes + .tex templates
│   │   ├── resume.cls                 # 2-page resume class
│   │   ├── cv.cls                     # Multi-page CV class
│   │   ├── resume_template.tex        # Resume structural template
│   │   ├── cv_template.tex            # CV structural template
│   │   └── coverletter_template.tex   # Cover letter template
│   ├── helpers/
│   │   └── char_count.py              # Character counting utility for bullets
│   ├── examples/                      # Fictional "Dr. Jordan Chen" — full worked example
│   ├── experience/                    # YOUR experience files (built by /setup-build-kb)
│   ├── bundles/                       # YOUR role-type bundles (built by /setup-build-kb)
│   └── support/                       # Skills taxonomy, pub metadata, AI fingerprint rules
│       └── ai_fingerprint_rules.md    # Banned words, structural rules, 12-item checklist
├── knowledge_base/
│   ├── extractions/                   # Paper extractions (built by /setup-extract)
│   ├── papers/                        # Drop your PDFs / .tex source here
│   └── notes/                         # Any other reference material
├── JDs/                               # Job descriptions (text files)
└── output/                            # Generated .tex files, session files, critiques
```

---

## Prerequisites

- **[Claude Code](https://docs.anthropic.com/en/docs/claude-code)** CLI installed and authenticated
- **A LaTeX distribution** for compiling `.tex` → `.pdf` (e.g., [TeX Live](https://tug.org/texlive/), [MacTeX](https://tug.org/mactex/), [MiKTeX](https://miktex.org/))
- **Your research papers** or project documentation ready for extraction

---

## Quickstart

### 1. Clone and enter the project

```bash
git clone https://github.com/ARPeeketi/claude-resume-kit.git
cd claude-resume-kit
```

### 2. Configure your profile

Edit `config.md` with your details. This file is read by every skill.

```markdown
## Personal Info
- **Name:** Your Name
- **Email:** you@email.com
- **LinkedIn:** linkedin.com/in/yourprofile
...

## Provenance Flags
| Item | Status | Correct Framing |
|------|--------|----------------|
| My ML paper | published in Nature | OK to say "published" |
| Internal tool | unpublished | "infrastructure I developed" — never imply peer-reviewed |

## Role Types
| Role Name | Target Employers | Tier | Bundle File |
|-----------|-----------------|------|-------------|
| Academic  | R1 universities | 1    | bundle_academic.md |
| Industry  | Tech companies  | 2    | bundle_industry.md |
```

See `resume_builder/examples/example_config.md` for a complete example.

### 3. Drop your papers

Place PDFs or `.tex` source files in `knowledge_base/papers/`.

### 4. Extract from each paper

```
/setup-extract knowledge_base/papers/my_paper.pdf
```

Claude reads the paper, asks clarifying questions about your specific contributions, then creates a structured extraction in `knowledge_base/extractions/`. Repeat for each paper.

### 5. Build your knowledge base

```
/setup-build-kb
```

This synthesizes all extractions into:
- **Experience files** (`resume_builder/experience/`) — one per position, with pre-written 2L and 3L bullet variants for every achievement
- **Role-type bundles** (`resume_builder/bundles/`) — positioning guides for each audience (what to emphasize, what to omit, how to frame)
- **Support files** (`resume_builder/support/`) — skills taxonomy, publication metadata, AI fingerprint avoidance rules

### 6. Customize your LaTeX templates

Open the templates and fill in your **FIXED sections** — content that never changes per JD:

- `resume_builder/templates/resume_template.tex` — Education, header, awards
- `resume_builder/templates/cv_template.tex` — Education, publications, header, awards, collaborations
- `resume_builder/templates/coverletter_template.tex` — Header, signature block

The `[CONFIG: ...]` placeholders show you exactly what to fill in. The `[GENERATE: ...]` sections are filled by Claude during generation.

### 7. Generate for a job

Save the job description as a text file in `JDs/`, then:

```
/make-resume JDs/target_job.txt
```

This runs a 3-phase pipeline:
- **Phase 0:** Web-searches the company, analyzes JD keywords, selects role-type bundle
- **Phase 1:** Plans which bullets to include and in what order (you approve the plan)
- **Phase 2:** Generates the full `.tex` file with enforced character limits

### 8. Cover letter + critique (separate sessions)

```
/clear
/make-cl
```
```
/clear
/critique
```

Then `/edit-resume` to address any critique findings.

---

## Concepts

### Session Files

Every JD gets a session file (`output/<Folder>/session_<name>.md`) that tracks:
- JD analysis and ATS keywords
- Which bundle was selected
- Bullet plan (which achievements, in what order, at what length)
- All generation decisions and their rationale
- Cover letter plan
- Critique scores

All 4 generation skills read and update this file. It's the single source of truth for each application.

### Experience Files

One file per position (e.g., `experience_postdoc_university.md`). Each achievement has:
- **Source paper** with citation
- **Methods and tools** used
- **Quantitative results**
- **Pre-written bullet variants** (2-line and 3-line)
- **Tags** for which role types this achievement is relevant to
- **Significance** context for cover letters

### Role-Type Bundles

One file per target audience (e.g., `bundle_academic.md`). Each bundle contains:
- **S1: Role Profile** — what this audience values, positioning strategy
- **S2: Summary Guide** — how to write the summary for this role type
- **S3: Achievement Reframing Map** — priority ranking of your achievements for this audience
- **S4: Skills Guide** — which tools to bold, which to include, grouping strategy
- **S5: Cover Letter Guide** — opening hooks, paragraph templates, anti-patterns

### Provenance Flags

The system enforces accuracy through provenance tracking in `config.md`. Every achievement is tagged with its publication status. The skills check this table before every output and will never:
- Claim unpublished work is published
- Claim internal tools are peer-reviewed
- Use full-ownership verbs for shared work
- Inflate author position

### The Critique System

The `/critique` skill runs an 8-part assessment:
1. **Domain-Specialist Lens** — reviewer persona, gap analysis, competitive landscape
2. **Five-Perspective Read-Through** — ATS bot, recruiter (10s), HR (30s), hiring manager (2min), technical reviewer (10min)
3. **Eight-Dimension Scoring** — weighted score out of 100
4. **Interview Likelihood** — per-reader probability estimates
5. **Tiered Improvements** — ranked by point impact
6. **Interview Bridge Points** — resume-to-interview talking points
7. **Cover Letter Critique** — 6 sub-checks
8. **Post-Generation Verification** — mechanical and content checklists

---

## What You Can Customize

### Everything in `config.md` (edit directly)

| Setting | What it controls | Example |
|---------|-----------------|---------|
| **Personal Info** | Name, email, phone, links on all outputs | Your contact details |
| **Document Preferences** | Page counts, bullet line variants, skills layout | `Resume: 2 pages, CV: 5 pages` |
| **Provenance Flags** | What claims are safe to make | `ML paper: under review → never say "published"` |
| **Role Types** | Target audiences and their bundles | `Academic (Tier 1), Industry R&D (Tier 2)` |
| **Decision Tree** | How JD keywords map to role types | `"tenure-track" → Academic` |
| **FIXED Sections** | Template sections that never change per JD | `Education, Publications, Awards` |
| **Output Rules** | Package formats and constraints | `Resume: 2pg + 1pg CL = 3pg package` |
| **KB Corrections** | Errors to never re-introduce | `Accuracy is 2.1 meV/atom, not 2.3` |

### LaTeX Templates (edit directly)

- **Fonts, colors, spacing** — modify `.cls` files
- **Section order** — reorder sections in `.tex` templates
- **FIXED content** — fill in education, awards, publications, header
- **Icons** — replace `GS.png` / `orcid.png` with your own
- **Page geometry** — adjust margins in `.cls` if needed

### Knowledge Base (built by skills, then editable)

| File | How to customize |
|------|-----------------|
| **Experience files** | Edit bullet text, add/remove achievements, adjust tags |
| **Bundles** | Change priority matrices, rewrite summary guides, add role types |
| **Skills taxonomy** | Add/remove skills, change groupings, adjust bold rules |
| **Pub metadata** | Update citation counts, add new publications |

### Reference Docs (advanced — edit if you know what you're doing)

| File | What you'd change |
|------|-------------------|
| `resume_reference.md` | Page budgets, character limits, section specs |
| `cl_reference.md` | Cover letter paragraph templates, word count targets |
| `critical_rules.md` | Generation-time rules tables |
| `critique_framework.md` | Scoring weights, critique dimensions |
| `shared_ops.md` | Session workflow, file derivation logic |

### Skill Prompts (advanced)

Each skill is a markdown file in `.claude/skills/<name>/SKILL.md`. You can:
- Add STOP points for more user control
- Change the number of web searches in Phase 0
- Adjust how many bullets per position
- Modify the critique scoring weights
- Add new skills for your workflow

---

## Skill Reference

| Skill | Purpose | Input | Output |
|-------|---------|-------|--------|
| `/setup-extract` | Extract structured data from a paper | Paper path | `knowledge_base/extractions/*.md` |
| `/setup-build-kb` | Build resume artifacts from extractions | All extractions | `resume_builder/{experience,bundles,support}/` |
| `/make-resume` | Generate tailored resume or CV | JD path | `output/<Folder>/e2e_*.tex` + session file |
| `/make-cl` | Generate matching cover letter | Session file | `output/<Folder>/*_cover_letter.tex` |
| `/edit-resume` | Edit resume/CV/CL from feedback | Session file + feedback | Updated `.tex` files |
| `/critique` | Independent quality review | Session file | `output/<Folder>/critique_*.md` |

---

## Three-Session Workflow

For best results, use a **separate Claude Code session** for each step. This gives each skill fresh context, which produces better quality (especially for critique — you want fresh eyes, not the same context that generated the resume).

```
Session 1:  /make-resume JDs/job.txt     → resume/CV .tex
            /clear
Session 2:  /make-cl                      → cover letter .tex
            /clear
Session 3:  /critique                     → critique .md with score
            /clear
            /edit-resume                  → refined .tex (if needed)
```

---

## Key Design Decisions

- **Accuracy > Relevance > Impact > ATS > Brevity** — the priority hierarchy for every generation decision
- **LaTeX-only output** — Claude generates `.tex`, you compile locally. No formatting surprises.
- **FLIPPED position format** — the bold line under each position title is a JD-customized theme, not a generic description. This is the strongest tailoring lever.
- **Structured provenance** — every achievement is tracked from source paper → extraction → experience file → resume bullet
- **Character-precise budgets** — every bullet is calibrated to fit the template geometry. No "try to keep it short."
- **Session files as state** — all decisions for a JD live in one file. Skills can recover from interruptions.
- **Anti-fabrication by design** — provenance flags, verb discipline, and corrections logs prevent overclaiming even under pressure to impress.
- **AI fingerprint avoidance** — a dedicated rules file (`resume_builder/support/ai_fingerprint_rules.md`) is loaded by all 4 generation/critique skills. It includes banned words and phrases (with technical exceptions), structural anti-patterns (e.g., excessive `-ing` bullet endings, prose em-dashes), positive markers to prefer, and a 12-item post-generation checklist. Templates use period separators instead of em-dashes in Fellowships/Honors sections to avoid a common AI tell.

---

## Examples

The `resume_builder/examples/` directory contains a complete worked example for a fictional researcher, **Dr. Jordan Chen** (computational biologist). This includes:

- `example_config.md` — filled-in configuration
- `extractions/example_extraction.md` — a paper extraction
- `experience/example_experience.md` — experience file with 11 achievements across 2 positions
- `bundles/example_bundle.md` — an Academic role-type bundle
- `example_session_file.md` — a completed session file showing the full pipeline

Study these to understand the data model before building your own knowledge base.

---

## FAQ

**Q: Do I need to know LaTeX?**
No. Claude generates the `.tex` files. You just compile them (`pdflatex file.tex`). The templates handle all formatting.

**Q: How many papers should I extract?**
All papers where you're first author or co-first author, plus key contributing-author papers. Quality matters more than quantity — 5 well-extracted papers beat 20 shallow ones.

**Q: Can I use this for non-academic roles?**
Yes. The framework supports any role type — define them in `config.md`. Industry R&D, consulting, data science, and engineering roles all work. Just create appropriate bundles.

**Q: What if I don't have a Google Scholar / ORCID?**
Remove those lines from the templates. The framework adapts to what you have.

**Q: How do I update after publishing new papers?**
Run `/setup-extract` on the new paper, then update your experience file and bundles. Existing session files are not affected.

**Q: Can I use this with resume formats other than the included templates?**
Yes. The `.cls` files define the visual style. You can modify them or write your own. The skills generate content based on the template structure — update the `[GENERATE: ...]` and `[FIXED: ...]` markers in your template.

**Q: How long does the initial setup take?**
Depends on how many papers you have. Expect ~10 minutes per paper for extraction, then ~30 minutes for `/setup-build-kb` to synthesize everything. After that, each new JD takes about 15-20 minutes across all three sessions.

**Q: Can multiple people use the same kit?**
Each person needs their own clone with their own `config.md`, knowledge base, and templates. The framework itself is shared; the content is personal.

**Q: What Claude model should I use?**
The skills are designed for Claude's most capable models (Opus, Sonnet). Less capable models may skip steps or produce lower-quality output.

---

## Contributing

Issues and PRs welcome. If you find a bug in the skill prompts, critique framework, or templates, please open an issue.

When contributing, keep in mind:
- The example files use the fictional Dr. Jordan Chen — keep examples in that persona
- Reference docs should stay domain-agnostic (no field-specific examples)
- Test skill changes against the example data before submitting

---

## License

MIT — see [LICENSE](LICENSE).
