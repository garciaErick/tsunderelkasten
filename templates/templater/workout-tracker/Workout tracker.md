---
currentExerciseName: ⚠️ Select an exercise first
currentExerciseDescription: No description
lastLineNumber: "166"
workoutType: 
exerciseToAdd: 
createdFrom: "[[Workout tracker]]"
parent: "[[<% tp.file.title.replace(/ Workout$/, '') %>]]"
obsidianUIMode: preview
currentImagePath:
  type: error
  title: Failed to execute JS
  content: Failed to execute JS during execution "b26a13dd-a001-42d0-84f2-49e0960de962"
  code: |-
    TypeError: Cannot read properties of undefined (reading 'path')
        at Is.anonymous [as func] (plugin%3Ajs-engine%3AJS_EXECUTION%3Ab26a13dd-a001-42d0-84f2-49e0960de962:7:31)
        at Is.runFunction (plugin:js-engine:49:636)
        at Zu.execute (plugin:js-engine:70:74859)
        at Fs.execute (plugin:js-engine:70:1760)
        at Jv.evaluateCode (plugin:obsidian-meta-bind-plugin:152:10347)
        at async Jv.evaluate (plugin:obsidian-meta-bind-plugin:152:10655)
---
# 🏋🏾‍♀️ Workout Tracker
If you need inspiration, you can follow my [[🏋🏿 Exercises - 3-day Split Regime Exercise Guide]]
<% await tp.file.include("[[3. Workout Tracker - TOC]]") %>
## 🔎 Workout Selector
This is a two step form, you first select you initial filter. I usually do a push, pull, leg, 3 day split. This will filter the next list, you can select an exercise to view a brief explanation and add to tracking.
```meta-bind-js-view
{workoutType} as workoutType
{exerciseToAdd} as exerciseToAdd
{lastLineNumber} as lastLineNumber
---
const dv = app.plugins.plugins["dataview"].api;
const workoutTag = context.bound.workoutType || "exercise"; // Fallback if empty
const exerciseOptions = dv.pages('"tsunderelkasten/4.reference"')
    .where(p => p.file.path.includes("🏋🏿 Exercises") && !p.file.path.includes("templates") && p.tags?.includes(workoutTag))
    .map(p => `option(${p.file.link}, ${p.file.name})`)
    .join(", ");
const lines = [];
lines.push("```meta-bind");
lines.push('INPUT[select(title(1. Exercise type), defaultValue(""), option(push, Push Day), option(pull, Pull Day), option(leg, Leg Day), option(exercise, All)):workoutType]');
lines.push("```");
lines.push(`### 2. Exercises to Add: \`INPUT[suggester(${exerciseOptions}):exerciseToAdd]\``);

const lastLine = context.bound.lastLineNumber;
lines.push("```meta-bind-button");
lines.push("id: add-selected-exercise-button");
lines.push("style: primary");
lines.push("label: ➕ Exercise");
lines.push("hidden: true");
lines.push("action:");
lines.push("  type: insertIntoNote");
lines.push(`  line: ${lastLine}`);
lines.push("  value: templates/templater/workout-tracker/1. Workout tracker - Add exercise and sets based on selection.md");
lines.push("  templater: true");
lines.push("```");
lines.push("```meta-bind-button");
lines.push("id: add-workout-breakdown-button");
lines.push("style: primary");
lines.push("label: 🏁 Finish");
lines.push("hidden: true");
lines.push("action:");
lines.push("  type: insertIntoNote");
lines.push(`  line: ${lastLine}`);
lines.push("  value: templates/templater/workout-tracker/2. Workout tracker - Exercise breakdown");
lines.push("  templater: true");
lines.push("```");

lines.push("```meta-bind-button");
lines.push("id: refresh-line-number-button");
lines.push("style: primary");
lines.push("label: 🔄");
lines.push("hidden: true");
lines.push("action:");
lines.push("  type: replaceInNote");
lines.push("  fromLine: 4");
lines.push("  toLine: 4");
lines.push("  replacement: templates/templater/workout-tracker/4. Workout Tracker - Update last line number");
lines.push("  templater: true");
lines.push("```");

