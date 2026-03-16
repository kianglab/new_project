## `data/`

Processed (analysis-ready) data files live here. Every file should be produced by a script in `code/` — never edited by hand.

### Data dictionary

| File | Description | Produced by | Date |
|------|-------------|-------------|------|
| `example.csv` | _Brief description_ | `01_clean_data.R` | _YYYY-MM-DD_ |

### Notes

- Files in this folder **can** be shared publicly (e.g., pushed to GitHub).
- If a file is too large for GitHub (>100 MB), add it to `.gitignore` and note the alternative location here.
- Raw, unmodified source data belongs in `data_raw/`. Restricted-access data belongs in `data_private/`.
