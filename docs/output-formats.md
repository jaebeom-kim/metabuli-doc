# Output Formats

The [`classify`](modules/classify.md) module generates three output files with the prefix `JOB_ID`:

---

## JOB_ID_classifications.tsv

Per-read classification results. Use `--lineage 1` in the `classify` command to append the full taxonomic lineage after the `rank` column.

### Columns

| Column | Name | Description |
|--------|------|-------------|
| 1 | `is_classified` | `1` if classified, `0` if not |
| 2 | `name` | Read ID |
| 3 | `taxID` | Taxonomy ID in the taxonomy dump files used for database creation |
| 4 | `query_length` | Effective read length |
| 5 | `score` | DNA-level identity score |
| 6 | `rank` | Taxonomic rank of the assigned taxon |
| 7 | `taxID:match_count` | List of `taxID:k-mer_match_count` pairs |

### Example

```
#is_classified  name    taxID   query_length    score   rank            taxID:match_count
1               read_1  2688    294             0.627551 subspecies     2688:65
1               read_2  2688    294             0.816327 subspecies     2688:78
0               read_3  0       294             0        no rank
```

---

## JOB_ID_report.tsv

A summary report following **Kraken2's report format**. The first line is a header; the remaining lines are tab-separated values.

### Columns

| Column | Name | Description |
|--------|------|-------------|
| 1 | `clade_proportion` | Percentage of reads classified to the clade rooted at this taxon |
| 2 | `clade_count` | Number of reads classified to the clade rooted at this taxon |
| 3 | `taxon_count` | Number of reads classified directly to this taxon |
| 4 | `rank` | Taxonomic rank |
| 5 | `taxID` | Taxonomy ID |
| 6 | `name` | Taxonomic name |

### Example

```
#clade_proportion  clade_count  taxon_count  rank          taxID   name
33.73              77571        77571         no rank       0       unclassified
66.27              152429       132           no rank       1       root
64.05              147319       2021          superkingdom  8034    d__Bacteria
22.22              51102        3             phylum        22784   p__Firmicutes
22.07              50752        361           class         22785   c__Bacilli
17.12              39382        57            order         123658  o__Bacillales
15.81              36359        3             family        126766  f__Bacillaceae
15.79              36312        26613         genus         126767  g__Bacillus
2.47               5677         4115          species       170517  s__Bacillus amyloliquefaciens
0.38               883          883           subspecies    170531  RS_GCF_001705195.1
0.16               360          360           subspecies    170523  RS_GCF_003868675.1
```

---

## JOB_ID_krona.html

An interactive Krona taxonomy chart. Open it in any modern web browser to explore the taxonomic composition of your sample.

!!! tip
    A Sankey diagram is also available in the [Metabuli App](https://github.com/steineggerlab/Metabuli-App) (GUI).

---

## Refined Output Files

When using [`classifiedRefiner`](modules/classified-refiner.md), additional output files are generated:

| File | Description |
|------|-------------|
| `JOB_ID_refined.tsv` | Refined per-read classification file (same format as `_classifications.tsv`) |
| `JOB_ID_refined_report.tsv` | Summary report of refined results (with `--report`) |
| `JOB_ID_refined_krona.html` | Krona chart of refined results (with `--report`) |
| `JOB_ID_refined_higherRanks.tsv` | Classifications at ranks above `--rank` (with `--rank-file-type 2`) |
