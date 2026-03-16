## `data_raw/`

Original, unmodified source data. Treat this folder as **read-only** — scripts read from here but never write to it.

### Data sources

| File | Source | URL / Citation | Date accessed | Notes |
|------|--------|----------------|---------------|-------|
| `example.csv` | _e.g., US Census Bureau_ | _URL or DOI_ | _YYYY-MM-DD_ | _Version, filters applied, etc._ |

### Notes

- Never modify files in this folder by hand. Download the data, drop it here, and document it in the table above.
- If the source data is too large for GitHub, add it to `.gitignore` and record the download instructions here so a collaborator can reproduce your setup.
- Restricted-access data belongs in `data_private/`, not here.
