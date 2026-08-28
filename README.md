# RNA-seq Differential Expression and Pathway Analysis

A transcriptomics pipeline covering read quality control through differential expression to
GO pathway enrichment, implemented across R and Python.

## Pipeline

```
raw reads (public SRA)
   -> FastQC per-sample QC
   -> MultiQC aggregate report
   -> alignment / quantification
   -> differential expression        (differential_expression.Rmd / .R)
   -> Ensembl ID -> gene symbol map  (notebooks/ensembl_id_converter.ipynb)
   -> GO pathway enrichment          (notebooks/go_pathway_analysis.ipynb)
   -> GO term reduction              (notebooks/go_term_reduction.ipynb)
```

The **GO term reduction** step is the part most pipelines skip. Raw enrichment output is
dominated by redundant, nested parent terms; collapsing them is what turns a list of
hundreds of significant terms into a readable biological story.

## Contents

| File | Purpose |
|---|---|
| `differential_expression.Rmd` | Main analysis, knits to an HTML report |
| `differential_expression.R` | Same logic as a plain script |
| `notebooks/qc_and_alignment.ipynb` | Read QC and alignment workflow |
| `notebooks/ensembl_id_converter.ipynb` | Ensembl gene ID to gene symbol mapping |
| `notebooks/go_pathway_analysis.ipynb` | GO over-representation analysis on DEGs |
| `notebooks/go_term_reduction.ipynb` | Collapsing redundant GO terms |

## Data

Public data only. Sequencing reads are **not** committed - they are large and freely
retrievable. Pull them from the SRA accession referenced in the notebooks, or use the
GEO series matrix for the expression-level analysis.

## Stack

R (Bioconductor, DESeq2-style workflow, R Markdown), Python (pandas, GO enrichment
libraries), FastQC, MultiQC.
