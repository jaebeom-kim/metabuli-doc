# Pre-built Databases

Metabuli provides several pre-built databases for common use cases. All databases can be downloaded with the [`databases`](modules/databases.md) module or manually from [https://metabuli.steineggerlab.workers.dev/](https://metabuli.steineggerlab.workers.dev/).

!!! note
    A human genome (T2T-CHM13v2.0) is included in all databases below.

---

## Available Databases

### RefSeq Virus

| Property | Value |
|----------|-------|
| **DB_NAME** | `RefSeq_virus` |
| **Size** | 8.1 GiB |
| **Contents** | NCBI RefSeq release 223 virus genomes |

```bash
metabuli databases RefSeq_virus OUTDIR tmp
# Database stored in: OUTDIR/refseq_virus
```

---

### RefSeq Prokaryote and Virus

| Property | Value |
|----------|-------|
| **DB_NAME** | `RefSeq` |
| **Size** | 115.6 GiB |
| **Contents** | RefSeq prokaryote genomes (Complete Genome/Chromosome, 2024-03-26) + RefSeq Virus |

```bash
metabuli databases RefSeq OUTDIR tmp
# Database stored in: OUTDIR/refseq_prokaryote_virus
```

---

### GTDB

| Property | Value |
|----------|-------|
| **DB_NAME** | `GTDB` |
| **Size** | 101 GiB |
| **Contents** | GTDB 214.1 genomes (Complete Genome/Chromosome, CheckM completeness > 90%, contamination < 5%) |

```bash
metabuli databases GTDB OUTDIR tmp
# Database stored in: OUTDIR/gtdb
```

!!! tip
    A newer GTDB R226 database is also available. See [https://mmseqs.com/metabuli](https://mmseqs.com/metabuli) for the latest releases.

---

### RefSeq Release 224

| Property | Value |
|----------|-------|
| **DB_NAME** | `RefSeq_release` |
| **Size** | 619 GiB |
| **Contents** | Viral and prokaryotic genomes of RefSeq release 224 |

```bash
metabuli databases RefSeq_release OUTDIR tmp
# Database stored in: OUTDIR/refseq_release
```

---

## GTDB R226 Database (Latest)

A newer GTDB R226 database is available at [https://hulk.mmseqs.com/jaebeom/gtdb226db/](https://hulk.mmseqs.com/jaebeom/gtdb226db/):

- Species representative genomes with CheckM2 completeness > 70% and contamination < 5%
- 129,671 species out of 143,614 species in GTDB R226 are included

---

## Custom Databases

If the pre-built databases do not fit your needs, you can build a custom database using the [`build`](modules/build.md) module. You can also extend an existing database using [`updateDB`](modules/update-db.md).
