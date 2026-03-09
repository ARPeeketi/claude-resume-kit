<!-- NOTE: Example bullets below show em-dashes (---) for parenthetical breaks. -->
<!-- In actual generation, limit to max 2 em-dashes per full document. -->
<!-- Prefer commas, semicolons, or parentheses for mid-bullet breaks. -->

# Position: Postdoctoral Research Associate at Lakewood University

## Dates: Aug 2023 -- Present

## Cross-Position Themes (for cover letters)
- Research trajectory: classical protein simulation (PhD) to ML-accelerated protein engineering (postdoc)
- Recurring architecture pattern: experimental data -> ML surrogate -> large-scale computational screening
- Consistent focus: protein stability and folding thermodynamics throughout career

---

## Achievements

### L1: ML-Guided Enzyme Stability Screening
**Source:** Chen et al., ACS Catalysis 2025
**Methods:** ESM-2 protein language model, GROMACS, replica exchange MD, Python/BioPython
**Quantitative:** 0.82 Spearman on stability prediction, 3,000x throughput vs experiment, 8,500 variants screened, 5 confirmed hits
**Bullet (2L):** Fine-tuned ESM-2 protein language model on 45K experimental melting temperatures, achieving 0.82 Spearman correlation and enabling 3,000$\times$ throughput screening of 8,500 enzyme variants for industrial thermostability.
**Bullet (3L):** Fine-tuned ESM-2 protein language model on 45K experimental melting temperatures with transfer learning, achieving 0.82 Spearman correlation and 3,000$\times$ throughput over experimental screening --- identified 7 thermostable lipase variants with 15$+$ $^\circ$C stability gain, 5 experimentally confirmed via differential scanning calorimetry.
**Tags:** academic, industry_rd
**Significance:** Demonstrates independent ML pipeline development and protein engineering impact. 3,000x speedup is a concrete metric. Published first-author in high-impact journal.

### L2: Enzyme Solvent Tolerance Prediction
**Source:** Chen, Yamamoto, Holmberg, Proteins: Structure, Function, and Bioinformatics 2025 (under review)
**Methods:** ESM-2 fine-tuning, GROMACS, explicit solvent MD, MM/PBSA free energy
**Quantitative:** 0.78 Spearman on solvent tolerance, 50-ns MD of 80 enzyme-solvent systems, 4 solvent-tolerant variants identified
**Bullet (2L):** Extended protein language model to predict enzyme solvent tolerance across 8 organic co-solvent systems, validating against 50-ns explicit-solvent MD for 80 enzyme variants and identifying 4 candidates for green chemistry applications.
**Bullet (3L):** Extended protein language model to predict enzyme solvent tolerance across 8 organic co-solvent systems (0.78 Spearman on held-out set) validated against 50-ns explicit-solvent molecular dynamics free energy calculations for 80 enzyme variants --- identified 4 solvent-tolerant lipase candidates now under experimental characterization for green chemistry applications.
**Tags:** academic, industry_rd
**Significance:** Deepens enzyme engineering expertise into industrial conditions. Natural extension of thermostability work. Under-review status must be stated clearly.

### L3: Automated Screening Pipeline
**Source:** Internal infrastructure project (unpublished)
**Methods:** Python, Snakemake, SLURM, GROMACS automation, PostgreSQL
**Quantitative:** Automated sequence-to-simulation pipeline for 6 researchers, reduced per-variant setup from 4 hours to 10 minutes
**Bullet (2L):** Automated sequence-to-simulation computational pipeline using Snakemake workflow manager, reducing per-variant setup from 4 hours to 10 minutes and supporting 6 researchers across 3 active projects.
**Bullet (3L):** Designed and deployed automated sequence-to-simulation pipeline integrating AlphaFold2, GROMACS, and Snakemake with SLURM job scheduling --- reduced per-variant computational setup from 4 hours to 10 minutes and currently supports 6 researchers across 3 active protein engineering projects.
**Tags:** academic, industry_rd
**Significance:** Demonstrates software engineering and team-enabling skills beyond pure research. "6 researchers" shows collaborative impact. Unpublished -- never imply this is peer-reviewed.

