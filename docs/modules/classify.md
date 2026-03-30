# classify

The `classify` module classifies metagenomic reads by comparing them to a reference database.

!!! tip
    We recommend running adapter trimming and quality filtering (e.g., [`fastp`](https://github.com/OpenGene/fastp) for short reads, [`fastplong`](https://github.com/OpenGene/fastplong) for long reads) before classification.

---

## Usage

```
metabuli classify <i:FASTA/Q> <i:DBDIR> <o:OUTDIR> <Job ID> [options]
```

| Argument | Description |
|----------|-------------|
| `FASTA/Q` | Input FASTA/Q file(s) of reads to classify (gzip supported). Provide two files for paired-end reads. |
| `DBDIR` | Directory of the reference database. |
| `OUTDIR` | Directory where result files will be written. |
| `Job ID` | Prefix used for all output file names. |

---

## Examples

=== "Paired-end"

    ```bash
    metabuli classify read_1.fna read_2.fna DBDIR OUTDIR JOB_ID
    ```

=== "Single-end"

    ```bash
    metabuli classify --seq-mode 1 read.fna DBDIR OUTDIR JOB_ID
    ```

=== "Long-read"

    ```bash
    metabuli classify --seq-mode 3 read.fna DBDIR OUTDIR JOB_ID
    ```

---

## Options

| Option | Default | Description |
|--------|---------|-------------|
| `--seq-mode` | `2` | Sequencing mode: `1` = single-end, `2` = paired-end, `3` = long-read |
| `--threads` | all | Number of threads to use |
| `--max-ram` | `128` (GiB) | Maximum RAM usage in GiB |
| `--min-score` | — | Minimum score to classify a read |
| `--min-sp-score` | — | Minimum score to classify at or below species rank |
| `--taxonomy-path` | `DBDIR/taxonomy` | Directory containing taxonomy dump files |
| `--accession-level` | `0` | Set `1` to use accession-level classification (requires DB built with this option) |
| `--validate-input` | `0` | Set `1` to validate query file format |
| `--validate-db` | `0` | Set `1` to validate database files |
| `--lineage` | `0` | Set `1` to print full lineage next to the rank column in the classifications file |

### Precision Mode (Metabuli-P)

Use the following `--min-score` and `--min-sp-score` settings to increase precision:

| Read Type | `--min-score` | `--min-sp-score` |
|-----------|--------------|-----------------|
| Illumina short reads | `0.15` | `0.5` |
| PacBio HiFi reads | `0.07` | `0.3` |
| PacBio Sequel I reads | `0.005` | — |
| ONT reads | `0.008` | — |

---

## Output Files

Running `classify` produces three output files in `OUTDIR`:

| File | Description |
|------|-------------|
| `JOB_ID_classifications.tsv` | Per-read classification results |
| `JOB_ID_report.tsv` | Summary report in Kraken2 format |
| `JOB_ID_krona.html` | Interactive Krona taxonomy chart |

See [Output Formats](../output-formats.md) for a full description of each file.

---

## Resource Requirements

Metabuli operates within user-specified RAM limits (`--max-ram`), so it can search any database that fits on disk regardless of RAM size. A machine with 8 GiB of RAM is sufficient for most analyses.
