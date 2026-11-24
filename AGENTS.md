\# Project

Find genes consistently differentially expressed in DCM compared with non-failing hearts across GSE5406 and GSE42955.

\# Data

\- Human left ventricular heart tissue.

\- GSE5406: GPL96, 86 DCM and 16 controls.

\- GSE42955: GPL6244, 12 DCM and 5 controls.

\- Exclude ischemic cardiomyopathy samples from both comparisons.

\- Check GEO sample labels and metadata before analysis.

\# Conventions

\- Use R, with tidyverse for data handling and plots where possible.

\- Use tidyverse verbs such as `filter()`, `left_join()`/`inner_join()`, `arrange()`, and `distinct()` for table filtering, joining, sorting, and deduplication whenever practical; use base R when it is clearer or required by the analysis.

\- Add short comments explaining why each step is needed, especially for filtering, transformations, model settings, and output generation.

\- Use limma for differential expression and adjusted p &lt; 0.05.

\- Compare genes across studies using gene symbols and matching expression directions.

\# Layout

\- notebooks/: analysis notebooks

\- plan/: analysis plan

\- results/figures/: QC plots

\- results/tables/: result tables

\- chat/: AI conversations

\- worksheets/: class worksheets

\- data/raw/: downloaded data

\# Boundaries

\- Do not modify files in data/raw/ or commit raw data.

\- Do not run analyses or download data before I approve the plan.

\- Do not exclude samples without checking and explaining why.

