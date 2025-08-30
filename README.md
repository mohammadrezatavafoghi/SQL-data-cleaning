# SQL Data Cleaning — Tech Layoffs

This project shows beginner-friendly SQL data cleaning on a public tech layoffs dataset. The goal is to take a raw table and produce a clean, analysis‑ready table.

## Dataset
- Kaggle: https://www.kaggle.com/datasets/swaptr/layoffs-2022  
  (Download the CSV from Kaggle and load it into a table named `world_layoffs.layoffs` before running the script.)

## What’s inside
- `sql/layoffs_data_cleaning.sql` — end‑to‑end cleaning script that creates staging tables, standardizes values, and outputs a clean table (`world_layoffs.layoffs_staging2`).

## Key cleaning steps
- Make a safe copy of the raw data in a staging table.
- Remove duplicates with a `ROW_NUMBER()` window function and delete rows where `row_num > 1`.
- Standardize categorical text (e.g., unify variants of “Crypto”; trim punctuation in `country`). 
- Normalize dates by converting text to proper `DATE` using `STR_TO_DATE` and `ALTER TABLE … MODIFY`.
- Handle nulls: keep meaningful `NULL`s for analysis; drop rows where both `total_laid_off` AND `percentage_laid_off` are `NULL`.
- Deliver a final, deduplicated, typed table: `world_layoffs.layoffs_staging2`.

## How to run
1. **Create the schema and raw table** (example with MySQL):
   ```sql
   CREATE SCHEMA IF NOT EXISTS world_layoffs;
   -- Load the Kaggle CSV into world_layoffs.layoffs using your preferred method (MySQL Workbench import, `LOAD DATA INFILE`, or GUI).
   ```
2. **Run the cleaning script** in your SQL client:
   ```sql
   SOURCE sql/layoffs_data_cleaning.sql;
   -- or copy‑paste the content and run
   ```
3. **Use the cleaned table**:
   ```sql
   SELECT * FROM world_layoffs.layoffs_staging2 LIMIT 10;
   ```

## Repo structure
```
sql-layoffs-cleaning-project/
├─ sql/
│  └─ layoffs_data_cleaning.sql
├─ README.md
├─ LICENSE
└─ .gitignore
```

## Notes
- Tested with MySQL‑compatible syntax.
- Feel free to open an issue or PR with improvements (e.g., additional standardizations, constraints, or QA checks).

## License
MIT — see `LICENSE`.
