# genome-editing-assay-design-and-analysis
Genome Editing Assay Design and Analysis Pipeline

Project Overview

This repository presents an end-to-end workflow for validating genome editing for the EMX1 locus, a canonical benchmarking target for CRISPR-Cas-9 genome editing, uses PCR-based assays, Sanger sequencing, and amplicon next-generation sequencing (NGS). The project is designed to reflect the analytical, quality control, and reporting practices of a genome engineering or molecular biology core facility.

The workflow integrates:

PCR assay design
Sanger sequencing interpretation
Targeted amplicon NGS analysis
Digital PCR (dPCR) assay metadata
Explicit QC thresholds and pass/fail logic
Client-ready, service-oriented reporting

All analyses use publicly available or simulated data and are intended for demonstration and training purposes.

Biological Background

Genome editing technologies such as CRISPR-Cas9 introduce targeted double-strand breaks that are repaired primarily through non-homologous end joining (NHEJ), resulting in insertions and deletions (indels) at the cut site. Accurate validation of these events is essential for confirming editing efficiency, determining functional consequences (e.g., frameshift vs in-frame mutations), and identifying potential unintended outcomes.

The EMX1 locus is one of the most widely used targets for benchmarking CRISPR-Cas9 editing efficiency and indel profiling. It is frequently cited in foundational genome editing literature and is commonly used by core facilities to validate new assays, pipelines, and technologies.

Using EMX1 allows this project to focus on assay design, analytical rigor, QC, and reporting, rather than target-specific biology

Repository Structure

genome-editing-assay-design-and-analysis/

├── assay_design/

├── primers.csv
└── dpcr_assays.csv

├── data/

│   ├── reference/
│   │   └── EMX1_reference.fasta
│   ├── amplicon_ngs/
│   │   └── metadata/
│   │       └── sample_sheet.csv
│   └── dpcr/
│       └── metadata/
│           └── dpcr_sample_sheet.csv

├── analysis/

│   ├── notebooks/
│   │   └── demo_analysis_EMX1.ipynb
│   └── utils/
│       ├── helper_functions.py
│       └── dpcr_qc.py

├── qc/

│   └── qc_metrics.md
├── results/
│   ├── qc_summary.csv
│   ├── editing_summary.csv
│   ├── sanger_qc_summary.csv
│   └── dpcr_summary.csv
└── README.md

Assay Design Strategy
PCR assays were designed to flank the expected CRISPR cut site, enabling detection of indels by both Sanger sequencing and amplicon NGS.

Two assay types are defined:

Sanger sequencing assay (~400–450 bp) for rapid qualitative screening

Amplicon NGS assay (~250–300 bp) for quantitative indel profiling

Primer sequences, amplicon sizes, melting temperatures, and design rationale are documented in:

assay_design/primers.csv



Sample Metadata

All sequencing and dPCR workflows are metadata-driven.

Metadata files:

data/amplicon_ngs/metadata/sample_sheet.csv

data/dpcr/metadata/dpcr_sample_sheet.csv

Metadata include:

Sample identifiers and technical replicates

Edited vs unedited controls

Expected editing efficiency

Platform and run information

This project is provided for demonstration and educational purposes.


Analysis Workflow (EMX1)

1. Amplicon NGS Analysis
   
Read-level QC (depth, quality, mapping rate)

Alignment to EMX1 reference sequence

Indel calling and size distribution

Frameshift vs in-frame classification

Editing efficiency estimation

Replicate concordance assessment

Outputs:

results/qc_summary.csv

results/editing_summary.csv


2. Sanger Sequencing Analysis
   
Representative or simulated Sanger traces

Identification of mixed chromatogram peaks near the cut site

Qualitative confirmation of editing

Sanger-specific QC (read length and trace quality)

Outputs:

results/sanger_qc_summary.csv


3. Digital PCR (dPCR) Integration
   
Dropout-style dPCR assay spanning the EMX1 cut site

Reference assay for normalization

Poisson-based estimation of copies/µL

Editing fraction calculated as:

editing ≈ 1 − (WT_target / reference)


dPCR QC includes:


Minimum accepted droplet counts

Saturation checks

Control background editing limits

Replicate concordance thresholds


Outputs:

results/dpcr_summary.csv

results/dpcr_qc_summary.csv

results/dpcr_replicate_concordance.csv


Quality Control Framework


QC is treated as a first-class deliverable, consistent with shared resource laboratory standards.

QC metrics include:


Sequencing read depth and base quality

Mapping efficiency

Background indel rates in controls

Replicate concordance

Sanger trace interpretability

dPCR droplet counts and saturation


Explicit QC thresholds and pass/fail logic are documented in:

qc/qc_metrics.md
