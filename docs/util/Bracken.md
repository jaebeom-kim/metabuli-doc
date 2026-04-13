# Metabuli-Bracken

Bracken is originally developed for Kraken software to estimate species abundance from Kraken classification results. 
Here, Metabuli-compatible Bracken is provided: [Bracken GitHub fork](https://github.com/jaebeom-kim/Bracken-Metabuli).
Please use this  to process Metabuli's reports with Bracken.

## Usage
Bracken installation, Kraken2 database building, and Bracken database building are the same as the original Bracken.
Input Metabuli's report file instead of Kraken's report file. The rest of the steps are the same as the original Bracken.

## Available Bracken Databases
Kraken2, HRGM2, and HROM teams provide Bracken databases for their Kraken2-compatible databases.
Here, we created Metabuli databases with the same sequences and taxonomic lineages as Kraken2's databases, so you can use Kraken2's Bracken databases for Metabuli's databases.

| Metabuli database| Kraken2 counterpart |
|------------------|---------------------|
| [`refseq_standard`](../databases/new-database.md/#refseq_standard) | [Kraken2's PlusPF database](https://benlangmead.github.io/aws-indexes/k2) |
| [`hrgm2`](../databases/new-database.md/#hrgm2)          | [HRGM2 custom DB](https://www.decodebiome.org/HRGM/listdir.php?directory=data/genome_catalog/Taxonomy_Profiling/HRGMv2_kraken2_customdb/HRGMv2_Concat) |
| [`hrom`](../databases/new-database.md/#hrom)            | [HROM custom DB](https://www.decodebiome.org/HROM/listdir.php?directory=data/genome_catalog/HROM_kraken2_customdb) |


## Rationale
We acknowledge that because Metabuli utilizes both DNA and amino acid information, its penalty landscape for near-matches differs from Kraken2. Consequently, the Kraken2 Bracken matrix is an approximation. However, this approximation is highly accurate because the probability matrix generated during the Bracken-build phase relies on error-free simulated reads. When Metabuli processes these perfect subsets of the reference database, the exact DNA identity maximizes the match score. In this scenario, Metabuli behaves essentially as an exact DNA matcher, closely mirroring Kraken2's core logic.

Ultimately, the distribution of ambiguous reads during self-classification is driven by the underlying biological homology between genomes rather than algorithmic differences. When a simulated read falls on a highly conserved region shared identically by two or more species, both Kraken2 and Metabuli will recognize the exact match and symmetrically push the assignment up to the Lowest Common Ancestor (LCA). Because this physical sequence overlap dictates the confusion matrix, using a Kraken2-generated Bracken matrix serves as a robust, computationally practical, and mathematically sound proxy for redistributing Metabuli's taxonomic assignments.

## Citation
- Lu, Jennifer, et al. "Bracken: estimating species abundance in metagenomics data." PeerJ Computer Science 3 (2017): e104.


