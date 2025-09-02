# Narwhals_data_frames

[Narwhals](https://github.com/narwhals-dev/narwhals) is a new Python library that acts as a unified API layer for different DataFrame backends like pandas, polars, and Modin. It lets you write one codebase that works seamlessly across these backends, which can be really handy, where datasets are often large and workflows need to be scalable.


# Summary

This notebook demonstrates a scalable bioinformatics workflow for analyzing **rare loss-of-function (LoF) variants** across samples and genes. It uses [**Narwhals**](https://github.com/narwhals-dev/narwhals/) — a **unified dataframe API** — to write code once and run seamlessly on either **Polars** (fast, efficient) or **Pandas** (flexible, widely used).

The goal of this pipeline is to:
1. **Read** variant call data from `.tsv` or `.parquet` files.
2. **Filter** variants to identify rare LoF events based on allele frequency (`AF`) thresholds.
3. **Annotate** variants into frequency buckets (`ultra_rare`, `rare`, `common`).
4. **Aggregate** per-sample, per-gene burden counts.
5. **Pivot** the data into a **sample × gene burden matrix**.
6. **Join** with sample metadata to generate a final **design matrix** for downstream modeling.


Why this shows Narwhals’ uniqueness:
- Write once, scale later: Prototype on a laptop with pandas; switch to polars for large cohorts—all transformations stay identical.
- Declarative expressions: Clear, composable feature engineering without backend-specific .apply functions.
- Robust IO & interop: CSV/TSV now, Arrow/Parquet later—same API. Great fit for variant tables, gene counts, cell metadata, etc.
- Consistent wide-table shaping: Pivots, joins, groupbys, and window ops behave uniformly—critical in pipelines that hop between wide (sample×gene) and long (tidy) layouts.
- Optional laziness: When the backend supports it (polars), you get optimization and pushdown “for free.”