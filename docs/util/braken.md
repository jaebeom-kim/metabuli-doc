# Metabuli-Braken (WIP)

Braken is originally developed for Kraken software to estimate species abundance from Kraken classification results. 
Here, we provide Metabuli-compatible Braken databases for some of our pre-built databases.
Please use this [Braken GitHub fork](https://github.com/jaebeom-kim/Bracken-Metabuli) to process Metabuli's reports with Braken.

## Available Braken Databases

| Metabuli DB Name | Link |
|---------------|------|
| `gtdb226`     | WIP |


## Rationale
We acknowledge that because Metabuli utilizes both DNA and amino acid information, its penalty landscape for near-matches differs from Kraken2. Consequently, the Kraken2 Bracken matrix is an approximation. However, this approximation is highly accurate because the probability matrix generated during the Bracken-build phase relies on error-free simulated reads. When Metabuli processes these perfect subsets of the reference database, the exact DNA identity maximizes the match score. In this scenario, Metabuli behaves essentially as an exact DNA matcher, closely mirroring Kraken2's core logic.

Ultimately, the distribution of ambiguous reads during self-classification is driven by the underlying biological homology between genomes rather than algorithmic differences. When a simulated read falls on a highly conserved region shared identically by two or more species, both Kraken2 and Metabuli will recognize the exact match and symmetrically push the assignment up to the Lowest Common Ancestor (LCA). Because this physical sequence overlap dictates the confusion matrix, using a Kraken2-generated Bracken matrix serves as a robust, computationally practical, and mathematically sound proxy for redistributing Metabuli's taxonomic assignments.

## Citation
- Lu, Jennifer, et al. "Bracken: estimating species abundance in metagenomics data." PeerJ Computer Science 3 (2017): e104.


