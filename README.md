 catena-retail
Batch and event data pipelines with data quality checks, built in Databricks with PySpark


 Environment
- Databricks Free Edition
- PySpark for the pipelines, Spark SQL for the modelling
- Raw files loaded into a Unity Catalog volume
- Cleaned output written as Parquet, partitioned by order year and month

 Repository structure
- 01_batch_ingestion` covers Task 1 and Task 2: ingest and clean orders and customers, run data quality checks, write partitioned Parquet
- 02_event_processing` covers Task 3: parse the clickstream and compute session metrics per customer
- 03_star_schema_sql` covers Task 4: star schema DDL and the four analytics queries


Approach
Read the raw files as text, check what is actually wrong, clean each issue, run quality checks, then write the cleaned output. The key decisions and assumptions are in the submission document.

 Data quality notes
The pipeline handles currency strings, mixed date formats, nulls, duplicates, and an orphaned customer reference. The orphaned order is kept and flagged rather than dropped, so revenue is not silently lost. Six of the seven quality checks pass. The referential integrity check fails by design, to surface the orphaned reference rather than hide it.

 How to run
Open the notebooks in Databricks and run them in order (01, 02, 03) If your catalog or schema names differ, update the volume path at the top of each notebook.
