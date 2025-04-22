This README outlines the structure of my Zettelkasten system, its categories, and the guidelines for organizing notes. 
```dataviewjs
const currentFile = dv.current().file;
const content = await dv.io.load(currentFile.path);
const lines = content.split("\n");

// Find headers
const headings = lines
  .map((line, index) => {
    const match = line.match(/^(#+)\s*(.+)$/);
    if (match) {
      return {
        level: match[1].length,
        text: match[2].trim(),
        line: index
      };
    }
    return null;
  })
  .filter(h => h);

// Build TOC items with indentation
const tocItems = headings.map(h => {
  const indent = "  ".repeat(h.level - 1); // Indent based on header level
  const link = dv.sectionLink(currentFile.path, h.text, false, h.text);
  return `${indent}- ${link}`; // Single bullet with indent
});

// Render TOC in one paragraph
dv.paragraph("## 📑 Table of Contents\n" + tocItems.join("\n"));
```

---
## Zettelkasten
A Zettelkasten is a straightforward note-taking system I use in Obsidian to keep my ideas organized and connected. It’s like a digital filing cabinet where every note is a single thought or fact, written in my own words, and linked to other notes with simple tags or references. This setup helps me dump info from books, articles, or random thoughts into one place, then grow it into a practical web of knowledge I can easily navigate. In this README, I’ll lay out how I’ve structured it—folders, categories, and all—so anyone (or future me) can see how it works and keep it tidy.

Think of it as your second brain
### Folder Structure
![[📔 Zettelkasten - Folder Structure]]
### How to setup cross-platform sync
![[📔 Obsidian - Free cross-platform sync setup]]
## References
* [[📔 Obsidian]]
* [[📔 Zettelkasten]]