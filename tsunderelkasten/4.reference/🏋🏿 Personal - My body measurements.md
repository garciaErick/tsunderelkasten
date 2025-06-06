---
title: 🏋🏿 Personal - My BMR (Basal metabolic rate)
created: 2025-04-08
dg-publish: false
dg-show-local-graph: false
description: 
tags: 
aliases: 
isToc: false
isRootNote: false
parent: "[[🏋🏿 Personal -  Energy and Metabolism Metrics]]"
---
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
## My measurements
* heigh: 168cm
* weight: 77kg
* age: 30 years