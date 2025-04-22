The following query, brings in the pending tasks from my vault. It excludes templates, [[Birthday Listing]], empty tasks, and #todo/dailyQuest

```dataviewjs
// Step 1: Get all files with tasks, filter tasks later
const filesWithTasks = dv.pages()
  .where(p => p.file.tasks.length > 0);

// Step 2: Sort files by taskSortPriority
const sortedFiles = filesWithTasks.sort(f => f.taskSortPriority === "low" ? 1 : 0, "asc");

// Step 3: Render tasks per file with filtering
for (const file of sortedFiles) {
  const filteredTasks = file.file.tasks
    .where(t => !t.completed
      && !t.path.includes("birthdays")
      && !t.path.includes("templates")
      && !t.tags.includes("#todo/dailyQuest")
      && t.text !== ""
	  && !/^⏳ ?\d{4}-\d{2}-\d{2}$/.test(t.text)
    ); 
  if (filteredTasks.length > 0) {
    dv.header(3, file.file.link);
    dv.taskList(filteredTasks, false);
  }
}
```
