---
description: Re-critique existing resume/CV output files against a JD
user-invocable: true
disable-model-invocation: true
---

# /critique

**User input:** `$ARGUMENTS`

Parse `$ARGUMENTS`:
- Session file path (e.g., `output/Acme/session_acme_engineer.md`) → read session file, derive .tex paths from Output Files
- .tex file path(s) + JD source (existing format) → backward compatible
- Session name (e.g., `acme_engineer`) → find session file via derivation

If no CL .tex provided or found in session file, critique resume/CV alone (Part 7 adjustments noted below).

---

## Safety Rules

**Accuracy > Relevance > Impact > ATS > Brevity**

Read `config.md` Provenance Flags. Verify every claim against that table.
Check `config.md` KB Corrections Log — do not flag corrected items as errors.
Use the email from `config.md` Personal Info — flag if a different email appears in output.
FIXED sections (from `config.md` FIXED Sections) are template-locked — do not flag for editing. Flag only VARIABLE sections.

---

## User Input During Execution

If the user provides feedback, corrections, or suggestions at any point:
1. Acknowledge the input immediately
2. If it changes scoring criteria or focus: adjust the critique accordingly
3. Never restart — resume from current position

---

## Startup

Read `resume_builder/reference/shared_ops.md` — Fresh Session Startup + Session File Derivation.
Read `CLAUDE.md` — check Active Sessions and KB Corrections.
Read `config.md` — load Provenance Flags, FIXED Sections, email.
Find and read the session file for the .tex being critiqued (use derivation protocol from shared_ops.md).

**Recovery check:**
- If CL not DONE in session file → "CL not yet generated. Run `/make-cl` first."
- If Critique: CURRENT → "Already critiqued (score X/100). Re-run? Waiting for confirmation."
- If Critique: STALE → "Edits made since last critique. Re-critiquing."
- If Critique: PENDING → proceed

---

## Protocol

1. **Read session file** — specifically note:
   - **Company Context** → reviewer persona, "why this company"
   - **Framing Strategy** → intentional reframing decisions (flag only execution inconsistencies, not the strategy itself)
   - **Cover Letter Plan** → CL structure rationale
   - **Critique Context** → reviewer persona, competitive landscape, domain vocabulary
   - If session file lacks Company Context or Critique Context: do 1-2 web searches to fill gaps
2. Read `resume_builder/reference/critique_framework.md`
3. Read `resume_builder/support/ai_fingerprint_rules.md` — use Section 6 checklist in Part 7 verification
3. Read the .tex file(s) — derive paths from session file Output Files, or from `$ARGUMENTS`
4. Read the JD (path from `$ARGUMENTS` or session file)
5. Read the relevant bundle (`resume_builder/bundles/bundle_[role_type].md` — from session file)
6. Run char count:
   ```bash
   python3 resume_builder/helpers/char_count.py -f [resume|cv] [file.tex]
   ```
7. Compile and visually verify:
   ```bash
   pdflatex -interaction=nonstopmode -output-directory=output/<FolderName> [file.tex]
   ```
   Use the Read tool to view the compiled PDF — check orphans, page fill, header wrapping.
   If compile fails: note "COMPILE FAILED — visual checks could not be verified" in Part 8.
8. If a prior critique exists (`output/<FolderName>/critique_<name>.md`): read it and note previous score.
8b. **Paper Hook Verification:** If the CL cites named papers, PIs, programs, or publications, web-search to verify title, journal, year, and PI affiliation. Flag factual errors as Tier 1 fixes.

9. **Run the full critique per critique_framework.md. The output MUST contain ALL 8 sections** (even if the framework file has partially compacted, produce every section):

    1. **Domain-Specialist Lens** — 7 elements:
       (a) Reviewer persona (b) Company context (c) JD vocabulary extraction (d) Domain vocabulary map
       (e) Gap ranking (fatal/serious/cosmetic) (f) Methodology transfer test (g) Competitive landscape
    2. **Five-Perspective Read-Through** — ATS, Recruiter (10s), HR (30s), HM (2min), Technical (10min) — each with verdict
    3. **Eight-Dimension Scoring** — weighted table summing to 100
       (ATS 15%, Summary 10%, Skills 10%, Bullets 25%, Publications 10%, Narrative 15%, Visual 5%, Credibility 10%)
    4. **Interview Likelihood** — per-reader probability + ceiling analysis
    5. **Tiered Improvements** — Tier 1 (>=1pt each), Tier 2 (0.3-0.9), Tier 3 (<0.3)
    6. **Interview Bridge Points** — 5-7 resume-to-interview talking points
    7. **Cover Letter Critique** — 6 sub-checks (6A anti-patterns, 6B tailoring, 6C context-specific, 6D ATS, 6E structural, 6F package cohesion)
       - **If no CL provided:** Skip 6A-6E. Run 6F as resume standalone assessment — evaluate whether the resume earns an interview without a CL. Note: "Cover letter not provided — package cohesion not assessed."
    8. **Post-Generation Verification** — mechanical + content + structural checklists

10. Save to `output/<FolderName>/critique_<name>.md`
11. **Update session file** — Critique Summary (score, findings, tier 1 fixes), Status → Critique: CURRENT
12. **Update memory pointer** with new score

Progress: "Reading session file for framing context..." / "Running ATS keyword scan — 16/20 match..." / "Scoring 8 dimensions..." / "Score: 87.0/100"

### >>>>>> MANDATORY STOP <<<<<<
Present: score table + tier 1 actionable fixes + interview likelihood.
**You MUST wait for the user's explicit text response before continuing.**
If edits needed, tell user to run `/edit-resume`.

### When user approves / says "looks good" / finalizes:
Verify all expected files exist in `output/<FolderName>/`:
- session file, resume/CV .tex + .pdf, CL .tex + .pdf, critique .md
- Compile artifacts (.aux, .log, .out)
Confirm to user: "Package complete in output/<FolderName>/ — [list files]"
