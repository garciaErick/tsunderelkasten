---
title: 📔 Zettelkasten
created: 2025-03-29
dg-publish: false
dg-show-local-graph: false
description: 
tags: 
aliases: 
isToc: true
isRootNote: false
parent: "[[📔 Obsidian]]"
obsidianUIMode: preview
---
#### Parent > [[📔 Obsidian]]
```dataviewjs
// Get the current page
const currentPage = dv.current();

// Get all pages
const allPages = dv.pages();

// Filter for children of the current page using parent.toString()
const children = allPages.where(p => {
    return p.parent && p.parent.toString() === currentPage.file.link.toString();
});

if (children.length === 0) {
    dv.paragraph("No direct children found for '" + currentPage.file.name + "'.");
}

// Build the list
function buildList(page, indent = 0) {
    let output = "";
    const indentStr = "  ".repeat(indent);
    output += `${indentStr}- [[${page.file.name}]]\n`;
    if (page.isToc) {
        const nestedChildren = allPages.where(p => {
            return p.parent && p.parent.toString() === page.file.link.toString();
        });
        for (const child of nestedChildren) {
            output += buildList(child, indent + 1);
        }
    }
    return output;
}

let result = "";
for (const child of children) {
    result += buildList(child);
}
dv.paragraph("## TOC\n" + result);
```
## What is a Zettelkasten?
A Zettelkasten is a straightforward note-taking system I use in Obsidian to keep my ideas organized and connected. It’s like a digital filing cabinet where every note is a single thought or fact, written in my own words, and linked to other notes with simple tags or references. This setup helps me dump info from books, articles, or random thoughts into one place, then grow it into a practical web of knowledge I can easily navigate. In this README, I’ll lay out how I’ve structured it—folders, categories, and all—so anyone (or future me) can see how it works and keep it tidy.