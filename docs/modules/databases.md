# databases

The `databases` module downloads pre-built Metabuli databases directly from the official server.

!!! warning
    The `databases` workflow requires the latest version of Metabuli. If you are using an older version, download databases manually from [https://metabuli.steineggerlab.workers.dev/](https://metabuli.steineggerlab.workers.dev/).

---

## Usage

```
metabuli databases <DB_NAME> <OUTDIR> <tmp>
```

| Argument | Description |
|----------|-------------|
| `DB_NAME` | Name of the database to download (see table below) |
| `OUTDIR` | Directory where the database will be saved |
| `tmp` | Temporary directory for intermediate files |

Downloaded files are stored in `OUTDIR/DB_NAME` and can be passed as `DBDIR` to the [`classify`](classify.md) module.

---

## Available Databases

| DB_NAME | Size | Contents | Command |
|---------|------|----------|---------|
| `RefSeq_virus` | 8.1 GiB | NCBI RefSeq release 223 virus genomes + human genome (T2T-CHM13v2.0) | `metabuli databases RefSeq_virus OUTDIR tmp` |
| `RefSeq` | 115.6 GiB | RefSeq prokaryote genomes (Complete Genome/Chromosome, 2024-03-26) + RefSeq Virus + human genome | `metabuli databases RefSeq OUTDIR tmp` |
| `GTDB` | 101 GiB | GTDB 214.1 (Complete Genome/Chromosome, CheckM completeness > 90%, contamination < 5%) + human genome | `metabuli databases GTDB OUTDIR tmp` |
| `RefSeq_release` | 619 GiB | Viral and prokaryotic genomes of RefSeq release 224 | `metabuli databases RefSeq_release OUTDIR tmp` |

!!! note
    A human genome (T2T-CHM13v2.0) is included in all databases listed above.

For more details on the available databases, see the [Pre-built Databases](../databases.md) page.
