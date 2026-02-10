# /arxivpdf — Convert a publication to an arxiv-ready PDF

## Step 1: Introduce and Prompt for Input

Start with this message:

---

**arxiv-pdf: Publication to LaTeX converter**

This will generate a complete `main.tex` you can paste into [Prism](https://prism.openai.com) and compile to an arxiv-ready PDF. No external files needed — everything in one document.

**What I need from you:**

1. **Best option:** A downloaded `.docx` or `.pdf` of the publication (drag it in or give me the file path). This preserves inline citations, tables, and formatting.
2. **Also works:** A URL to the published web version. Note: websites often strip footnote markers and may truncate long reference lists.
3. **If they differ:** Share both — I'll use the doc for citation mapping and the URL for any updates.

Drop your file or link whenever you're ready.

---

Then **wait for the user to provide their input** before proceeding.

## Step 2: Process the Input

Once the user provides a file, URL, or both:

1. Read the skill file at `~/.claude/skills/arxiv-pdf/SKILL.md` and all files in `~/.claude/skills/arxiv-pdf/references/`.
2. Extract the document content:
   - **Local file (.docx):** Use `textutil -convert txt -stdout <path>` on macOS to extract text.
   - **Local file (.pdf):** Read the PDF directly with the Read tool.
   - **URL:** Use WebFetch to extract content. If the page is behind authentication or truncated, ask the user to provide a downloaded version instead.
   - **Both provided:** Use the local file as the primary source (preserves citations). Cross-check with the URL for any content differences.
3. Run **Phase 1: Audit** as defined in SKILL.md.

## Step 3: Audit and Approval

Present the structured audit report per SKILL.md Phase 1:
- Flag issues with status icons (missing, needs adjustment, good, informational)
- Generate draft abstract and keywords inline if missing
- Flag improper table/figure references with proposed rewrites
- Light-flag optional missing items

**Wait for user to review and approve before proceeding.**

## Step 4: Prep Fixes

Run **Phase 2: Prep** as defined in SKILL.md:
- Propose specific fixes for each flagged issue
- Batch related fixes together
- Wait for user approval on each batch

## Step 5: Generate LaTeX

Run **Phase 3: Generate** as defined in SKILL.md:
- Produce complete, self-contained `main.tex`
- Save to `~/Downloads/main.tex` (or ask user for preferred path)
- End with Prism paste instructions

**Important:** Write the file to disk so the user can open and paste it. Don't just show it in chat — the file will be too large to copy from terminal output.
