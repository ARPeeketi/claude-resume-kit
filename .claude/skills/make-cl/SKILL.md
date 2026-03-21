---
description: Generate a tailored cover letter from an existing session file and finished resume/CV
user-invocable: true
disable-model-invocation: true
---

# /make-cl

**User input:** `$ARGUMENTS`

Parse `$ARGUMENTS`:
- Session file path (e.g., `output/Acme/session_acme_engineer.md`) → read that session file
- Session name (e.g., `acme_engineer`) → find session file via shared_ops.md derivation
- Empty → check `CLAUDE.md` Active Sessions for latest

---

## Safety Rules (ALWAYS ENFORCED)

**Accuracy > Relevance > Impact > ATS > Brevity**

Read `config.md` Provenance Flags before generating any content. Verify every claim against that table.

- Use the email from `config.md` Personal Info in all outputs
- CL deepens what resume presents — never introduces new claims not traceable to resume bullets
- Source field context from `resume_builder/support/significance_*.md` files

---

## User Input During Execution

If the user provides feedback, corrections, or suggestions at any point:
1. Acknowledge the input immediately
2. If it affects already-written content: fix it, re-verify word count and anti-patterns
3. If it changes the framing: note the change in session file Framing Strategy
4. Never restart — resume from current position

---

## Startup

Read `resume_builder/reference/shared_ops.md` for session startup and file derivation.

Then:
1. Read `CLAUDE.md` — check Active Sessions and KB Corrections
2. Read `config.md` — load Provenance Flags, email, role types
3. Find and read the session file
4. **Recovery check:**
   - If CL Status is DONE → "CL already generated. Run `/critique` next." Show next command. Stop.
   - If CL Status is IN_PROGRESS → check if CL .tex exists, offer to resume or regenerate
   - If Resume Status is not DONE → "Resume not yet generated. Run `/make-resume` first." Stop.
   - If CL Status is PENDING → proceed to Phase 1

---

## Phase 1: Load Context

Read in this order:
1. **Session file** — specifically: Company Context, Cover Letter Plan, Framing Strategy, ATS Keywords
2. **Finished resume/CV .tex** — path from session file Output Files. Read to understand what CL must complement.
3. `resume_builder/reference/cl_reference.md` — CL format rules, paragraph templates, anti-patterns
4. `resume_builder/support/ai_fingerprint_rules.md` — Banned words, structural rules (CLs are most vulnerable)
5. The matching bundle from session file role type → `resume_builder/bundles/bundle_[role_type].md` — Section 5 (Cover Letter)
5. All significance files from `resume_builder/support/significance_*.md`

Update session file Status: `Cover Letter: IN_PROGRESS`

Progress: "Loading CL context — [company], [role type] bundle, [institution type]..."

---

## Phase 2: Generate Cover Letter

Read `resume_builder/templates/coverletter_template.tex`.

**Detect institution type** from session file Cover Letter Plan:
- Industry → 3 paragraphs, 250-300 words
- National Lab → 4 paragraphs, 350-450 words
- Academic → 4 paragraphs, 350-450 words (postdoc) or 450-650 words (faculty)

**Generate CL following cl_reference.md paragraph structure:**
- Use significance files for field-context depth (NOT resume bullet text)
- Use session file CL hooks and "why them" angle
- Ensure every major claim is traceable to a resume/CV bullet
- Open with a specific reference to their work — no generic openers
- Weave credentials into body paragraphs, not closing

Save to `output/<FolderName>/e2e_<name>_cover_letter.tex`

Progress: "Writing [institution type] cover letter — [N] paragraphs, targeting [N] words..."

### CL Hook Verification Gate (MANDATORY before presenting to user)

Web-search every hook used in the CL:
- Academic: PI name + cited paper/research area
- National Lab: named program, thrust area, or group publication
- Industry: product, technology, or company news referenced

Present evidence as:
> **Claim:** [what the CL says] → **Evidence:** [what the search found] → **Source:** [URL]

Flag any unverified item: **"UNVERIFIED — please confirm"**

Do NOT present the CL draft to the user until all hooks are verified or flagged.

---

## Phase 3: Compile & Verify

```bash
pdflatex -interaction=nonstopmode -output-directory=output/<FolderName> output/<FolderName>/e2e_<name>_cover_letter.tex
```

Use Read tool to view compiled PDF. Verify:

| Gate | Check | If FAIL |
|------|-------|---------|
| Word count | Industry 250-300, Lab/Academic 350-450 | Trim/expand |
| Page count | Resume package: 1 page. CV package: 1-2 pages | Adjust content |
| Page fill | 1pg: well-filled. 2pg: page 2 >= half filled before signature | Adjust |
| Anti-patterns | No generic opener, no defensive framing, no credential dump | Rewrite |
| Package cohesion | CL claims traceable to resume bullets, no contradictions | Fix |
| Compile | Clean pdflatex | Fix LaTeX errors |

Update session file:
- Add CL to Output Files
- Status: `Cover Letter: DONE`
- Add Next Critique command

Progress: "Compiled — 1 page, 278 words. Package cohesion verified."

### >>>>>> MANDATORY STOP — DO NOT PROCEED <<<<<<
Present: CL summary (word count, page count, key hooks used).
**You MUST wait for the user's explicit text response before continuing.**

If user requests changes: apply them, re-compile, re-verify. Update session file.
If user approves: update Status, present next command.

**Do NOT trigger file organization** — that happens after `/critique` approval.

"Cover letter done. Next steps:
1. /clear
2. [exact /critique command with session file path]"
