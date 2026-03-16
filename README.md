## `new_project`

A template repository to jumpstart projects in the [Kiang Lab](https://kianglab.com).

## About

This is a template repository, which means it has the required folder structure and files you'll need to create a new research project in the [Kiang Lab](https://kianglab.com). This template is designed to make it easy for all of us to quickly create standardized project folders. The goal is to minimize mistakes, allow for smooth collaboration, and ensure our projects are reproducible. Here are a couple examples of [research](https://github.com/mkiang/opioid_treatment_distance) [projects](https://github.com/mkiang/airline_testing_strategies) [that used](https://github.com/mkiang/opioid_inequities) [this](https://github.com/mkiang/modeling_reemergence) [same](https://github.com/mkiang/opioid_geographic) [structure](https://github.com/mkiang/disproportionate_prescribing).

For more on the rationale behind this template, see our lab manual appendices on [project structure and workflow](https://kianglab.github.io/labmanual/projectstructure.html) and [R code style](https://kianglab.github.io/labmanual/codestyle.html).

To use this template repository, just click on the green "Use this template" button on [the main repo page](https://github.com/kianglab/new_project) or go to [`https://github.com/kianglab/new_project/generate`](https://github.com/kianglab/new_project/generate) and create a new repository. (See this [GitHub blog post](https://github.blog/2019-06-06-generate-new-repositories-with-repository-templates/) for more.)

### File paths

Note: [`{here}`](https://here.r-lib.org/) is a core dependency in all our projects. `here::here()` builds file paths relative to the project root (anchored by the `.Rproj` file), so paths work on any machine without hard-coding. This is especially important because our projects often spread across multiple environments (e.g., linux on Stanford servers, macOS locally, Windows for a collaborator, etc.). Use `here::here("data", "clean.csv")` instead of `"data/clean.csv"` or absolute paths. Never use `setwd()`. See the lab manual's [project structure appendix](https://kianglab.github.io/labmanual/projectstructure.html#projectstructure-setwd) for more.

## Project structure

- **`code/`**: This folder should contain all your code. Most files should begin with a number and all files should be ordered so they can be run sequentially (e.g., `01_clean_data.R`, `02_fit_models.R`, `03_analyze_results.R`, etc.). There are usually two exceptions: `utils.R` which contains short helper functions you'll use across multiple code files and `mk_nytimes.R` or other plot themes that you'll use across multiple plotting scripts.
- **`data/`**: In this folder are intermediate processed data that *can be shared* or uploaded to Github — cleaned datasets, merged files, model outputs that downstream scripts consume. Make sure all data files here adhere to our data use agreement for each project. Every file here should be produced by a script in `code/` — never edited by hand.
- **`data_private/`**: In this folder are data that **_cannot_ be shared**. Data files in this folder will be `.gitignore`d and not shared. See `data_private/README.md` for prompts to document IRB numbers, DUA constraints, and data destruction deadlines.
- **`data_raw/`**: In this folder are the **raw** data. You should treat this folder as *read-only* when interacting with it. For example, if you use the US Census web portal to download population estimates, the files you download go here. When you read in and clean up the files, the data should be saved in `data/`. The files in this folder should **never** be manipulated by hand. Use the `README.md` file in this folder to keep important information handy (e.g., when did you access the data, what URL did you use).
- **`lit/`**: This folder should contain either the PDF of important papers we should read related to this project or URLs to those papers. Optimally, there should be a spreadsheet or document that briefly notes how each paper relates to the project. This folder is crucial for making sure everybody has the same necessary background information.
- **`manuscript/`**: This is where manuscripts and manuscript-related files should go. Usually, this starts with a URL link to a shared Google Doc, but before submission, this folder should contain Word or latex files to be submitted (along with pdf and jpg versions of figures if the journal submission portal allows it).
- **`output/`**: Many journals ask for the underlying data for each plot. This folder should contain a csv file corresponding to a figure or table that would allow a third-party to replicate it exactly. The distinction from `data/` is that `output/` holds *final* numerical results behind specific figures and tables, while `data/` holds intermediate processed datasets consumed by downstream scripts.
- **`plots/`**: This folder should contain both PDF and JPG (dpi >= 600) versions of the figures used in the manuscript. They should be named according to their order, with a very short description. For example, `fig01_overall_prevalence.pdf` or `figS10_sensitivity_analysis_by_state.pdf`.
- **`qmd/`**: Should contain Quarto (or rmarkdown) files and their resulting output files for the tables used in the manuscript. Tables should never be entered by hand. This both minimizes mistakes and allows us to quickly update our numbers when we receive new data or change the analysis.

### Data flow

Each script in `code/` does one job: read input files, do some work, write output files. Scripts communicate through files on disk, not objects in memory.

```
data_raw/ ──→ code/01_clean_data.R   ──→ data/
data/     ──→ code/02_fit_models.R   ──→ output/
output/   ──→ code/03_make_figures.R ──→ plots/
output/   ──→ qmd/table01.qmd       ──→ qmd/table01.html
```

## Important files

- **`/new_project.Rproj`**: This file should be renamed to match the project folder name or deleted so you can create a new RStudio project file. The template ships with `RestoreWorkspace: No`, `SaveWorkspace: No`, and `AlwaysSaveHistory: No` — these ensure R starts with a clean environment every time, which is critical for reproducibility.
- **`/.gitignore`**: You should add project-specific gitignore items to things that you do not want to share (e.g., if a publicly available file is too large), but it is very rarely the case that you should delete any items from the template gitignore. By default, we gitignore private data, secrets, `{renv}` libraries, Quarto build artifacts, and common large binary formats (parquet, duckdb, etc.).
- **`/config.yml`**: Project-level parameters (date ranges, core counts, data paths, analysis flags). Read with `{config}` via `config::get()`. Centralizing parameters means changing a date range or toggling a sensitivity analysis requires editing one file, not hunting through every script.
- **`code/secrets.R`**: This file is used to store information that is not super sensitive but that you don't want shared publicly. For example, API keys (which should be changed every project), proprietary column names of restricted data, location of data on secure Stanford servers, other credentials you may need in your code. By default, this file is `.gitignore`d so there is a `code/secrets_TEMPLATE.R` file that you can rename.
- **`code/utils.R`**: Shared helper functions used across multiple scripts. Source it with `source(here::here("code", "utils.R"))`. If a helper grows complex enough to need its own documentation or tests, move it to a package.
- **`renv.lock`**: Machine-readable record of package dependencies (committed to Git). Run `renv::restore()` to reproduce the exact package environment. See the `{renv}` section below.

## How to use this template

1. [Generate a new template](https://github.com/kianglab/new_project/generate) in your own Github account.
    - This new repository should have a short but descriptive name. This is the name we will use internally to refer to this project for future meetings, notes, etc.
2. [Clone or pull the repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) so you have a local version on your computer.
3. Delete the `DELETEME.md` and rename `/new_project.Rproj` to match your project name.
4. Rename `/code/secrets_TEMPLATE.R` to `/code/secrets.R`.
5. Update `config.yml` with your project-specific parameters (date ranges, core counts, data paths).
6. Initialize `{renv}`: open the project in RStudio, run `renv::init()`, then `renv::snapshot()`.
7. Start filling the folders with relevant data, literature, manuscript drafts, etc.
8. Share this folder with Matt (preferably Dropbox or Google Drive).
9. Replace this README with information relevant to the project (e.g., project title, objectives, data sources, how to run the analysis, timeline, Google Doc links). See the example projects linked above for what a finished project README looks like.

## Credits

Special thanks to early testers of this repository who provided useful feedback: 

-   Esther Velasquez
-   Anna Nguyen
-   Julianna Hsing
-   Amy Mann
