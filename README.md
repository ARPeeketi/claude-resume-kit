# claude-resume-kit

Most AI resume tools work the same way: paste resume + paste JD, get a rewrite. They don't know which of your papers is published vs. under review. They don't know you only ran the simulations, not the experiments. They'll upgrade "contributed to" into "developed" without blinking.

This is different. You extract your papers, codebases, and reports once — the system asks structured questions about each one. After that, every new application is just pointing it at a JD. It picks the right achievements, frames them for the audience, enforces accuracy, and generates LaTeX you compile locally.

Built for researchers and engineers with lots of source material (papers, code, reports) who apply to many positions across different employer types.

---

## What makes this different

**Knowledge base, not a rewriter.** You extract once. Every application draws from verified source material — not a pasted resume that gets "improved."

**Anti-fabrication by design.** Provenance flags on every achievement (published / under review / internal). Verb discipline rules prevent overclaiming. A corrections log ensures fixed errors don't reappear.

**AI fingerprint avoidance.** Banned-word lists, structural anti-patterns, and a 12-item post-generation scan so output reads as human-written.

**Multi-perspective critique.** Five reader personas (ATS bot through technical reviewer) score your resume across 8 dimensions in a fresh context window.

**LaTeX output, locally compiled.** No data leaves your machine beyond the Claude Code conversation.

---

## Example Output

Here's what the system generates for the included fictional researcher (Dr. Jordan Chen, computational biologist) applying to a tenure-track faculty position:

- [Example Resume (PDF)](resume_builder/examples/example_resume.pdf) — 2-page resume with JD-tailored bullets, skills, and publications
- [Example Cover Letter (PDF)](resume_builder/examples/example_cover_letter.pdf) — 1-page academic cover letter with specific hooks
- [Example Session File](resume_builder/examples/example_session_file.md) — the decision log that produced this output
- [Source .tex files](resume_builder/examples/output/) — the LaTeX source Claude generated

All example data is in `resume_builder/examples/` — extraction, experience file, bundle, config, and session file.

---

## What you actually do

**One-time setup (~10 min per paper):**
1. Drop your papers/reports into `knowledge_base/papers/`
2. Run `/setup-extract` on each — Claude reads it and asks you questions about your contributions and publication status
3. Run `/setup-build-kb` — synthesizes everything into your knowledge base

**Per application (~15-20 min):**
1. Drop the JD into `JDs/`
2. Run `/make-resume JDs/target_job.txt` — approve the bullet plan, get a `.tex` file
3. Run `/make-cl` for a cover letter
4. Run `/critique` for a scored review with specific fixes

Each step uses a **separate Claude Code session** for best quality (fresh context = less bias).

---

## Prerequisites

- **[Claude Code](https://docs.anthropic.com/en/docs/claude-code)** CLI installed and authenticated
- **A LaTeX distribution** for compiling `.tex` to `.pdf` (e.g., [TeX Live](https://tug.org/texlive/), [MacTeX](https://tug.org/mactex/), [MiKTeX](https://miktex.org/))
- **Your research papers** or project documentation ready for extraction

---

## Try it first (5 minutes)

Want to see what it does before extracting your own papers? The repo includes a complete example knowledge base for a fictional researcher:

```bash
git clone https://github.com/ARPeeketi/claude-resume-kit.git
cd claude-resume-kit
claude
/make-resume JDs/example_jd.txt
```

This runs the full pipeline — JD analysis, bullet selection, LaTeX generation — using the included example data. No setup required.

---

## Full Setup

### 1. Clone and configure

```bash
git clone https://github.com/ARPeeketi/claude-resume-kit.git
cd claude-resume-kit
```

Edit `config.md` with your details (name, email, provenance flags, role types). See `resume_builder/examples/example_config.md` for a complete example.

### 2. Extract your papers

## Research Focused

Place PDFs or `.tex` source files in `knowledge_base/papers/`, then:

```
/setup-extract knowledge_base/papers/my_paper.pdf
```

Claude reads the paper, asks clarifying questions about your contributions, and creates a structured extraction. Repeat for each paper.

## Industry Focused

Place PDFs from your Tailored Resumes or place your resume in `knowledge_base/industry, then: 

```
/setup-industry-extract knowledge_base/papers/my_paper.pdf
```
Claude reads the resumes, asks clarifying questions about your work, and creates a structured extraction. No Need to repeat for each resume.

### 3. Build your knowledge base

## Research Focused

```
/setup-build-kb
```

## Industry Focused

```
/setup-build-industry-kb
```

This synthesizes all extractions into experience files, role-type bundles, and support files.

### 4. Customize your LaTeX templates

Open the templates in `resume_builder/templates/` and fill in your FIXED sections — education, header, awards, publications. The `[CONFIG: ...]` placeholders show you what to fill in.

### 5. Generate for a job

```
/make-resume JDs/target_job.txt
```

Then in separate sessions: `/make-cl` for the cover letter, `/critique` for a scored review.

---

## How It Works

```
Your Papers --> /setup-extract --> Extractions --> /setup-build-kb --> Knowledge Base
                                                                          |
Job Description --> /make-resume --> Tailored Resume/CV (.tex)            |
                        |              v                                  |
                   /make-cl --> Cover Letter (.tex)                       |
                        |              v                                  |
                   /critique --> 8-Part Score + AI Scan + Fixes           |
                        |              v                                  |
                   /edit-resume --> Refined Package                       |
```

| Skill | Purpose | Input | Output |
|-------|---------|-------|--------|
| `/setup-extract` | Extract structured data from a paper | Paper path | `knowledge_base/extractions/*.md` |
| `/setup-industy-extract` | Extract structured data from resumes | Resume path | `knowledge_base/extractions/*.md` |
| `/setup-build-kb` | Build KB from extractions | All extractions | `resume_builder/{experience,bundles,support}/` |
| `/setup-build-industry-kb` | Build KB from extractions | All extractions | `resume_builder/{experience,bundles,support}/` |
| `/make-resume` | Generate tailored resume or CV | JD path | `output/<Folder>/e2e_*.tex` + session file |
| `/make-cl` | Generate matching cover letter | Session file | `output/<Folder>/*_cover_letter.tex` |
| `/edit-resume` | Edit resume/CV/CL from feedback | Session + feedback | Updated `.tex` files |
| `/critique` | Independent quality review | Session file | `output/<Folder>/critique_*.md` |

---

## Documentation

For architecture details, customization tables, the full critique system breakdown, key design decisions, and FAQ, see **[DOCS.md](DOCS.md)**.

---

## Contributing

Issues and PRs welcome. When contributing:
- Example files use the fictional Dr. Jordan Chen — keep examples in that persona
- Reference docs should stay domain-agnostic
- Test skill changes against the example data before submitting

---

## License

MIT — see [LICENSE](LICENSE).
