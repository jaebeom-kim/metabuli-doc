# Metabuli

**Metabuli** classifies metagenomic reads by comparing them to reference genomes. You can use Metabuli to profile the taxonomic composition of your samples or to detect specific (pathogenic) species.

---

## Key Features

**Sensitive and Specific.**
Metabuli uses a novel k-mer structure, called *metamer*, to analyze both amino acid (AA) and DNA sequences. It leverages AA conservation for sensitive homology detection and DNA mutations for specific differentiation between closely related taxa.

**A laptop is enough.**
Metabuli operates within user-specified RAM limits, allowing it to search any database that fits in storage. A PC with 8 GiB of RAM is sufficient for most analyses.

**A few clicks are enough.**
[Metabuli App](https://github.com/steineggerlab/Metabuli-App) is available for Windows, macOS, and Linux. With just a few clicks, you can run Metabuli and browse the results with Sankey and Krona plots on your PC.

**Short reads, long reads, and contigs.**
Metabuli can classify all types of sequences.

---

## Quick Start

```bash
# 1. Install via conda
conda install -c conda-forge -c bioconda metabuli

# 2. Download a pre-built database
metabuli databases RefSeq_virus OUTDIR tmp

# 3. Classify reads (paired-end)
metabuli classify read_1.fq read_2.fq OUTDIR/refseq_virus RESULT_DIR JOB_ID
```

---

## Citation

Kim J, Steinegger M. **Metabuli: sensitive and specific metagenomic classification via joint analysis of amino acid and DNA.** *Nature Methods* (2024). [https://doi.org/10.1038/s41592-024-02273-y](https://doi.org/10.1038/s41592-024-02273-y)

---

## Modules

| Module | Description |
|--------|-------------|
| [`classify`](modules/classify.md) | Classify metagenomic reads against a reference database |
| [`classifiedRefiner`](modules/classified-refiner.md) | Refine classification results with additional filtering options |
| [`extract`](modules/extract.md) | Extract reads classified under a specific taxon |
| [`build`](modules/build.md) | Build a custom reference database |
| [`updateDB`](modules/update-db.md) | Add new sequences to an existing database |
| [`databases`](modules/databases.md) | Download pre-built databases |
