# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Hands-on series that applies Google Cloud AI features to the UCI Online Retail Dataset (UK gift and homeware wholesaler). Each part is published as a Zenn article.

- **00_setup**: Prepare data (xlsx → CSV → BigQuery `retail_ai` dataset). Shared by all parts
- **01_ai_tagging**: Tag products with categories using BigQuery AI functions (AI.GENERATE, AI.CLASSIFY, AI.EMBED)
- **02_analysis_agent**: Build an analysis agent on Gemini Enterprise Agent Platform, using the tags from 01

This repo is independent of `data-engineering-handson-gc` (the earlier DE series). It uses the same dataset and period, but must not depend on that repo's GCS bucket or `de_handson` dataset.

## Setup

```bash
uv sync
gcloud auth login
gcloud config set project YOUR_PROJECT_ID
```

Download `Online_Retail.xlsx` from the UCI repository (see `data/README.md`) and place it at `data/Online_Retail.xlsx`.

## Conventions

- BigQuery dataset: `retail_ai`, location `us-central1`
- SQL files use `${PROJECT_ID}` and are run with `bq query --use_legacy_sql=false "$(sed "s/\${PROJECT_ID}/${PROJECT_ID}/g" file.sql)"`
- Do not put comments at the top of SQL files (bq CLI parses a leading `--` as a flag)
- Tables that store AI function results are tables, not views (views would call the LLM on every read)
- Python: no docstrings; comments only for WHY; `pathlib.Path` for paths
- Lint before marking scripts done: `uv run ruff check .` must be warning-free

## Data Notes

- Period: 2010-12-01 to 2011-02-28 (3 months)
- `CustomerID` is ~34% null — treat as guest purchases
- `InvoiceNo` starting with `C` are cancellations
- Product descriptions are English, uppercase, ~25 characters on average
