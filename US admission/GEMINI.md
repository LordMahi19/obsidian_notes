# Directory Overview

This directory is an [Obsidian](https://obsidian.md/) vault used to organize research and track applications for Master of Science programs in the United States, with a focus on Computer Science. It uses the Obsidian Dataview plugin to create dynamic tables and organize information about different universities.

The primary goal is to identify affordable universities and programs that offer funding opportunities like Graduate, Teaching, or Research Assistantships (GA/TA/RA).

# Key Files

*   **`Database.md`**: This is the main dashboard. It uses the Dataview plugin to generate a sortable table of all universities from the `university/` directory. The table displays application status, state, and yearly tuition.

*   **`Deep research.md`**: This file contains detailed research in two main tables:
    1.  A list of affordable universities with estimated tuition fees.
    2.  A list of universities known for providing full funding (tuition waivers and stipends) for Master's students.

*   **`visualisation.html`**: An HTML file that contains data visualizations (graphs) based on the data collected in `Deep research.md`.

*   **`university/` (directory)**: This directory contains individual Markdown notes for each university. Each note is expected to contain YAML frontmatter (metadata) that is used by `Database.md`.
    *   **Example Metadata:**
        ```yaml
        ---
        type: university
        status: "Not Started"
        state: "Illinois"
        tuition: 17823
        ---
        ```

*   **`states/` (directory)**: This directory contains notes that group universities by state, providing a state-level overview of the available programs and their costs.

# Usage

This Obsidian vault is designed to be a central hub for university application tracking.

1.  **Adding a New University**: To add a new university, create a new Markdown file in the `university/` directory (e.g., `university/New_University.md`).
2.  **Add Metadata**: At the top of the new file, add the YAML frontmatter with the required fields (`type`, `status`, `state`, `tuition`).
3.  **View the Database**: The `Database.md` file will automatically update to include the new university in its table.
4.  **Conduct Research**: Use the `Deep research.md` file to add and compare information about funding, program details, and application links.
