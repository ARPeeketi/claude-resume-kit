---
description: Edit existing resume/CV or cover letter from critique feedback and user suggestions
user-invocable: true
disable-model-invocation: true
---

# /edit-resume

**User input:** `$ARGUMENTS`

Parse `$ARGUMENTS`: First argument is the .tex file path (required). A `.md` path is the critique file. Text in quotes is inline instructions.
- `/edit-resume output/Acme/e2e_acme_resume.tex`
- `/edit-resume output/Acme/e2e_acme_resume.tex output/Acme/critique_acme.md`
- `/edit-resume output/Acme/e2e_acme_resume.tex "shorten Position 1 header, fill last page"`

If only .tex path and no instructions: ask the user what to fix.

---

## Safety Rules (ALWAYS ENFORCED)

**Accuracy > Relevance > Impact > ATS > Brevity**

Read `config.md` Provenance Flags before editing any content. Verify every claim against that table.

- Use the email from `config.md` Personal Info in all outputs
- Source ALL bullet content from `resume_builder/experience/` files. Never fabricate.
- Resume bullets: ALL variable bullets must be 2L (CV: 2L/3L mix OK, check `config.md` Document Preferences)
- Run `python3 resume_builder/helpers/char_count.py` after edits — the tool is authoritative

### FIXED Sections — Refuse if Asked to Edit
Check `config.md` FIXED Sections for the list of template-locked sections. Say no and explain: these are template-locked across all outputs.

VARIABLE sections only: Summary, Technical Skills, Research Experience bullets/headers.

---

## User Input During Execution

If the user provides feedback, corrections, or suggestions at any point:
1. Acknowledge the input immediately
2. If it affects an already-applied edit: go back, fix it, re-run char count gate
3. If it changes the edit plan: update session file, adjust remaining edits
4. If it's a question: answer it, then continue from current step
5. Never restart a phase — resume from current position

---

## Startup

Read `resume_builder/reference/shared_ops.md` — Fresh Session Startup + Session File Derivation.
Read `CLAUDE.md` — check Active Sessions and KB Corrections.
Read `config.md` — load Provenance Flags, email, FIXED Sections, document preferences.
Find and read the session file (use derivation protocol from shared_ops.md).

**Recovery check:**
- Read session file, check for existing Edit N Status
- If Edit N Status shows IN_PROGRESS: read .tex, identify which edits are done, resume
- If no edit in progress: proceed to Phase 1

---

## Phase 1: Load Context

