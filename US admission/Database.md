# University Application Database

This note uses the Dataview plugin to collect all notes with `type: university` in their metadata and displays them in a table.

```dataview
TABLE
    status as "Application Status",
    state as "State",
    tuition as "Yearly Tuition (USD)"
FROM ""
WHERE type = "university"
SORT tuition ASC
```

### How it Works:

-   `TABLE ...`: This specifies you want to create a table. The lines that follow define the columns. `status as "Application Status"` creates a column with the header "Application Status" using the `status` metadata field from each note.
-   `FROM ""`: This tells Dataview to search in all folders in your vault.
-   `WHERE type = "university"`: This is the filter. It only includes notes that have `type: university` in their frontmatter metadata.
-   `SORT tuition ASC`: This sorts the resulting table by the `tuition` field in ascending order.

You can create as many university notes as you want following the same pattern, and this table will update automatically.
