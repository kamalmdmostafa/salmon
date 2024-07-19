
# Salmon Pipeline

This README file provides detailed instructions on how to use the `flexible_salmon_pipeline_qc.sh` script for transcript quantification using the Salmon tool.

## Introduction

Salmon is a tool for quantifying the expression of transcripts in RNA-Seq data. It uses lightweight algorithms and statistical models to provide accurate transcript-level estimates of expression. Salmon's focus on speed and accuracy makes it a popular choice for large-scale transcriptomic studies, where quick turnaround times and high precision are critical. This pipeline automates the process, including cleaning the CDS FASTA file, building the index, performing quantification, and generating a quality check report.

## Prerequisites

Ensure the following tools are installed and available in your system's PATH:

- Salmon: Tool for transcript quantification
- awk: Text processing tool
- grep: Text searching tool
- sed: Text stream editor

You can install these tools using package managers like `apt`, `brew`, or `conda`.

## Usage

\`\`\`bash
./flexible_salmon_pipeline_qc.sh -cds <CDS file> -k <k-mer number> -threads <number of threads> [-genome <genome file>] [-vb]
\`\`\`

### Parameters

- `-cds`: Path to the CDS FASTA file (required)
- `-k`: K-mer size for indexing (required)
- `-threads`: Number of threads to use (required)
- `-genome`: (Optional) Path to the genome FASTA file for decoy-aware indexing
- `-vb`: (Optional) Use Variational Bayesian Optimization in quantification

### Example

\`\`\`bash
./flexible_salmon_pipeline_qc.sh -cds example.fasta -k 31 -threads 4 -genome genome.fasta -vb
\`\`\`

## Steps

1. **Check and Clean CDS FASTA File**

   The script verifies and cleans the CDS FASTA file, ensuring sequences contain only valid nucleotide characters (ATGCN) and are at least 20 nucleotides long.

2. **Build Salmon Index**

   The script builds a Salmon index using the cleaned CDS file and specified k-mer size. If a genome file is provided, a decoy-aware reference is created.

3. **Quantification**

   The script performs transcript quantification using Salmon for each paired-end sample. It supports optional Variational Bayesian Optimization.

4. **Quality Check**

   The script generates a quality check report with metrics such as the total number of reads mapped, mapping rate, the number of quantified genes (TPM > 0), and mean TPM.

## Output

- Cleaned CDS file
- Combined reference and decoy list (if genome file is provided)
- Salmon index
- Quantification results for each sample
- Quality check report

## Detailed Instructions

1. **Install Salmon**

   Follow the installation instructions for Salmon from the [official website](https://salmon.readthedocs.io/en/latest/).

2. **Prepare Your Data**

   Ensure your CDS FASTA file, genome file (if used), and paired-end RNA-Seq files (e.g., `sample_R1.fastq.gz` and `sample_R2.fastq.gz`) are in the working directory.

3. **Run the Script**

   Use the provided command-line example to run the script with your data. Adjust the parameters as needed based on your dataset.

4. **Interpret Results**

   The results will be stored in the `salmon` directory. The `qc_report.txt` file will provide a summary of the quality metrics for each sample.

## Troubleshooting

- Ensure all required tools are installed and accessible.
- Check input file paths and formats.
- Review the log files in the output directory for error messages and retry information.