lines.push("`BUTTON[add-selected-exercise-button, add-workout-breakdown-button, refresh-line-number-button]`");

// Get metadata with corrected link handling
const linkPath = String(context.bound.exerciseToAdd).replace(/\[\[(.*?)(?:\|.*)?\]\]/, "$1");
const exerciseData = dv.page(linkPath);
const { exerciseName = "⚠️ Select an exercise first", description = "", imagePath = "", musclesWorked = []} = exerciseData || {};
lines.push(`#### ${exerciseName}`);
lines.push(`${description}`);
lines.push("");
if(musclesWorked.length){
	lines.push("##### Muscles worked");
	musclesWorked.forEach(muscle => lines.push(`- ${muscle}`));
}
lines.push(`${imagePath ? "!"+ imagePath : ""}`);  

return engine.markdown.create(lines.join("\n"));
```
 ```meta-bind-js-view
{exerciseToAdd} as exerciseToAdd 
{workoutType} as workoutType
save to {lastLineNumber}  
hidden
---
const dv = app.plugins.plugins["dataview"].api;
const currentFile = dv.page(app.workspace.getActiveFile().path); // Use active file path
const content = await app.vault.read(app.workspace.getActiveFile()); // Read file content
const lineCount = content.split('\n').length;
return `${lineCount}`;
```
 ```meta-bind-js-view
{workoutType} as workoutType
{exerciseToAdd} as exerciseToAdd
save to {currentExerciseName}  
hidden
---
const dv = app.plugins.plugins["dataview"].api;
const linkPath = String(context.bound.exerciseToAdd).replace(/\[\[(.*?)(?:\|.*)?\]\]/, "$1");
const exerciseData = dv.page(linkPath) || { exerciseName: "⚠️ Select an exercise first", description: "" };
return exerciseData.exerciseName;
```
 ```meta-bind-js-view
{workoutType} as workoutType
{exerciseToAdd} as exerciseToAdd
save to {currentExerciseDescription}  
hidden
---
const dv = app.plugins.plugins["dataview"].api;
const linkPath = String(context.bound.exerciseToAdd).replace(/\[\[(.*?)(?:\|.*)?\]\]/, "$1");
const exerciseData = dv.page(linkPath) || { exerciseName: "Unknown", description: "No description" };
return exerciseData.description;
```
 ```meta-bind-js-view
{workoutType} as workoutType
{exerciseToAdd} as exerciseToAdd
save to {shortName}  
hidden
---
const dv = app.plugins.plugins["dataview"].api;
const linkPath = String(context.bound.exerciseToAdd).replace(/\[\[(.*?)(?:\|.*)?\]\]/, "$1");
const exerciseData = dv.page(linkPath) || { exerciseName: "Unknown", description: "No description" };
return exerciseData.shortName;
```
```meta-bind-js-view
{workoutType} as workoutType
{exerciseToAdd} as exerciseToAdd
save to {currentMusclesWorked}  
hidden
---
const dv = app.plugins.plugins["dataview"].api;
const linkPath = String(context.bound.exerciseToAdd).replace(/\[\[(.*?)(?:\|.*)?\]\]/, "$1");
const exerciseData = dv.page(linkPath) || { exerciseName: "Unknown", description: "No description" };
return exerciseData.musclesWorked;
```
```meta-bind-js-view
{workoutType} as workoutType
{exerciseToAdd} as exerciseToAdd
save to {currentImagePath}  
hidden
---
const dv = app.plugins.plugins["dataview"].api;
const linkPath = String(context.bound.exerciseToAdd).replace(/\[\[(.*?)(?:\|.*)?\]\]/, "$1");
const exerciseData = dv.page(linkPath) || { exerciseName: "Unknown", description: "No description" };
return exerciseData.imagePath.path;
```
## 🤸🏾‍♀️ Weight and Reps by Exercise  
