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
## BMR Definition
The _Basal Metabolic Rate (BMR) Calculator_ estimates your basal metabolic rate—the amount of energy expended while at rest in a neutrally temperate environment, and in a post-absorptive state (meaning that the digestive system is inactive, which requires about 12 hours of fasting).
### My BMR calculation 2025
* BMR: 1675 calories a day
### Daily calorie needs based on activity level
According to Grok, with my current training regime of strength training, cardio, stretching 3 to 4 times a week, I classify as either category:

* Exercise 4-5 times a week (**2454 calories**) 
* **Expected category** Intense exercise 3-4 times a week (**2519 calories**)
## Screenshot from calculator
![[pasted-image-20250408124819.png|650]]
## References
* [BMR Calculator](https://www.calculator.net/bmr-calculator.html?cage=30&csex=m&cheightfeet=5&cheightinch=10&cpound=160&cheightmeter=160&ckg=77&cmop=0&coutunit=c&cformula=m&cfatpct=20&ctype=metric&x=Calculate)