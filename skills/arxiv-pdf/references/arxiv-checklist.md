# ArXiv Compliance Checklist

Use this checklist during Phase 1 (Audit) to evaluate a document's readiness for arxiv submission.

---

## 1. Abstract
- **Required:** Yes
- **Check:** Is an abstract present?
- **Standards:** 150-300 words. Should summarize the problem, approach, results, and significance. No citations, no equations, no references to figures/tables.
- **Common issues:** Missing entirely, too long (>300 words), too short (<100 words), contains references or math notation.

## 2. Title
- **Required:** Yes
- **Check:** Is the title clear, specific, and appropriately concise?
- **Standards:** Avoid abbreviations unless universally known. Title case or sentence case (be consistent). No trailing period.
- **Common issues:** Too vague, contains undefined acronyms, excessively long.

## 3. Authors and Affiliations
- **Required:** Yes
- **Check:** Are all authors listed with institutional affiliations?
- **Standards:** Full names (not just initials). Each author should have at least one affiliation. Include email for corresponding author.
- **Common issues:** Missing affiliations, inconsistent name formatting, missing corresponding author designation.

## 4. Section Structure
- **Required:** Yes
- **Check:** Does the document follow a logical section hierarchy?
- **Standards:** Typical structure: Introduction, Related Work/Background, Methods, Results/Experiments, Discussion, Conclusion. Sections should be numbered. Subsections should nest properly (no orphan subsections).
- **Common issues:** Missing introduction or conclusion, inconsistent numbering, sections out of logical order, deeply nested subsections (>3 levels).

## 5. Figures
- **Required:** If the document references figures
- **Check:** Are all figures properly numbered, captioned, and referenced in text?
- **Standards:** Every figure must have a number and descriptive caption below it. Every figure must be referenced at least once in the body text. Figures should be high resolution. Captions should be self-contained (understandable without reading the full text).
- **Common issues:** Missing captions, unreferenced figures, inconsistent numbering, low-resolution images, captions that say only "Figure 1" with no description.

## 6. Tables
- **Required:** If the document contains tables
- **Check:** Are all tables properly numbered, captioned, and referenced in text?
- **Standards:** Every table must have a number and descriptive caption (typically above the table). Every table must be referenced in the body text. Avoid merged cells where possible. Use clean formatting (booktabs style preferred).
- **Common issues:** Merged cells that don't translate to LaTeX, missing captions, unreferenced tables, inconsistent formatting, tables too wide for the page.

## 7. Bibliography / References
- **Required:** Yes (for most papers)
- **Check:** Are references complete, consistent, and properly formatted?
- **Standards:** Each reference should have: author(s), title, venue/journal, year. DOIs or URLs are recommended. In-text citations should be consistent (numbered [1] or author-year). Every cited work must appear in the reference list and vice versa.
- **Common issues:** Incomplete entries (missing year, venue), plain-text references that aren't structured, inconsistent citation style, dangling citations (cited but not in references), uncited references.

## 8. Mathematics and Equations
- **Required:** If the document contains math
- **Check:** Are equations properly formatted and numbered where appropriate?
- **Standards:** Important equations should be numbered. Inline math should be brief. Display math for complex expressions. Consistent notation throughout.
- **Common issues:** Equations as images instead of text, inconsistent notation, unnumbered equations that are referenced later, Unicode math symbols that need LaTeX equivalents.

## 9. Special Characters
- **Required:** Always check
- **Check:** Are there characters that need LaTeX escaping?
- **Characters to catch:**
  - Smart quotes (" " ' ') → LaTeX quotes (`` ` `` and `'`)
  - Em-dash (—) → `---`
  - En-dash (–) → `--`
  - Ampersand (&) → `\&`
  - Percent (%) → `\%`
  - Dollar sign ($) → `\$`
  - Hash (#) → `\#`
  - Underscore in text (_) → `\_`
  - Tilde (~) → `\textasciitilde`
  - Caret (^) → `\textasciicircum`
  - Backslash in text (\) → `\textbackslash`
  - Non-breaking spaces → regular spaces or `~`
  - Ellipsis (…) → `\ldots`
- **Common issues:** Copy-pasted text from Word/Docs with smart typography, Unicode characters that don't compile.

## 10. Footnotes
- **Required:** If the document uses footnotes
- **Check:** Are footnotes properly marked and content appropriate?
- **Standards:** Use `\footnote{}` in LaTeX. Footnotes should be brief. Consider whether content should be in the main text or a footnote.
- **Common issues:** Footnotes that should be citations, very long footnotes, footnotes with complex formatting.

## 11. Keywords / Subject Classification
- **Required:** Recommended
- **Check:** Are keywords or subject classifications provided?
- **Standards:** 3-6 keywords that describe the paper's topics. ACM CCS or MSC classification codes if applicable to the venue.
- **Common issues:** Missing entirely, too few keywords, overly broad keywords.

## 12. Acknowledgments
- **Required:** Recommended
- **Check:** Is there an acknowledgments section?
- **Standards:** Should credit funding sources, helpful colleagues, computational resources, etc. Placed after the conclusion and before references.
- **Common issues:** Missing funding acknowledgments (often required by grants), missing entirely.

## 13. Table of Contents / Document Navigation
- **Required:** No (arxiv papers typically don't include a ToC)
- **Check:** Is the section structure clear enough to serve as implicit navigation?
- **Standards:** Sections and subsections should have descriptive titles. Numbering should be consistent.
- **Common issues:** Generic section titles ("Part 1"), missing subsection titles.

## 14. Cross-References
- **Required:** If the document references its own sections, figures, tables, or equations
- **Check:** Are all internal references valid?
- **Standards:** Use `\ref{}` and `\label{}` for all cross-references. Every `\ref` should have a corresponding `\label`. References should use consistent formatting ("Section 3" vs "section 3" vs "Sec. 3").
- **Common issues:** Broken references ("Section ??"), inconsistent reference formatting, references to nonexistent labels.

## 15. Page Layout and Length
- **Required:** Check
- **Check:** Is the document an appropriate length for its content?
- **Standards:** No strict arxiv limit, but papers should be appropriately concise. Standard margins (geometry package). Single or double column as appropriate.
- **Common issues:** Excessive whitespace, very short papers that should be notes, extremely long papers that could be split.
