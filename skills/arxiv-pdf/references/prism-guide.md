# Prism Paste-and-Compile Guide

Instructions for compiling LaTeX in OpenAI Prism. Include these at the end of Phase 3 output.

---

## Standard Instructions (copy-paste to user)

### How to compile in Prism

1. **Open Prism:** Go to [prism.openai.com](https://prism.openai.com)
2. **Create a new project:** Click the **+** button to start a new project
3. **Clear the editor:** In `main.tex`, select all with **Cmd+A** (Mac) or **Ctrl+A** (Windows/Linux), then delete
4. **Paste the LaTeX:** Paste the entire LaTeX code block above into the editor
5. **Compile:** Click the **Compile** button (or press the compile shortcut)
6. **Review:** Check the PDF preview for any formatting issues
7. **Upload figures (if any):** For each figure placeholder in the code:
   - Click the file upload area in Prism's file panel
   - Upload your image files matching the filenames in the `\includegraphics` commands
   - Re-compile after uploading
8. **Download:** Once satisfied, download the compiled PDF

---

## Troubleshooting

### Common compilation errors and fixes

**"Undefined control sequence"**
- A package is missing. Check which command is undefined and add the appropriate `\usepackage`.

**"Missing $ inserted"**
- An underscore `_` or caret `^` appears outside math mode. Escape with `\_` or `\^{}`, or wrap in `$...$` if it's math.

**"File not found" for figures**
- Upload the image files to Prism's file browser. Filenames must match exactly (case-sensitive).

**"Too many }'s"**
- Mismatched braces. Check the line number in the error and count opening/closing braces.

**"Environment undefined"**
- Missing package. Common ones: `algorithm` needs `\usepackage{algorithm}`, `subfigure` needs `\usepackage{subcaption}`.

**Overfull/underfull hbox warnings**
- Usually cosmetic. For tables: reduce column widths or use `tabularx`. For text: LaTeX will handle most cases; persistent issues may need manual line breaks.

---

## Figure Upload Checklist

When the generated LaTeX references figures, remind the user:

- [ ] All figure files are named to match `\includegraphics{filename}` paths
- [ ] Images are in PNG, JPG, or PDF format
- [ ] Resolution is at least 300 DPI for print quality
- [ ] Files are uploaded to the correct directory in Prism (typically root or `figures/`)
- [ ] Re-compile after uploading all figures
