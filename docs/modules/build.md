# build

The `build` module creates a custom reference database from a set of FASTA files. Metabuli supports two types of taxonomies: **GTDB-based** and **NCBI/custom taxonomy-based**.

---

## GTDB-based Database

### Requirements

Reference FASTA file names (or paths) must include an assembly accession matching the pattern `GC[AF]_[0-9]+\.[0-9]+` (e.g., `GCF_028750015.1`). Files from RefSeq or GenBank meet this requirement.

### Steps

#### 1. Download GTDB taxdump files

Download taxonkit-generated GTDB taxdump files from [https://github.com/shenwei356/gtdb-taxdump/releases](https://github.com/shenwei356/gtdb-taxdump/releases).

#### 2. Build the database

```bash
metabuli build --gtdb 1 <DBDIR> <FASTA_LIST> <GTDB_TAXDUMP/taxid.map> \
    --taxonomy-path <GTDB_TAXDUMP> [options]
```

| Argument | Description |
|----------|-------------|
| `DBDIR` | Directory where the database will be created |
| `FASTA_LIST` | File containing absolute paths to reference genome FASTA files (one per line) |
| `GTDB_TAXDUMP/taxid.map` | Path to the `taxid.map` file inside the GTDB taxdump directory |
| `--taxonomy-path` | Directory containing the GTDB taxdump files |

---

## NCBI / Custom Taxonomy-based Database

### Requirements

1. **FASTA files** — each sequence must have a unique `>accession.version` or `>accession` header (e.g., `>CP001849.1`).
2. **NCBI-style `accession2taxid`** — sequences with accessions absent here are skipped; versions are ignored.
3. **NCBI-style taxonomy dump** — must contain `names.dmp`, `nodes.dmp`, and `merged.dmp`. Sequences with tax IDs absent here are skipped.

### Preparing taxonomy files

- Download `accession2taxid` from [https://ftp.ncbi.nlm.nih.gov/pub/taxonomy/accession2taxid/](https://ftp.ncbi.nlm.nih.gov/pub/taxonomy/accession2taxid/).
- Download `taxdump` files from [https://ftp.ncbi.nlm.nih.gov/pub/taxonomy/new_taxdump/](https://ftp.ncbi.nlm.nih.gov/pub/taxonomy/new_taxdump/).

For custom sequences, edit `accession2taxid` and `taxdump` as follows:

- **`accession2taxid`**: Add `custom[tab]custom[tab]taxid[tab]anynumber` for a sequence with header `>custom`. Version number is not required. The `taxid` must exist in `nodes.dmp` and `names.dmp`.
- **`taxdump`**: Edit `nodes.dmp` and `names.dmp` if you introduce new taxIDs in `accession2taxid`.

### Build the database

```bash
metabuli build <DBDIR> <FASTA_LIST> <accession2taxid> \
    --taxonomy-path <TAXDUMP> [options]
```

| Argument | Description |
|----------|-------------|
| `DBDIR` | Directory where the database will be created |
| `FASTA_LIST` | File containing absolute paths to reference FASTA files (one per line) |
| `accession2taxid` | NCBI-style accession2taxid file |
| `--taxonomy-path` | Directory containing taxonomy dump files |

---

## Options

The following options apply to both GTDB-based and NCBI/custom taxonomy-based builds:

| Option | Default | Description |
|--------|---------|-------------|
| `--gtdb` | `0` | Set `1` to build a GTDB-based database |
| `--threads` | all | Number of threads to use |
| `--max-ram` | `128` (GiB) | Maximum RAM usage in GiB |
| `--accession-level` | `0` | Set `1` to enable accession-level classification |
| `--make-library` | `0` | Enable for faster execution when many species share a single FASTA file |
| `--cds-info` | — | File listing absolute paths to CDS files (GenBank/RefSeq format). Provided CDS files are used instead of running Prodigal. |
| `--validate-input` | `0` | Set `1` to validate FASTA file format |
| `--validate-db` | `0` | Set `1` to validate created database files |

---

## Output Files

The following files are generated in `DBDIR`:

| File | Description |
|------|-------------|
| `diffIdx` | Differential index file |
| `info` | Database metadata |
| `split` | Sequence split information |
| `taxID_list` | Taxonomy ID list |

!!! note
    You can delete `*_diffIdx` and `*_info` files after the build. For NCBI-based builds, the `DATE-TIME` folder (e.g., `2025-1-24-10-32`) can also be removed if present.
