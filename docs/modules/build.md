# `build`

It creates a custom reference database from a set of FASTA files. 

---

## GTDB-based Database

!!! note
    Reference FASTA file names (or paths) must include an assembly accession matching the pattern `GC[AF]_[0-9]+\.[0-9]+` (e.g., `GCF_028750015.1`). Files from RefSeq or GenBank meet this requirement.

### 1. Prepare taxonomy files

GTDB taxdump files are available at [https://github.com/shenwei356/gtdb-taxdump/releases](https://github.com/shenwei356/gtdb-taxdump/releases).
> Please cite [TaxonKit](https://doi.org/10.1016/j.jgg.2021.03.006) for the GTDB taxdump files.

### 2. Build the database

```bash
# GTDB_TAXDUMP : Directory of the downloaded taxdump files.
# FASTA_LIST   : File of reference genome absolute paths.
# DBDIR        : Directory to store the database.

metabuli build --gtdb 1 <DBDIR> <FASTA_LIST> <GTDB_TAXDUMP/taxid.map> \
    --taxonomy-path <GTDB_TAXDUMP> [options]
```
#### Important Options
| Option | Default | Description |
|--------|---------|-------------|
| `--space-mask` | - | Pattern for spaced k-mer extraction (e.g., 1110111011). Contiguous k-mer by default |
| `--custom-metamer` | - | Custom metamer JSON file. See [Custom Metamer Example](#custom-metamer-example) |
| `--syncmer` | 0 | Set `1` to use syncmers |
| `--smer-len` | 5 | *s*-mer length used for syncmer selection. Compression factor = (*k*-*s*+1)/2 |

#### Other Options
| Option | Default | Description |
|--------|---------|-------------|
| `--threads` | all | The number of threads to use |
| `--max-ram` | 128 | The maximum RAM usage |
| `--cds-info` | - | List of absolute paths to CDS files |
| `--validate-input` | `0` | Set `1` to validate query file format |
| `--validate-db` | `0` | Set `1` to validate database files |


---

## NCBI / Custom Taxonomy-based Database

### 0. Requirements

1. **FASTA files** — each sequence must have a unique `>accession.version` or `>accession` header (e.g., `>CP001849.1`).
2. **NCBI-style `accession2taxid`** — sequences with accessions absent here are skipped; versions are ignored.
3. **NCBI-style taxonomy dump** — must contain `names.dmp`, `nodes.dmp`, and `merged.dmp`. Sequences with tax IDs absent here are skipped.

### 1. Prepare taxonomy files

- Download `accession2taxid` from [here](https://ftp.ncbi.nlm.nih.gov/pub/taxonomy/accession2taxid/).
- Download `taxdump` files from [here](https://ftp.ncbi.nlm.nih.gov/pub/taxonomy/new_taxdump/).

For custom sequences, edit `accession2taxid` and `taxdump` as follows:

- **`accession2taxid`**: Add `custom[tab]custom[tab]taxid[tab]anynumber` for a sequence with header `>custom`. Version number is not required. The `taxid` must exist in `nodes.dmp` and `names.dmp`.
- **`taxdump`**: Edit `nodes.dmp` and `names.dmp` if you introduce new taxIDs in `accession2taxid`.

### 2. Build the database

```bash
### DBDIR           : Directory to store the database.
### FASTA_LIST      : File of reference genome absolute paths.
### TAXDUMP         : Directory of taxonomy dump files.
### accession2taxid : NCBI-style accession2taxid file.

metabuli build <DBDIR> <FASTA_LIST> <accession2taxid> --taxonomy-path <TAXDUMP> [options]
```
The same options described above are supproted here as well.

---

## Database Files

The following files are generated in `DBDIR`:

| File | Description |
|------|-------------|
| `diffIdx` | k-mer values |
| `info` | k-mer tax IDs |
| `split` | DB offsets for parallel search |
| `taxID_list` | Taxonomy ID list |
| `taxonomyDB` | Taxonomy tree |
| `db.parameters` | Database parameters parsed during classification |


!!! note
    You can delete `*_diffIdx` and `*_info` files after the build. `DATE-TIME` folder (e.g., `2025-1-24-10-32`) can also be removed if present.

---

## Custom metamer example
You can set *k*-mer length and a translation table. Lines starting with `===` are required for parsing.
"length" defines the *k*-mer length. Put *k* zeros in "position_codes". "codons" defines the translation table. Pattern for spaced *k*-mer is not set in this file, but by setting `--space-mask`.

!!! note
    This JSON format is designed to support setting different genetic codes for different positions in the future. For now, only one code set is supported. Thus, "code_count" must be `1` and "position_codes" must be all zeros.


```json 
##Reduction of protein sequence complexity by residue grouping
===BEGIN_CUSTOM_METAMER===
{
  "name": "Reduced Alphabet (15+stop)",
  "length": 9,
  "code_count": 1,
  "position_codes": [0, 0, 0, 0, 0, 0, 0, 0, 0],
  "codes": [
    {
      "id": "Reduced Alphabet (15+stop)",
      "codons": [
        ["A", ["GCT", "GCC", "GCA", "GCG"]],
        ["R", ["CGT", "CGC", "CGA", "CGG", "AGA", "AGG"]],
        ["N", ["AAT", "AAC"]],
        ["D", ["GAT", "GAC"]],
        ["C", ["TGT", "TGC"]],
        ["QE", ["CAA", "CAG", "GAA", "GAG"]],
        ["G", ["GGT", "GGC", "GGA", "GGG"]],
        ["H", ["CAT", "CAC"]],
        ["IV", ["ATT", "ATC", "ATA", "GTT", "GTC", "GTA", "GTG"]],
        ["ML", ["ATG", "TTA", "TTG", "CTT", "CTC", "CTA", "CTG"]],
        ["K", ["AAA", "AAG"]],
        ["FYW", ["TTT", "TTC", "TAT", "TAC", "TGG"]],
        ["P", ["CCT", "CCC", "CCA", "CCG"]],
        ["S", ["TCT", "TCC", "TCA", "TCG", "AGT", "AGC"]],
        ["T", ["ACT", "ACC", "ACA", "ACG"]],
        ["X", ["TAA", "TAG", "TGA"]]
      ]
    }
  ]
}
===END_CUSTOM_METAMER===
```