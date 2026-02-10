# ArXiv PDF Skill

Convert publications into arxiv-ready LaTeX code that compiles in OpenAI Prism.

## Overview

This skill implements a 3-phase workflow: **Audit > Prep > Generate**. The goal is a single `main.tex` file the user can paste into Prism (prism.openai.com) and compile to a properly formatted arxiv PDF.

## Reference Files

- `references/arxiv-checklist.md` — Compliance checklist with explanations
- `references/latex-templates.md` — LaTeX snippets and templates
- `references/prism-guide.md` — Prism paste-and-compile instructions

Read all reference files before starting any phase.

---

## Input Handling

### Priority Order
1. **Local .docx or .pdf file** (best): Preserves inline citation markers `[1]`, `[2]`, etc., tables, and full formatting. Use `textutil -convert txt -stdout <path>` on macOS for .docx files. Use the Read tool for .pdf files.
2. **Website URL** (good): Captures clean text and structure. However, websites often strip inline citation markers and may truncate long reference lists due to fetch limits. Best for publications without numbered inline citations.
3. **Both** (ideal when they differ): Use the local file as primary source for citation mapping. Cross-reference with the URL for any content updates or corrections.
4. **Pasted content** (fallback): If the user pastes content directly, work with that.

### URL Handling
- Use WebFetch to retrieve content.
- If the URL is a Google Docs URL, try the export URL: replace `/edit` with `/export?format=txt`.
- If fetching fails or content is truncated, ask the user to provide a downloaded file instead.
- Always check whether inline citation markers (e.g., `[1]`, `[2]`) are present in the fetched text. If missing, warn the user that citation placement may need manual review, or request the original document.

---

## Phase 1: Audit

**Goal:** Identify everything that is NOT arxiv-ready in the source document.

### Checklist
Run through every item in `references/arxiv-checklist.md`. For each item, determine:
- **Status:** Missing/broken, Needs adjustment, Good, or Informational (optional, not found)
- **Details:** What specifically is wrong and where

### Proactive Suggestions During Audit
For certain missing items, don't just flag them — **generate a draft suggestion immediately** so the user can review and approve it in one step:

- **Abstract missing/too long:** Draft a 150-300 word abstract based on the document's introduction, conclusion, or executive summary. Present it inline in the audit report.
- **Keywords missing:** Propose 5-7 relevant keywords based on the paper's content. Present them inline.
- **Author affiliations incomplete:** Propose structured author block based on any author info found. Ask user to confirm.

### Light-Flagging for Optional Items
For items that are truly optional or not applicable, note their absence briefly:
- No footnotes detected — not required, just flagging.
- No internal/organizational metadata found — nothing to remove.
- No acknowledgments section — optional, ask if user wants one.

Do NOT treat these as errors. Simply note their absence so the user is informed.

### Table & Figure Cross-Reference Check
Check that every table and figure is referenced **properly** in the body text using academic conventions:
- **Correct:** "As shown in Table 1, the three actor categories..." or "Table 1 summarises..."
- **Incorrect:** Introducing a table/figure with just a colon, e.g., "...three categories:" followed by the table with no formal reference.
- **Incorrect:** No mention of the table/figure at all in the surrounding text.

For each improperly referenced table or figure, flag it and propose a rewritten sentence that uses "Table X" or "Figure X" in academic style.

### Output Format
Present a structured report as a table with: Status, Item, Details.

Include inline proposals for abstract, keywords, and any rewritten cross-references.

End with a summary count of issues by category.

**Wait for user confirmation before proceeding to Phase 2.**

---

## Phase 2: Prep

**Goal:** Fix every flagged issue with user approval.

### Process
For each issue, in order of importance:

1. **Propose a specific fix.** Don't just say "add an abstract" — draft the actual abstract text.
2. **Show the proposal clearly.** Use before/after format when modifying existing content.
3. **Batch related fixes.** Group figure captions together, bibliography entries together, etc.
4. **Wait for approval.** The user can approve, edit, or reject each proposal.

### Common Fixes

**Abstract:** Draft from the paper's introduction/conclusion. Keep to 150-300 words. Include the problem, approach, key results.

