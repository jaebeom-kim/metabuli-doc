# Databases (WIP)
!!! note
    Databases here requires Metabuli v1.2.0 or later. For older versions, please refer to the [Old Database](old-database.md) page.

Pre-built databases are provided for common use cases. All databases can be downloaded from [here](https://opendata.mmseqs.org/metabuli).

---

### Summary

!!! note
    Please refer [Metabuli-Braken](../util/braken.md) page for instructions on how to use Braken with Metabuli's databases.

| Database Name | Taxonomy | Size(GB) | Braken | Contents | Link |
|---------------|----------|------|--------|----------|------|
| `gtdb226`     | GTDB     | 378  | - |GTDB R226 genomes | [Download](https://opendata.mmseqs.org/metabuli/gtdb+human+virus.tar.gz) |
| `refseq_standard` | NCBI | -    | Yes |RefSeq archaea, bacteria, virus, plasmid, protozoa, fungi, and human | WIP |
| `hrgm2`       | GTDB     | 85 | Yes |Human Reference Gut Microbiome v2 ([HRGM2](https://www.decodebiome.org/HRGM/))  | [Download](https://opendata.mmseqs.org/metabuli/hrgm2.tar.gz) |
| `hrom`        | GTDB     | -    | Yes |Human Reference Oral Microbiome ([HROM](https://www.decodebiome.org/HROM/)) | WIP |



### `gtdb226`
- Citation: GTDB R226 ([Parks et al., 2026](https://doi.org/10.1093/nar/gkaf1040))
- Species representative genomes with checkm2 completeness > 90% and contamination < 5%.
- Includes 90,791 species out of 143,614 species in GTDB R226.
- Human genome (T2T-CHM13v2.0) and RefSeq Virus (2026-03-31) are added.
- `build` options: `--space-mask 11101110111 --custom-metamer reduced_15_pattern.txt --syncmer 1 --smer-len 6`
    - As many genomes are included, syncmers are used to reduce database size and improve classification speed. 


### `hrgm2`
- Citation: Human Reference Gut Microbiome v2 ([HRGM2](https://www.decodebiome.org/HRGM/)).
- HRGM2 statistics:
    - Only near-complete genomes (Completeness ≥ 90%, Contamination ≤ 5%, and GUNC CSS < 0.45)
    - 155,211 genomes representing 4,824 species.
- Human genome (T2T-CHM13v2.0) and RefSeq Virus (2026-03-31) are added.
- Braken support:
    - Download Braken database from HRGM2 page [here](https://www.decodebiome.org/HRGM/listdir.php?directory=data/genome_catalog/Taxonomy_Profiling/HRGMv2_kraken2_customdb/HRGMv2_Concat).
    - **NOTE**: The HRGM2 Braken databases only include prokaryotic genomes. Viral and eukaryotic portions of Braken results should be interpreted with caution. 
- `build` options: `--space-mask 11101110111 --custom-metamer reduced_15_pattern.txt`


### `refseq_standard` WIP
- Citation: NCBI RefSeq 
- Metabuli version of [Kraken2's PlusPF database](https://benlangmead.github.io/aws-indexes/k2) (2/26/2026 update)
    - RefSeq archaea, bacteria, virus, plasmid, protozoa, fungi, human, and UniVec_Core sequences are included.
- Braken support: Braken database is bundled with Kraken2's PlusPF database.
- `build` options: `--space-mask 11101110111 --custom-metamer reduced_15_pattern.txt --syncmer 1 --smer-len 6`
    - As many genomes are included, syncmers are used to reduce database size and improve classification speed. 




### `hrom` WIP
- Citation: Human Reference Oral Microbiome ([HROM](https://www.decodebiome.org/HROM/)).
- HROM statistics:
    - High quality genomes (Completeness ≥ 90%, Contamination ≤ 5%, and GUNC CSS < 0.45)
    - 72,641 NC genomes representing 3,426 species.
- Braken support: You can download Braken database from HROM page [here](https://www.decodebiome.org/HROM/listdir.php?directory=data/genome_catalog/HROM_kraken2_customdb).
- `build` options: `--space-mask 11101110111 --custom-metamer reduced_15_pattern.txt`