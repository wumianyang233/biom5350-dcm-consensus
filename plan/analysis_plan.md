# Analysis plan: DCM versus non-failing hearts

## Objective

Identify genes differentially expressed in dilated cardiomyopathy (DCM) compared with non-failing controls in GSE5406 and GSE42955. Analyze the studies separately because they use different platforms, then identify gene symbols that are significant in both studies and have the same expression direction.

## Studies and sample selection

Use only samples explicitly labeled as DCM or non-failing/normal controls. Exclude ischemic cardiomyopathy (ICM) samples. Verify the sample labels against GEO metadata and match the selected GSM accessions to matrix columns before analysis. Save a sample information table for each study with the GSM, original label, assigned group, inclusion status, and reason for the decision. Do not remove any other sample without checking and documenting why.

The previously reviewed labels indicate the following expected counts; confirm them against the matrices before analysis:

| Study | DCM | Controls | ICM excluded |
| --- | ---: | ---: | ---: |
| GSE5406 | 86 | 16 | 108 |
| GSE42955 | 12 | 5 | 12 |

## Processed expression matrices

Use the GEO processed matrix for a study only when its platform and feature identifiers, sample labels, normalization status, and log2 scale can be verified. Check that matrix columns correspond to the selected samples. Do not switch to raw data, another processed source, or a different processing method if these checks fail; pause and ask for direction.

Do not overwrite or alter existing files in `data/raw/`, and do not commit raw data. Any future data acquisition is outside this plan-writing commit and must follow the project instructions.

## Probe filtering and annotation

Remove platform control probes using platform annotation. Retain biological probes in probe-level results, including probes with ambiguous or unmapped gene symbols. Record the annotation source and version, and include probe identifiers and available annotation fields in the output tables.

Inspect the matrix and annotation before deciding on any additional probe filtering. Present the proposed rule and its effect for approval before applying any additional filter. Do not exclude samples or probes for other reasons without checking and explaining the decision.

## Quality control

For each study, create sample-level quality-control plots that include expression distributions, PCA, MDS, and sample clustering. Report possible sample outliers and the plot evidence. Flagging an outlier does not remove it; obtain approval before excluding any sample.

For PCA, MDS, and clustering, inspect missingness and feature variance first. Use probes with finite values across all included samples for these QC calculations, and omit zero-variance probes from those calculations. Report the number of features omitted for missing or non-finite values and for zero variance. Do not impute values by default. If missingness prevents a useful QC calculation, pause and ask before choosing an imputation or alternative method. These QC-only feature omissions do not by themselves filter the differential-expression input.

## Differential expression

Analyze each study independently with limma. Use disease status as the sole model term, with no covariates or batch correction. Estimate the DCM-minus-control contrast, so a positive log2 fold change means higher expression in DCM. Use Benjamini-Hochberg adjustment across tested biological probes within each study and define significance as adjusted $p < 0.05$, with no additional log2 fold-change cutoff.

Save the complete probe-level limma table for each study, including non-significant probes and retained ambiguous or unmapped probes. Also save the selected gene-symbol table and significant subsets at both probe and gene-symbol levels.

## Probe-to-gene selection and consensus

Within each study, select one probe per gene symbol by the smallest adjusted $p$-value. If probes tie on adjusted $p$-value, select the one with the larger absolute log2 fold change; if still tied, select the lexically first probe ID. Document this rule and retain the original probe-level table for review.

The consensus list contains gene symbols whose selected probe has adjusted $p < 0.05$ in both studies and whose log2 fold changes have the same sign. Match on gene symbol. Exclude ambiguous or unmapped probes from the gene-symbol tables and consensus list. Include each study's selected probe ID, log2 fold change, and adjusted $p$-value in the consensus output.

## Notebooks, outputs, and reproducibility

Use three Jupyter notebooks with an R kernel: one for each study and a separate consensus notebook. Add short comments explaining code steps. Record package versions and include `sessionInfo()` in each notebook.

Save sample information and result tables as CSV files, and QC plots as PNG or PDF. Planned outputs include:

- `notebooks/GSE5406_analysis.ipynb`
- `notebooks/GSE42955_analysis.ipynb`
- `notebooks/consensus_analysis.ipynb`
- `results/tables/GSE5406_sample_info.csv` and `results/tables/GSE42955_sample_info.csv`
- Complete probe-level limma tables for both studies
- Full selected gene-symbol tables for both studies
- Significant probe-level and gene-symbol subsets for both studies
- `results/tables/consensus_genes.csv`
- Study-specific QC figures in `results/figures/`

## Approval gates and scope

After approval of this plan, validate the processed matrices. If any required validation fails, pause and ask before trying another approach. After inspecting matrix and annotation characteristics, present any proposed additional probe filtering for approval before applying it. Flagged sample outliers also require approval before exclusion. No expression data will be downloaded and no analysis will be run as part of saving and committing this plan.