**Author/Affiliations:** Structure as: Name, Institution, Email. Ask user to confirm or provide missing info.

**Figures:** Generate descriptive captions based on surrounding text. Use format: "Figure N: [description]."

**Tables:** Restructure merged cells into proper rows/columns. Propose `booktabs`-style formatting.

**Bibliography:** Convert plain-text references to structured entries with: authors, title, venue/journal, year, DOI/URL where available. Use `\bibitem` format (not BibTeX .bib — Prism-friendly).

**Special Characters:** Identify and map: em-dash to `---`, en-dash to `--`, smart quotes to LaTeX quotes, ampersand to `\&`, percent to `\%`, etc.

**Keywords/Classification:** Propose based on paper content if missing.

**Acknowledgments:** Ask user if they need to acknowledge funding, collaborators, etc.

### Output
After all fixes are approved, confirm the full list of changes and proceed to Phase 3.

---

## Phase 3: Generate

**Goal:** Produce a single, complete, compilable `main.tex`.

### Requirements
1. **Self-contained.** No external .bib files, no external .sty files beyond standard LaTeX packages. Everything in one file.
2. **Prism-compatible.** Must compile in OpenAI Prism without errors. Use only packages available in standard TeX Live.
3. **Arxiv conventions.** Follows standard arxiv paper formatting.
4. **Complete content.** All text, tables, figures (as placeholders), and references from the source document.

### Document Structure
Follow the template structure in `references/latex-templates.md`:

1. Preamble (documentclass, packages)
2. Title, authors, affiliations, **date**
3. Abstract
4. Body sections and subsections
5. Acknowledgments (if applicable)
6. Bibliography (inline `thebibliography`)
7. **"How to Cite This Publication" section** (always include)
8. Appendices (if applicable)

### LaTeX Guidelines

**Packages:** Only include packages that are actually used. Common set:
- `inputenc` (utf8), `fontenc` (T1)
- `amsmath`, `amssymb` for math
- `graphicx` for figures
- `booktabs` for tables
- `hyperref` for links (load last)
- `geometry` for margins
- `xcolor` if colors are needed

**Tables:** Use `booktabs` (`\toprule`, `\midrule`, `\bottomrule`). No vertical lines. Use `tabularx` or `longtable` for wide/long tables.

**Figures:** Use `\includegraphics` with placeholder filenames like `figures/fig1.png`. Add clear comments about what image to upload.

**Math:** Use `equation`, `align`, `gather` environments. Number important equations.

**Citations:** Use `\cite{key}` in text and `\bibitem{key}` in bibliography.

**Bibliography URL overflow prevention:** Always include `\usepackage[hyphens]{url}` **before** `\usepackage{hyperref}` so that long URLs can break across lines. Additionally, wrap the bibliography in `{\sloppy ... }` to allow flexible line breaking.

**Publication date:** Include the publication date using `\date{Month Day, Year}`. If no date is found in the document, ask the user before generating.

**"How to Cite" section:** Always add a `\section*{How to Cite This Publication}` after the bibliography with a formatted plain-text citation and a BibTeX entry that readers can copy.

**Special characters:** Escape everything properly. Use `--` for en-dash, `---` for em-dash, and LaTeX quote marks.

### Output
1. **Write the file to disk** (default: `~/Downloads/main.tex`). The file will be too large for terminal output.
2. Follow with Prism paste instructions from `references/prism-guide.md`.
3. Note any figures the user needs to upload separately.

### Quality Checks Before Output
- Every `\begin` has a matching `\end`
- Every `{` has a matching `}`
- All special characters are escaped
- All `\cite` keys match `\bibitem` keys
- All figure references match figure labels
- All table references match table labels
- All tables and figures are referenced by name in body text (e.g., "Table 1", "Figure 2")
- No orphaned `\label` or `\ref` commands
- Package imports match actual usage
- `\usepackage[hyphens]{url}` loaded before `hyperref` (no URL overflow)
- Bibliography wrapped in `{\sloppy ... }` for flexible line breaking
- Publication date is set (not empty)
- "How to Cite This Publication" section is present after bibliography
