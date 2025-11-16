# Remote Control Override for Autonomous Tractor

This repository houses the LaTeX sources for my MMAN4951 Thesis A report on developing a remote-control solution that enables a human operator to assume positive control over an autonomous tractor. The research blends IoT telemetry with radio-frequency fail-safe links built around the FORT Robotics EPC1001 endpoint controller and the SRC Pro transmitter, and also discusses one-out-of-two (1oo2) redundancy and related safety requirements.

## Repository Layout
- `main.tex` – master document that pulls in every section and the bibliography. It currently loads `nomencl`, `geometry`, `footmisc`, `setspace`, `graphicx`, `subcaption`, and `float`.
- `Sections/` – modular `.tex` files (TitlePage, Introduction, Literature Review, Research Question & Project Plan, Project Dependent Preparations, Conclusion, Appendix, etc.) that make it easy to draft specific parts of the report.
- `Figures/` – image assets referenced from the sections.
- `References.bib` – BibTeX database for the literature review and safety/regulatory citations (e.g., for FORT devices, IEC functional safety references, 1oo2 architectures).
- `rubric.md` – the official MMAN4951 interim report rubric for quick access to assessment criteria.

## Building the PDF
1. Install a LaTeX distribution with the packages referenced in `main.tex` (TeX Live and MikTeX both provide them by default).
2. From the repository root run `latexmk -pdf main.tex` to build `main.pdf`. This automatically manages the `.aux`, `.bbl`, and nomenclature files.
   - Alternatively run the manual cycle: `pdflatex main.tex`, `bibtex main`, `makeindex main.nlo -s nomencl.ist -o main.nls`, and `pdflatex` twice more to resolve cross-references.
3. Clean auxiliary files with `latexmk -c` when you need a tidy working tree.

## Writing Workflow
1. **Set the context** – Replace the placeholders in `Sections/TitlePage.tex` and complete the abstract with the tractor override problem statement, highlighting the safety case for remote supervision of agricultural autonomy.
2. **Develop the literature review** – Use `Sections/Literature Review.tex` to summarise current autonomous tractor deployments, remote intervention standards, and functional safety practices (IEC 61508/ISO 25119).
3. **Detail the control solution** – In `Sections/Research Question and Project Plan.tex`, describe how the EPC1001 and SRC Pro chain together, how IoT telemetry feeds into the operator HMI, and how 1oo2 redundancy mitigates single-point failures. Include the testing plan (RF range verification, latency, fail-over drills) and any training requirements.
4. **Document preparations** – `Sections/Project Dependent Preparations.tex` should cover hardware acquisition, integration benches, firmware access for the FORT modules, and safety approvals or operator certifications.
5. **Reference rigorously** – Add BibTeX entries for datasheets, RF compliance notes, safety standards, and agricultural case studies to `References.bib`. Cite them inline with `\cite{}` so the bibliography stays consistent.

## Key Research Threads to Track
- Architecture of the human-in-the-loop override channel (primary IoT link vs. RF backup) and the transition logic between autonomous and manual control states.
- Implementation of 1oo2 redundancy in the stop/enable circuit so that the EPC1001 only energises actuators when the SRC Pro and redundant sensors agree.
- Cyber-security and spectrum management considerations when exposing remote interfaces on farm networks.
- Validation plan: bench integration, SIL determination, latency budget, range testing, and on-tractor dry runs.

## Assessment Reminders
Use `rubric.md` to ensure the thesis draft meets MMAN4951 expectations: roughly 12–15 pages for the literature review (50 % weighting), 3–5 pages for the research question and plan (20 %), 1–2 pages for project-dependent preparations (20 %), and high-quality presentation (10 %). Keep the maximum page limit of 20 (excluding appendices and references) in mind during edits.

## Version Control Tips
- Commit snapshots of `main.tex`, the relevant `Sections/*.tex`, and `References.bib` together so that each revision of the argument stays reproducible.
- Avoid committing LaTeX build artefacts (`main.aux`, `main.bbl`, etc.); the `.gitignore` is already configured to filter them out while keeping PDFs and source files.
