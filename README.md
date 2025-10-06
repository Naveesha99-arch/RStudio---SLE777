README -SLE777 Applied Bioinformatics - Assessment 4 (R Project)
Below, “script” refers to the corresponding code section in the R Markdown file. If you choose to split them into separate .R files, the purposes/inputs/outputs are the same.

0) Setup & Data download (used by multiple answers)

Purpose
Create project folders; download or point to the required input files; load packages.

Inputs
URLs for:
gene_expression.tsv and growth_data.csv (provided by unit GitHub)
CDS FASTA links for:
Escherichia coli K-12 MG1655 (CDS file: *_cds*.fa.gz)
Oxalobacter formigenes OXCC13 (GCA_000158495; CDS file: *_cds*.fa.gz)

Outputs
Files saved under data/
Package loaded: seqinr

Part 1 — R data analysis (gene expression & tree growth)

1.1) Read RNA-seq counts & first six genes

Purpose: Read gene_expression.tsv, set gene IDs as row names, show first 6 genes.
Inputs: data/gene_expression.tsv
Outputs: Printed preview table in the knitted report.

1.2) Mean expression column & first six genes

Purpose: Compute row means across samples, append as mean, print first 6.
Inputs: object from 1.1
Outputs: Printed preview table.

1.3) Top 10 genes by mean expression

Purpose: Identify 10 highest mean-expressed genes.
Inputs: object from 1.2
Outputs: Printed 10-row table.

1.4) Count of genes with mean < 10

Purpose: Simple threshold count.
Inputs: object from 1.2
Outputs: A single number printed.

1.5) Histogram of mean expression

Purpose: Visualize distribution of mean counts.
Inputs: object from 1.2
Outputs: Histogram embedded in report (optionally saved as output/expr_mean_hist.png if you keep that line).

1.6) Load tree growth CSV & column names

Purpose: Read growth_data.csv and report header/column names.
Inputs: data/growth_data.csv
Outputs: Printed vector of column names.

1.7) Mean & SD of circumference at start/end (by site)

Purpose: Compute mean/SD for 2005 (start) and 2020 (end) grouped by Site.
Inputs: data/growth_data.csv (columns: Site, Circumf_2005_cm, Circumf_2020_cm)
Outputs: Table with columns site, start_mean, start_sd, end_mean, end_sd.

1.8) Boxplot of circumference at start/end (by site)

Purpose: Compare distributions for 2005 vs 2020 across sites.
Inputs: same as 1.7
Outputs: Figure output/growth_boxplot_2005_2020.png and inline plot.

1.9) Mean growth over the last 10 years (2010→2020) by site

Purpose: Compute per-tree growth (2020 − 2010), average by site.
Inputs: Circumf_2010_cm, Circumf_2020_cm, Site
Outputs: 2-row table (site, mean_growth_last10_cm).

1.10) t-test for 10-year growth difference between sites

Purpose: t.test on per-tree (2020 − 2010) across sites.
Inputs: same as 1.9
Outputs: Test output in report (includes p-value); brief interpretation.

Part 2 — Examining biological sequence diversity
Inputs for all Part 2 scripts come from the two CDS FASTA files saved under data/:
ecoli_cds.fa.gz (E. coli)
oxalo_cds.fa.gz (O. formigenes OXCC13)

2.1) Number of CDS (table + description)

Purpose: Read CDS FASTA with seqinr::read.fasta(), count CDS for each organism, and describe the difference.
Inputs: data/ecoli_cds.fa.gz, data/oxalo_cds.fa.gz
Outputs: 2-row table of organism, n_cds plus a short descriptive paragraph.

2.2) Total coding DNA (table + description)

Purpose: Sum CDS lengths (bp) per organism; describe the difference (absolute, %, ratio).
Inputs: same as 2.1
Outputs: 2-row table of organism, total_coding_bases + descriptive paragraph.
(In the report I also relate this to Task 2.1 counts to comment on avg CDS length.)

2.3) CDS length distribution (table + boxplot + description)

Purpose: Compute mean/median CDS lengths; produce a boxplot; describe differences.
Inputs: same as 2.1
Outputs: summary table; figure output/cds_lengths_boxplot.png; short paragraph.

2.4) DNA base & amino-acid frequencies (tables + barplots + description)

Purpose: 
Concatenate all CDS and compute A/C/G/T frequencies (+ GC%).
Translate to protein and compute amino-acid frequencies.
Describe differences briefly.

Inputs: same as 2.1

Outputs: tables; figures output/base_freq_barplot.png, output/aa_freq_barplot.png; paragraph.

2.5) Codon usage & codon-bias (tables + barplots + description)

Purpose:
Build codon usage tables from concatenated CDS (in-frame).
Quantify codon-usage bias using Shannon entropy (lower bits = stronger bias).
Plot top 20 codons for each organism; describe differences.

Inputs: same as 2.1

Outputs: codon usage tables (printed), bias table (organism, entropy_bits),
figures output/codon_top20_ecoli.png, output/codon_top20_oxalo.png; paragraph.

2.6) Protein k-mer (k=3–5) enrichment (tables + barplots + explanation)

Purpose:
Translate CDS to protein and compute protein k-mer frequencies for k=3,4,5.
Identify top 10 over-represented and top 10 under-represented k-mers in O. formigenes relative to E. coli (either using frequency difference or log2 enrichment, per code).
Plot the comparisons and explain why such motifs may differ (composition, codon bias, protein function, selection).

Inputs: same as 2.1

Outputs: printed k-mer tables; plots saved as
output/kmers_over_k3.png, output/kmers_under_k3.png,
output/kmers_over_k4.png, output/kmers_under_k4.png,
output/kmers_over_k5.png, output/kmers_under_k5.png; brief explanation.
