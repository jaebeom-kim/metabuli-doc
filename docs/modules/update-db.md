# updateDB

The `updateDB` module adds new sequences to an existing Metabuli database. It supports both GTDB-based and NCBI/custom taxonomy-based databases, and allows adding sequences for existing taxa as well as new taxa.

!!! note
    If you want to upgrade to a new GTDB release, build a new database from scratch using the [`build`](build.md) module instead.

---

## GTDB-based Database

### Add GTDB genomes

```bash
metabuli updateDB --gtdb 1 <NEW_DBDIR> <FASTA_LIST> <GTDB_TAXDUMP/taxid.map> <OLD_DBDIR> [options]
```

| Argument | Description |
|----------|-------------|
| `NEW_DBDIR` | Directory where the updated database will be generated |
| `FASTA_LIST` | File listing absolute paths to new FASTA files |
| `GTDB_TAXDUMP/taxid.map` | Path to the `taxid.map` file from the GTDB taxdump |
| `OLD_DBDIR` | Directory of the existing database to update |

### Add sequences of new taxa to a GTDB database

!!! warning
    Mixing taxonomies within the same domain is not recommended. For example, adding prokaryotes using NCBI taxonomy to a GTDB database will cause issues. However, adding eukaryotes or viruses using NCBI taxonomy is fine since GTDB does not cover them.

#### Option A — Using `createnewtaxalist`

If you have `accession2taxid` and taxonomy dump files for the new sequences, use `createnewtaxalist` to prepare the input automatically:

```bash
metabuli createnewtaxalist <OLD_DBDIR> <FASTA_LIST> <new_taxdump_dir> <accession2taxid> <OUTDIR>
```

This generates:

- `OUTDIR/newtaxa.tsv` — input for `--new-taxa`
- `OUTDIR/newtaxa.accession2taxid`

Then update the database:

```bash
metabuli updateDB --gtdb 1 <NEW_DBDIR> <FASTA_LIST> <OUTDIR/newtaxa.accession2taxid> <OLD_DBDIR> \
    --new-taxa <OUTDIR/newtaxa.tsv>
```

#### Option B — Manually prepare a new taxa list

Provide a four-column TSV file for `--new-taxa` in the following format (no header):

```
taxID   parentID    rank    name
```

Each new taxon must be linked to a taxon already present in the existing database's taxonomy.

**Example** — adding *Saccharomyces cerevisiae* to a GTDB database where Fungi is absent:

```tsv
10000013    10000012    species     Saccharomyces cerevisiae
10000012    10000011    genus       Saccharomyces
10000011    10000010    family      Saccharomycetaceae
10000010    10000009    order       Saccharomycetales
10000009    10000008    class       Saccharomycetes
10000008    10000007    phylum      Ascomycota
10000007    10000000    kingdom     Fungi
```

Corresponding `accession2taxid`:

```tsv
accession   accession.version   taxid   gi
newseq1     newseq1             10000013    0
newseq2     newseq2             10000013    0
```

---

## NCBI / Custom Taxonomy-based Database

### Add sequences of existing taxa

#### 1. Prepare two files

- **New FASTA file list** — each sequence must have a unique `>accession.version` or `>accession` header.
- **NCBI-style `accession2taxid`** — sequences with accessions absent here are skipped; version numbers are ignored:

```tsv
accession       accession.version   taxID   gi
SequenceA       SequenceA.1         960611  0
SequenceB       SequenceB.1         960612  0
NoVersionOkay   NoVersionOkay       960613  0
```

#### 2. Update the database

```bash
metabuli updateDB <NEW_DBDIR> <FASTA_LIST> <accession2taxid> <OLD_DBDIR> [options]
```

| Argument | Description |
|----------|-------------|
| `NEW_DBDIR` | Directory where the updated database will be generated |
| `FASTA_LIST` | File listing paths to new FASTA files |
| `accession2taxid` | NCBI-style accession2taxid file |
| `OLD_DBDIR` | Directory of the existing database to update |

### Add sequences of new taxa

Use the same `--new-taxa` approach described in the GTDB section above.

---

## Options

| Option | Default | Description |
|--------|---------|-------------|
| `--gtdb` | `0` | Set `1` for a GTDB-based update |
| `--threads` | all | Number of threads to use |
| `--max-ram` | `128` (GiB) | Maximum RAM usage in GiB |
| `--accession-level` | `0` | Set `1` to include accession-level classification |
| `--make-library` | `0` (GTDB) / `1` (NCBI) | Enable for faster execution when many species share a single FASTA file |
| `--new-taxa` | — | TSV file listing new taxa to add |
| `--cds-info` | — | File listing absolute paths to CDS files |
| `--validate-input` | `0` | Set `1` to validate FASTA file format |
| `--validate-db` | `0` | Set `1` to validate database files |