### L4: Transfer Learning Framework for Protein Properties
**Source:** Chen, Rivera, Holmberg, Bioinformatics 2024
**Methods:** ESM-2 embeddings, regression heads, active learning, Python/PyTorch
**Quantitative:** 60% less labeled data needed, benchmarked on 5 protein families, open-source release (200+ GitHub stars)
**Bullet (2L):** Co-developed transfer learning framework from protein language models reducing labeled training data by 60\% across 5 enzyme families, released as open-source tool with 200+ GitHub stars.
**Bullet (3L):** Co-developed transfer learning framework leveraging ESM-2 protein language model embeddings with task-specific regression heads, reducing labeled training data requirements by 60\% across 5 enzyme families --- released as open-source Python package adopted by 4 external research groups (200+ GitHub stars).
**Tags:** academic, industry_rd
**Significance:** Open-source impact is strong evidence of community value. "Co-developed" verb is mandatory (shared with M. Rivera). GitHub stars provide external validation metric.

### L5: Enzyme Unfolding Pathway Analysis
**Source:** Chen et al., ACS Catalysis 2025 (same paper as L1, secondary result)
**Methods:** Replica exchange MD, hydrogen bond analysis, principal component analysis, MDAnalysis
**Quantitative:** 200-ns trajectories at 300--400 K for 14 variants, discovered unfolding pathway divergence at 340 K
**Bullet (2L):** Revealed sequence-dependent enzyme unfolding pathway divergence at 340 K through 200-ns replica exchange MD simulations, identifying stabilizing salt bridge networks that informed rational design criteria.
**Bullet (3L):** Revealed sequence-dependent unfolding pathway divergence in 14 lipase B variants through 200-ns replica exchange MD at 300--400 K, discovering critical conformational transition at 340 K and mapping stabilizing salt bridge networks that established rational design criteria for next-generation thermostable enzymes.
**Tags:** academic
**Significance:** Shows ability to extract mechanistic insight from large-scale simulations, not just run them. Salt bridge analysis is an actionable design metric.

### L6: Mentorship and Collaboration
**Source:** Group activities (ongoing)
**Methods:** N/A
**Quantitative:** Mentored 3 graduate students, 1 co-authored publication, organized weekly group seminar
**Bullet (2L):** Mentored 3 graduate students on protein ML pipelines and MD simulation workflows, with 1 student co-authoring a peer-reviewed publication within 8 months of joining.
**Bullet (3L):** Mentored 3 graduate students on protein language models, MD simulation best practices, and HPC workflows --- 1 student co-authored peer-reviewed publication within 8 months; organized weekly computational biology seminar attended by 12 group members across 2 research groups.
**Tags:** academic
**Significance:** Mentorship evidence is critical for faculty positions. Concrete outcome (co-authored pub) is stronger than vague "guided students."

---
---

# Position: Ph.D. Researcher at Westfield Institute of Technology

## Dates: Aug 2018 -- Jul 2023

## Cross-Position Themes (for cover letters)
- Foundation in classical biomolecular simulation before pivoting to ML-accelerated methods
- Built core MD and free energy skills that underpin postdoc's ML protein engineering work
- Dissertation: "Enhanced Sampling Methods for Protein Folding and Ligand Binding Thermodynamics"

---

## Achievements

### P1: Enhanced Sampling for Protein Folding
**Source:** Chen, Alvarez, J. Chem. Theory Comput. 2022
**Methods:** Metadynamics, GROMACS, collective variable design, Python
**Quantitative:** Characterized folding free energy landscapes for 6 small proteins, predicted folding temperatures within 8 K of experiment
**Bullet (2L):** Developed metadynamics-based enhanced sampling protocol for protein folding free energy landscapes, predicting folding temperatures within 8 K of experiment across 6 small proteins.
**Bullet (3L):** Developed metadynamics-based enhanced sampling protocol for protein folding using GROMACS, designing collective variables to capture folding reaction coordinates across 6 small proteins --- predicted folding temperatures within 8 K of experimental circular dichroism measurements, establishing computational screening protocol for protein stability.
**Tags:** academic, industry_rd
**Significance:** Dissertation flagship result. Shows deep MD expertise predating the ML pivot. "Within 8 K" is a concrete validation metric.

