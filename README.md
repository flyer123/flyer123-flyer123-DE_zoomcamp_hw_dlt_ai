## Workshop Instructions

[](https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/cohorts/2026/workshops/dlt/README.md#workshop-instructions)

### Step 1: Create a New Project Folder

[](https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/cohorts/2026/workshops/dlt/README.md#step-1-create-a-new-project-folder)

Create a fresh folder for your pipeline and open it in Cursor (or your preferred agentic IDE):

mkdir my-dlt-pipeline
cd my-dlt-pipeline

### Step 2: Add the dlt MCP Server Config

[](https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/cohorts/2026/workshops/dlt/README.md#step-2-add-the-dlt-mcp-server-config)

Choose the setup for your IDE:

Cursor - go to **Settings → Tools & MCP → New MCP Server** and add:

    {
      "mcpServers": {
        "dlt": {
          "command": "uv",
          "args": [
            "run",
            "--with",
            "dlt[duckdb]",
            "--with",
            "dlt-mcp[search]",
            "python",
            "-m",
            "dlt_mcp"
          ]
        }
      }
    }



### Step 3: Install dlt Workspace

[](https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/cohorts/2026/workshops/dlt/README.md#step-3-install-dlt-workspace)

    pip install "dlt[workspace]"

### Step 4: Initialize the dlt Project



    dlt init dlthub:open_library duckdb

This scaffolds the pipeline files and configuration for Open Library. You now have everything you need to start prompting.

> 📖 **Reference:** [Open Library Workspace Instructions](https://dlthub.com/workspace/source/open-library)

### Step 5: Prompt the Agent to Build and Run the Pipeline

[](https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/cohorts/2026/workshops/dlt/README.md#step-5-prompt-the-agent-to-build-and-run-the-pipeline)

This is where the magic happens. The `dlt init` command scaffolds sample prompts you can use. Here's an example to get started:

```

   

 Please generate a REST API Source for Open Library API, as specified in @open_library-docs.yaml
    Start with endpoint(s) books and skip incremental loading for now.
    Place the code in open_library_pipeline.py and name the pipeline open_library_pipeline.
    If the file exists, use it as a starting point.
    Do not add or modify any other files.
    Use @dlt rest api as a tutorial.
    After adding the endpoints, allow the user to run the pipeline with python open_library_pipeline.py and await further instructions.

```

### Step 6: Debug with the Agent

If there are any errors, paste them into the chat and let the AI resolve them. This is the power of AI-assisted development: you iterate quickly without getting stuck.

### Step 7: Inspect Pipeline Data with the dlt Dashboard


Once your pipeline runs successfully, launch the dashboard to inspect your data and metadata:

    dlt pipeline open_library_pipeline show

This opens a web app where you can:

-   View pipeline state and run history
-   Explore schemas, tables, and columns
-   Query the loaded data
-   Debug any issues


### Step 8: Inspect the Pipeline via Chat

[](https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/cohorts/2026/workshops/dlt/README.md#step-8-inspect-the-pipeline-via-chat)

With the dlt MCP server configured, you can ask the AI about your pipeline directly:

    "What tables were created in the pipeline?"  
    "Show me the schema for the books table."  
    "How many rows were loaded?"

The agent has access to your pipeline metadata and can answer these questions.

### Step 9 (Bonus): Build Visualizations with marimo + ibis


Take your analysis further by creating interactive reports with [marimo](https://marimo.io/) notebooks and [ibis](https://ibis-project.org/).

Prompt the agent to build a visualization:

     "Create a marimo notebook that visualizes the top 10 authors by book count. Use ibis for data access. Reference: [https://dlthub.com/docs/general-usage/dataset-access/marimo](https://dlthub.com/docs/general-usage/dataset-access/marimo)"

By providing the docs link, the agent will use the correct stack.

Run your notebook:

# Edit mode (for development)

    marimo edit your_notebook.py

# Run mode (view the report)

    marimo run your_notebook.py


