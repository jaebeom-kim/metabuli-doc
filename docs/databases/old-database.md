# Old Databases

Databases here are built for Metabuli v1.0.0 to v1.1.1. Download them from [here](https://opendata.mmseqs.org/metabuli/archive).
Spaced k-mers and reduced amino acid alphabet are not used in these databases.

---

## Available Databases

### `refseq_virus`
- NCBI RefSeq release 223 virus genomes + human genome (T2T-CHM13v2.0)
- Size: 8.1 GB
- [Download link](https://steineggerlab.s3.amazonaws.com/metabuli/archive/refseq_virus.tar.gz)
---

### `refseq_prokaryote_virus`
- RefSeq prokaryote genomes (Complete Genome/Chromosome, 2024-03-26) + RefSeq Virus + human genome (T2T-CHM13v2.0)
- Size: 115.6 GB
- [Download link](https://steineggerlab.s3.amazonaws.com/metabuli/archive/refseq_prokaryote_virus.tar.gz)

---

### `refseq_release`
- Viral and prokaryotic genomes of RefSeq release 224 + human genome (T2T-CHM13v2.0)
- Size: 619 GB
- [Download link](https://steineggerlab.s3.amazonaws.com/metabuli/archive/refseq_release.tar.gz)

---

### `gtdb+virus+human`
- HQ GTDB R220 genomes (Complete Genome/Chromosome, CheckM completeness > 90%, contamination < 5%)
- RefSeq Virus (2025-03-07) + human genome (T2T-CHM13v2.0)
- Prokaryotes follow GTDB taxonomy, viruses and human follow NCBI taxonomy
- Size: 117 GB
- [Download link](https://steineggerlab.s3.amazonaws.com/metabuli/archive/gtdb+virus+human.tar.gz)

---

### `gtdb`
- HQ GTDB R214.1 genomes (Complete Genome/Chromosome, CheckM completeness > 90%, contamination < 5%) + human genome (T2T-CHM13v2.0)
- Size: 101 GB
- [Download link](https://steineggerlab.s3.amazonaws.com/metabuli/archive/gtdb.tar.gz)

---

### `gtdb226db`
- GTDB R226 species representative genomes with CheckM2 completeness > 70% and contamination < 5%
- Size: 453 GB
- `build` options: `--syncmer 1 --smer-len 5`
- [Download link](https://steineggerlab.s3.amazonaws.com/metabuli/archive/gtdb226db.tar.gz)