### P2: Force Field Benchmarking for Intrinsically Disordered Proteins
**Source:** Chen, Alvarez, Kowalski, J. Chem. Theory Comput. 2021
**Methods:** GROMACS (CHARMM36m, AMBER ff19SB, OPLS-AA/M), convergence testing, statistical analysis
**Quantitative:** Benchmarked 4 force fields on 15 disordered protein sequences, established CHARMM36m as optimal for IDP ensembles
**Bullet (2L):** Benchmarked 4 protein force fields on 15 intrinsically disordered protein sequences, establishing CHARMM36m as the optimal choice for IDP conformational ensemble prediction with 40\% better agreement with SAXS data.
**Bullet (3L):** Benchmarked 4 protein force fields (CHARMM36m, AMBER ff19SB, OPLS-AA/M, a99SB-disp) on 15 intrinsically disordered protein sequences and NMR chemical shift data, establishing CHARMM36m as optimal for IDP ensembles --- 40\% better agreement with experimental SAXS profiles while maintaining comparable computational cost.
**Tags:** academic, industry_rd
**Significance:** Systematic benchmarking shows methodological rigor. Force field selection expertise is broadly applicable. Good for academic positions.

### P3: Ligand Binding Free Energy Calculations
**Source:** Chen, Alvarez, J. Med. Chem. 2023
**Methods:** Free energy perturbation (FEP), GROMACS, PMX for alchemical transformations, enhanced sampling
**Quantitative:** Calculated relative binding free energies for 40 congeneric ligand pairs, RMSE of 0.9 kcal/mol vs experiment
**Bullet (2L):** Calculated relative binding free energies for 40 congeneric ligand pairs via free energy perturbation, achieving 0.9 kcal/mol RMSE against experimental IC50 data across 3 drug target families.
**Bullet (3L):** Calculated relative binding free energies for 40 congeneric ligand pairs across 3 drug target families using free energy perturbation with enhanced sampling in GROMACS --- achieved 0.9 kcal/mol RMSE against experimental IC50 data, enabling prospective ranking of 12 novel candidates for medicinal chemistry follow-up.
**Tags:** academic, industry_rd
**Significance:** Shows drug discovery application of simulation skills. FEP is a high-demand technique. Complements the protein-focused work of the postdoc.

### P4: Protein Stability Database and Analysis Pipeline
**Source:** Chen, Kowalski, Alvarez, Bioinformatics 2021
**Methods:** Python, PostgreSQL, BioPython, statistical analysis, automated data curation
**Quantitative:** Curated 12,000 experimental melting temperatures from 3 databases, built analysis pipeline, used by 8 lab members
**Bullet (2L):** Built curated protein thermostability database integrating 12,000 experimental melting temperatures from 3 public sources, with automated quality filters adopted by 8 lab members for ML training set construction.
**Bullet (3L):** Built curated protein thermostability database integrating 12,000 experimental melting temperatures from ProTherm, FireProtDB, and Meltome Atlas with automated quality filters and outlier detection --- adopted by 8 lab members for ML training set construction and directly enabled postdoctoral ESM-2 fine-tuning work.
**Tags:** academic
**Significance:** Infrastructure work that enabled later ML research. Shows data engineering skills. Directly connects PhD to postdoc research arc.

### P5: Teaching and Outreach
**Source:** Department records (2019--2023)
**Methods:** N/A
**Quantitative:** TA for 4 semesters, 120+ students total, developed 3 computational lab modules
**Bullet (2L):** Served as teaching assistant for computational biology courses across 4 semesters, developing 3 hands-on simulation lab modules adopted department-wide for 120+ students.
**Bullet (3L):** Served as teaching assistant for computational biology courses across 4 semesters (120+ students total), developing 3 hands-on GROMACS/Python simulation lab modules subsequently adopted department-wide and contributing to course receiving highest student evaluation score in department.
**Tags:** academic
**Significance:** Teaching evidence for academic applications. "Adopted department-wide" shows lasting impact beyond the TA role. Omit for industry resumes.