Read in this order:
1. **Session file** (`output/<FolderName>/session_<name>.md`) — note: Framing Strategy, Company Context, Bullet Plan, Edit History
2. `resume_builder/reference/resume_reference.md` — char limits, budgets, fixed sections
3. The .tex file being edited
4. Critique file (if provided in `$ARGUMENTS`)
5. JD file (path from session file's JD Info section)
6. Compile current .tex and record baseline page count
7. Run: `python3 resume_builder/helpers/char_count.py -f [resume|cv] [file.tex]`

**Record baseline in session file** under `## Edit [N] Baseline` (scan existing Edit History sections; next N = max existing + 1, or 1 if none):

```
## Edit [N] Baseline
- Pages: [N]
- Char violations: [list or "none"]
- Orphan violations: [list or "none"]
- White space last page: [N lines]
- Variable bullets: [N]
- Rendered lines: [N]
```

Progress: "Reading session file — [company], [role type] bundle..." / "Baseline: 2 pages, 0 char violations, 1 orphan..."

---

## Phase 2: Diagnose & Plan Edits

Gather change requests from THREE sources:
1. **User instructions** from `$ARGUMENTS` (highest priority)
2. **Critique file** (Tier 1 fixes first, then Tier 2)
3. **Auto-detected issues** from Phase 1 (char violations, orphans, page fill)

Cross-check against **session file framing strategy** — edits must stay consistent with decisions from `/make-resume`.

**For each change, classify:**
- **MODIFY:** Change text of existing bullet/summary/skills. Budget unchanged.
- **SWAP:** Replace one bullet with another. Budget unchanged if same variant.
- **ADD:** Insert new bullet. Budget increases by rendered lines.
- **REMOVE:** Drop a bullet. Budget decreases.
- **VARIANT CHANGE:** e.g., 2L → 3L. Budget changes by rendered line delta.
- **FIXED:** Blocked — show in plan with `[FIXED — cannot edit]` and explain why.

**Budget revalidation (if any change is ADD, REMOVE, SWAP-with-different-variant, or VARIANT CHANGE):**
Recalculate total variable bullets and rendered lines. Compare against budget from resume_reference.md.
If OVER budget: present overflow and ask user which bullet to drop or shorten.
Show: `Budget: [N] bullets ([M] rendered lines) vs target [T]. PASS/FAIL`

If edit targets **cover letter** (not resume/CV): note this — Phase 4 will use CL-specific gates. Load CL .tex path from session file Output Files section.

### >>>>>> MANDATORY STOP — DO NOT PROCEED <<<<<<
Present numbered edit plan. Each item shows: what, why, source, classification (MODIFY/ADD/SWAP/FIXED).
**You MUST wait for the user's explicit text response before continuing.**
Proceeding without confirmation may make unwanted edits that break package consistency.

---

## Phase 3: Load Reference Files (only confirmed edits)

Load ONLY what the confirmed edits need:

- **All edits:** `resume_builder/support/ai_fingerprint_rules.md` — scan for banned words/patterns before and after edits
- **Bullet expand/rewrite/add:** `resume_builder/experience/` files + matching bundle + `resume_builder/support/achievement_reframing_guide.md`
- **Summary rewrite:** Bundle (S2 summary guide) + `resume_builder/support/skills_taxonomy.md`
- **Cover letter edits:** `resume_builder/support/significance_*.md` + `resume_builder/reference/cl_reference.md`
- **Simple fixes** (orphans, headers, spacing): No extra files needed

---

## Phase 4: Execute Edits

Apply edits one section at a time. After each edited section:

1. Run char count gate:
   ```bash
   python3 resume_builder/helpers/char_count.py -f [resume|cv] output/<FolderName>/[file].tex
   ```
2. Fix any OVER violations or orphans before next section
3. If a bullet expansion doesn't render as expected (1L when targeting 2L, or 3L), adjust immediately

Update session file Edit N Status after each individual edit:
- Edit 1 (orphan fix): DONE
- Edit 2 (Summary rewrite): IN_PROGRESS

### Resume/CV Verification Gates
| Gate | Check | If FAIL |
|------|-------|---------|
| Char count | No OVER violations | Fix bullet before proceeding |
| Page fill | Resume: <= 3 lines white space. CV: check rendered line target | Expand/trim variable bullets |
| Page count | Match `config.md` Document Preferences | Trim/expand variable content |
| Orphan | 2L bullet last line >= 70% | Pad or trim |
| Title width | Position title + date fits 1 line | Shorten title |
| Compile | Clean pdflatex | Fix LaTeX errors |

### Cover Letter Verification Gates (if CL was edited)
| Gate | Check | If FAIL |
|------|-------|---------|
| Word count | Industry 250-300, Lab/Academic 350-450 | Trim/expand |
| Page fill | 1pg: well-filled. 2pg: page 2 >= half filled before signature | Adjust |
| Paragraph count | Industry 3, Lab/Academic 4 | Restructure |
| Anti-patterns | No generic opener, no defensive framing, no credential dump | Rewrite |
| Package cohesion | CL claims traceable to resume bullets, no contradictions | Fix |

After all edits, compile:
```bash
pdflatex -interaction=nonstopmode -output-directory=output/<FolderName> output/<FolderName>/[file].tex
```
Use the Read tool to view the compiled PDF — check page count, white space, orphans, header wrapping.

Progress: "Editing Position 1 bullet 6 — was 184 chars, now 197..." / "Compiling... 2 pages, page fill OK"

---

## Phase 5: Update Session File & Present

1. **Append Edit History** (use the N from Phase 1 baseline):
   ```
   ### Edit [N] ([date]): [short description]
   - Changes: [what changed]
   - Source: critique item # / user request / auto-detected
   - Verification: gates passed
   ```

2. **Compare against baseline:**

   | Metric | Before | After | Delta |
   |--------|--------|-------|-------|
   | Page count | [N] | [N] | [+/-] |
   | Char violations | [N] | [N] | [+/-] |
   | Orphans | [N] | [N] | [+/-] |
   | White space | [N] | [N] | [+/-] |

   Flag any metric that worsened.

3. **Update Status** — mark critique as STALE if edits made after last critique. Update Next.

4. **Update memory pointer** if status changed.

5. **Present:** Changes summary + delta table + compiled PDF.

### >>>>>> MANDATORY STOP <<<<<<
Show results. Wait for user approval or further edits.
**You MUST wait for the user's explicit text response before continuing.**

### When user approves / says "looks good" / finalizes:
Run file organization from `resume_builder/reference/shared_ops.md` — Finalization check.
