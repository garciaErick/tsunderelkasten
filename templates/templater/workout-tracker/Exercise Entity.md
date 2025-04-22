---
exerciseName: 
shortName: 
imagePath: "[[media/workout-dictionary/default.png]]"
description: 
tags:
  - exercise
  - pull
  - push
  - leg
type:
  - exercise
obsidianUIMode: preview
parent: "[[🏋🏿 Exercises]]"
substitute: 
createdFrom: "[[Exercise Entity]]"
musclesWorked: 
---
<%*
await tp.file.move(`/tsunderelkasten/4.reference/🏋🏿 Exercises - Exercise Name`);
%>## `VIEW[{exerciseName}][text]`
`VIEW[{description}][text]`
```meta-bind-js-view
{imagePath} as imagePath 
---
return engine.markdown.create(`!${context.bound.imagePath}`);
```

<% await tp.file.include("[[1. Exercise Entity - Exercise History]]") %>