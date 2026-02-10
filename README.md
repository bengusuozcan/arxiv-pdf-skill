# arxiv-pdf-skill

A Claude Code skill that converts publications into arxiv-ready LaTeX. Generates a complete, self-contained `main.tex` you can paste into [Prism](https://prism.openai.com) and compile to a PDF.

## What it does

Run `/arxivpdf` in Claude Code and provide a document. The skill runs a 3-phase workflow:

1. **Audit** — Checks the document against an arxiv compliance checklist (abstract, authors, references, tables, figures, special characters, etc.). Proactively drafts missing elements like abstracts and keywords. Flags issues with proposed fixes.

2. **Prep** — Proposes specific fixes for each issue. You approve, edit, or skip each one before proceeding.

3. **Generate** — Produces a single `main.tex` file with:
   - Proper `\documentclass{article}` with all required packages
   - Title, authors, affiliations, date, abstract, keywords
   - All sections with full content
   - Tables using `booktabs`
   - Figure placeholders with `\includegraphics` + captions
   - Inline bibliography (`\thebibliography` — no external .bib file)
   - "How to Cite" section with plain-text and BibTeX formats
   - Prism paste-and-compile instructions

## Input formats

| Format | Quality | Notes |
|--------|---------|-------|
| `.docx` file | Best | Preserves inline citations `[1]`, tables, full formatting |
| `.pdf` file | Good | Full content, may need OCR for scanned docs |
| Website URL | Good | Clean text, but may strip citation markers and truncate references |
| Both doc + URL | Ideal | Use doc for citations, URL for latest content |

## Installation

Copy the files into your Claude Code configuration directory:

```bash
# Copy the slash command
cp commands/arxivpdf.md ~/.claude/commands/

# Copy the skill files
cp -r skills/arxiv-pdf ~/.claude/skills/
```

Or clone and symlink:

```bash
git clone https://github.com/YOUR_USERNAME/arxiv-pdf-skill.git
ln -s "$(pwd)/arxiv-pdf-skill/commands/arxivpdf.md" ~/.claude/commands/arxivpdf.md
ln -s "$(pwd)/arxiv-pdf-skill/skills/arxiv-pdf" ~/.claude/skills/arxiv-pdf
```

## Usage

```
/arxivpdf
```

Then provide your document when prompted. The skill will:
1. Ask for your file or URL
2. Run the audit and show results
3. Propose fixes for your approval
4. Generate `main.tex` and save it to `~/Downloads/main.tex`
5. Give you Prism paste instructions

## Prism workflow

After the skill generates your LaTeX:

1. Go to [prism.openai.com](https://prism.openai.com)
2. Click **+** to create a new project
3. In `main.tex`, select all (**Cmd+A**) and delete
4. Paste the generated LaTeX
5. Upload any figure files referenced in the code
6. Click **Compile**
7. Download your PDF

## File structure

```
arxiv-pdf-skill/
  commands/
    arxivpdf.md              # Slash command entry point
  skills/
    arxiv-pdf/
      SKILL.md               # Main workflow (Audit > Prep > Generate)
      references/
        arxiv-checklist.md   # 15-item arxiv compliance checklist
        latex-templates.md   # LaTeX snippets and templates
        prism-guide.md       # Prism compilation instructions
```

## Customization

- **Checklist:** Edit `arxiv-checklist.md` to add venue-specific requirements
- **Templates:** Edit `latex-templates.md` to change default packages or styles
- **Prism guide:** Edit `prism-guide.md` if your LaTeX editor workflow differs
