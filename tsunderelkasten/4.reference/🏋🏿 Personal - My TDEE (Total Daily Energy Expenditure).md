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
## TDEE Definition
TDEE stands for total daily energy expenditure. It is the total energy that a person uses in a day. TDEE is hard to measure accurately and varies day by day. More often, it is estimated using factors such as a person's basal metabolic rate (BMR), activity level, and the thermic effect of food.
### Basal metabolic rate
BMR is a person's energy usage rate while at rest in a temperate environment when the digestive system is inactive. In other words, it is the minimum energy needed to maintain a person's vital organs only.
### Activity level
Activity level is a factor that is based on the amount of activity a person undergoes. This includes deliberate exercise as well as other activities that a person may undergo as part of their job or typical daily activities. These factors are more specifically referred to as the thermic effect of activity, and non-exercise activity thermogenesis (energy expended for non-sleeping, eating, or sports-like exercise).
### Thermic effect of food
The thermic effect of food, also referred to as specific dynamic action, is the amount of energy required by the body to process and use food. It is sometimes estimated as 10% of food energy intake, but this can vary significantly depending on the type of food consumed. Protein, for example, has a far larger thermic effect than dietary fat, since it is more difficult to process.
## My TDEE calculation 2025
* TDEE or body weight maintenance energy requirement: **2,596** Calories per day.
* BMI Score: 27.3kg/m2 (Overweight)
* Healthy BMI: 18.5-25kg/m2
### Energy intake to lose weight 
* Mild weight loss (.25kg/week): 2346 calories/day
* **Desired pace** Weight loss (.5kg/week): 2096 calories/day
* Extreme Weight loss (1kg/week): 1596 calories/day
### Energy intake to gain weight 
* Mild weight gain (.25kg/week): 2846 calories/day
* Weight gain (.5kg/week): 3096 calories/day
* Extreme Weight gain (1kg/week): 3596 calories/day
## Screenshot from calculator
![[pasted-image-20250408131719.png|650]]
 ## References
* [TDEE Calculator](https://www.calculator.net/tdee-calculator.html?cage=30&csex=m&cheightfeet=5&cheightinch=10&cpound=165&cheightmeter=168&ckg=77&cactivity=1.55&cmop=0&coutunit=c&cformula=m&cfatpct=20&printit=0&ctype=metric&x=Calculate)