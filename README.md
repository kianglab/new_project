## `new_project`

A template repository to jumpstart our lab projects. 

## About 

This is a template repository, which means it has the required folder structure and files you'll need
to create a new research project in the Kiang Lab. This template is designed to make it easy for
us to quickly create standardized project folders. The goal is to minimize mistakes and ensure
our projects are reproducible and collaborative. Here are a couple examples of [research](https://github.com/mkiang/opioid_treatment_distance) [projects](https://github.com/mkiang/airline_testing_strategies)
[that used](https://github.com/mkiang/opioid_inequities) [this same](https://github.com/mkiang/opioid_geographic) [structure](https://github.com/mkiang/disproportionate_prescribing). 

To use this template 
repository, just click on the green "Use this template" button on [the main repo
page](https://github.com/kianglab/new_project) or go to [`https://github.com/kianglab/new_project/generate`](https://github.com/kianglab/new_project/generate) and create a new repository. 

For more information, see this [blog post](https://github.blog/2019-06-06-generate-new-repositories-with-repository-templates/).

## Project structure

- **`code/`**: This folder should contain all your code. Most files should begin with a number and all files should be ordered so they can be run sequentially (e.g., `01_clean_data.R`, `02_fit_models.R`, `03_analyze_results.R`, etc.). There are usually two exceptions: `utils.R` which contains short helper functions you'll use across multiple code files and `mk_nytimes.R` or other plot themes that you'll use across multiple plotting scripts. 
- **`data/`**: In this folder are data that *can be shared* or uploaded to Github. Make sure all data files here adhere to our data use agreement for each project. 
- **`data_private/`**: In this folder are data that **cannot be shared**. Data files here will be `gitignore`d and not shared. 
- **`data_raw/`**: In this folder are the **raw** data. You should treat this folder as *read-only* when interacting with it. For example, if you use the US Census web portal to download population estimates, the files you download go here. When you read in and clean up the files, the data should be saved in `data/`. The files in this folder should **never** be manipulated by hand. Use the `README.md` file in this folder to keep important information handy (e.g., when did you access the data, what URL did you use).
- **`lit/`**: This folder should contain either the PDF of important papers we should read related to this project or URLs to those papers. Optimally, there should be a spreadsheet or document that briefly notes how each paper relates to the project. This folder is crucial for making sure everybody has the same background information. 
- **`manuscript/`**: This is where manuscripts and manuscript-related files should go. Usually, this starts with a URL link to a shared Google Doc, but before submission, this folder should contain Word or latex files. 
- **`output/`**: Many journals ask for the underlying data for each plot. This folder should contain a csv file corresponding to a plot that would allow a third-party to replicate the plot exactly. 
- **`plots/`**: This folder should contain both PDF and JPG (dpi >= 600) versions of the figures used in the manuscript. They should be named according to their order, with a very short description. For example, `fig01_overall_prevalence.pdf` or `figS10_sensitivity_analysis_by_state.pdf`.
- **`rmds/`**: Should contain rmarkdown or quarto files for the tables used in the manuscript. Tables should never be entered by hand. This both minimizes mistakes and allows us to quickly update our numbers when we received new data or change the analysis. 

## Important files
- **`/new_project.Rproj`**: This file should either be renamed to match the project folder name or deleted so you can create a new RStudio project file. 
- **`/.gitignore`**: You should add project-specific gitignore items to things that you do not want to share (e.g., if a publicly available file is too large), but it is very rarely the case that you should delete any items from the template gitignore. By default, we gitignore important files.
- **`code/secrets.R`**: This file is used to store information that is not super sensitive but that you don't want shared publicly. For example, API keys (which should be changed every project) but never identifiers for the data, location of the data on Stanford servers, or your credentials. By default, this file is gitignored so there is a `code/secrets_TEMPLATE.R` file that you can rename. 
- **`DELETEME.md`**: Delete this files before you get started. They are just here to retain the folder structure (Github will ignore empty folders). 

## How to use this template
1. [Generate a new template](https://github.com/kianglab/new_project/generate) in your own Github account.
    - This new repository should have a short but descriptive name. This is the name we will use internally to refer to this project for future meetings, notes, etc.
2. [Clone or pull the repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) so you have a local version on your computer. 
3. Delete the `DELETEME.md` and `/new_project.Rproj` files. 
4. Rename `/code/secrets_TEMPLATE.R` to `/code/secrets.R`.
5. Start filling the folders with relevant data, literature, manuscript drafts, etc.
6. Share this folder with Matt (preferable Dropbox or Google Drive). 
7. Delete the information in this README and replace it with information relevant to the project (e.g., Google Doc links, an "Objectives" statement, timeline, etc.).
