```
# DCM Gene Expression Analysis

## Project
This project compares gene expression between dilated cardiomyopathy (DCM) and non-failing hearts using GSE5406 and GSE42955.

## Reproducing the Analysis
Run these R notebooks in order:
1. notebooks/GSE5406_analysis.ipynb
2. notebooks/GSE42955_analysis.ipynb
3. notebooks/Consensus_analysis.ipynb

Download the GEO data as described in the notebooks. Raw and processed data files are not included in GitHub.

## Results
One consensus gene was identified: AASS, downregulated in DCM in both studies.

The results are saved in results/tables/.

## AI Use
I used CoCalc Codex with GPT-6-luna on November 24, 2026 to plan the analysis, generate R code, explain the methods, and improve the code.

I checked sample counts, expression scales, QC results, and significant gene counts. I also reran the notebooks and compared results before and after code restyling.

## Limitations and Trust

Verified myself:
- Sample counts and GEO group labels
- Main differential expression results
- Consensus gene direction

Tested by rerunning:
- Study 1 and Study 2 notebooks
- Consensus notebook
- Results comparison after restyling

Took on faith:
- Accuracy of GEO annotations
- Original normalization performed by GEO submitters
- Some assumptions of the statistical model

The studies use different platforms and sample sizes, which may affect the consensus results.

```
