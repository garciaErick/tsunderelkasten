---
exerciseName: Lying Leg Curl
imagePath: "[[media/workout-dictionary/lyingLegCurl.png]]"
description: Lie face down on the machine and curl the pad toward your glutes by bending your knees—keep your hips pressed into the bench and control the lowering phase.
tags:
  - exercise
  - leg
type:
  - exercise
obsidianUIMode: preview
parent: "[[🏋🏿 Exercises - Leg]]"
substitute: 
createdFrom: "[[Exercise Entity]]"
musclesWorked:
  - hamstrings
currentExerciseName: ⚠️ Select an exercise first
currentExerciseDescription: No description
lastLineNumber: "26"
shortName: lyingLegCurl
---
# `VIEW[{exerciseName}][text]`
`VIEW[{description}][text]`
```meta-bind-js-view
{imagePath} as imagePath 
---
return engine.markdown.create(`!${context.bound.imagePath}`);
```
### 📈 Exercise History 
```dataviewjs
// Get the current note's shortName from its frontmatter
const shortName = dv.current().shortName || "unknown";

// Define the folder where workout tracker files are stored
const workoutFolder = "tsunderelkasten/1.fleeting/1.daily";

// Get all files in the workout folder
const workoutFiles = dv.pages(`"${workoutFolder}"`);

// Initialize an array to store the historic data
let history = [];

// Iterate through each workout file
for (const page of workoutFiles) {
  // Extract date from filename (e.g., "2025-04-17" from "2025-04-17 Thursday Workout")
  const dateMatch = page.file.name.match(/(\d{4}-\d{2}-\d{2})/);
  const date = dateMatch ? dateMatch[1] : page.file.name;

  // Get all metadata keys for this file
  const metadata = page;

  // Temporary object to store sets for this date
  let sets = [];

  // Look for metadata keys that start with the shortName
  for (const key in metadata) {
    if (key.startsWith(shortName)) {
      // Extract set number and type (Weight or Reps) from the key
      const match = key.match(new RegExp(`^${shortName}(Weight|Reps)(\\d+)$`));
      if (match) {
        const type = match[1]; // "Weight" or "Reps"
        const setNumber = match[2]; // e.g., "1", "2"

        // Find or create an entry for this set
        let set = sets.find((s) => s.set === setNumber);
        if (!set) {
          set = { set: setNumber, weight: "-", reps: "-" };
          sets.push(set);
        }

        // Assign the value to weight or reps
        if (type === "Weight") {
          set.weight = metadata[key] || "-";
        } else if (type === "Reps") {
          set.reps = metadata[key] || "-";
        }
      }
    }
  }

  // If sets were found, add them to history under this date
  if (sets.length > 0) {
    // Sort sets by set number
    sets.sort((a, b) => parseInt(a.set) - parseInt(b.set));
    history.push({ date, sets });
  }
}

// Sort history by date (descending, latest first)
history.sort((a, b) => b.date.localeCompare(a.date));

// Render the table
dv.table(
  ["Date", "Sets"],
  history.map((entry) => [
    entry.date,
    entry.sets
      .map((s) => `Set ${s.set}: ${s.weight}kg, ${s.reps} reps`)
      .join("<br>")
  ])
);
```
 