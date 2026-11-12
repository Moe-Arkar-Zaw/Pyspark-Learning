# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A personal PySpark learning repository: a set of standalone Jupyter notebooks (one topic each), a reference PDF guide, Databricks screenshots, and `Troubleshooting.md` documenting setup errors and fixes. There is no package, build system, linter, or test suite — work happens inside notebooks. `README.md` lists each notebook and its topic.

## Environment

- Windows, conda-managed Python (see `.vscode/settings.json`), PySpark 4.x, JDK 17.
- PySpark needs `JAVA_HOME` pointing at JDK 17; a `[JAVA_GATEWAY_EXITED]` error means Java is missing/misconfigured, not a code bug (see `Troubleshooting.md`).
- Install: `pip install pyspark` (plus `jupyter`). Run a notebook headlessly with
  `jupyter nbconvert --to notebook --execute <notebook>.ipynb --output <out>.ipynb`.

## Notebook conventions

- Each notebook is self-contained: it creates its own session via `SparkSession.builder.appName(...).getOrCreate()` and reads a local file from the repo root with relative paths.
- Two execution contexts:
  - **Local notebooks** read CSVs in the repo root: `test1.csv` (Name, age, Experience, Salary), `test2.csv`, `test3.csv`, and `sample.xls`.
  - **Databricks notebooks** (`pyspark_with_databricks.ipynb`, `pyspark_multi_linear_regression.ipynb`) read Unity Catalog tables via `spark.sql("select * from workspace.default.<table>")` (`test_1`, `tips`) and use `df.display()`. They are not runnable locally as-is; `tips.csv` is the local copy of the `tips` table.
- `sample.xls` is actually a **tab-separated text file**, not Excel — read it with `spark.read.option("header", True).option("sep", "\t").csv("sample.xls")`.
- ML notebooks follow the Spark ML pattern: `StringIndexer` for categorical columns → `VectorAssembler` into a features column → `randomSplit` → `LinearRegression`.

## Data files are git-ignored

`.gitignore` excludes `sample.xls`, `test1.csv`, `test2.csv`, `test3.csv`, `tips.csv`, and `.vscode/`. These exist only locally (`test2.csv`, used by `pyspark_handling_missing_values.ipynb`, may be absent). Don't assume they're in version control.

## Troubleshooting log

When a new setup/runtime error is resolved, the user records it in `Troubleshooting.md` using the existing format: Environment, Error, Cause, Solution, Note.
