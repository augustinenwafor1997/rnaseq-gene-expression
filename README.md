# RNA-seq Differential Expression and Pathway Analysis

A transcriptomics workflow covering read quality control, differential expression and GO
pathway enrichment, implemented across R and Python.

## Pipeline

```
raw reads (public SRA)
  -> FastQC per-sample QC
  -> MultiQC aggregate report
  -> alignment and quantification
  -> differential expression          differential_expression.Rmd / .R
  -> Ensembl ID to gene symbol map    notebooks/ensembl_id_converter.ipynb
  -> GO pathway enrichment            notebooks/go_pathway_analysis.ipynb
  -> GO term reduction                notebooks/go_term_reduction.ipynb
```

GO enrichment output contains many redundant and nested parent terms, so the final step
collapses them into a smaller set before interpretation.

## Files

| File | Purpose |
|---|---|
| `differential_expression.Rmd` | Main analysis, knits to an HTML report |
| `differential_expression.R` | Same logic as a plain script |
| `notebooks/qc_and_alignment.ipynb` | Read QC and alignment |
| `notebooks/ensembl_id_converter.ipynb` | Ensembl gene ID to gene symbol mapping |
| `notebooks/go_pathway_analysis.ipynb` | GO over-representation analysis on DEGs |
| `notebooks/go_term_reduction.ipynb` | Collapsing redundant GO terms |

## Data

Public data only. Sequencing reads are not committed; retrieve them from the SRA accession
referenced in the notebooks, or use the GEO series matrix for the expression-level analysis.

## Stack

R (Bioconductor, R Markdown), Python (pandas, GO enrichment libraries), FastQC, MultiQC.
