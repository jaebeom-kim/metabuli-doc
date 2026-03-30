# Example

This example demonstrates how to classify RNA-seq reads from a COVID-19 patient using the RefSeq Virus database. The whole process takes less than 10 minutes on a personal machine.

---

## Step 1 — Download the RefSeq Virus Database (8.1 GiB)

Link: [https://steineggerlab.s3.amazonaws.com/metabuli/refseq_virus.tar.gz](https://steineggerlab.s3.amazonaws.com/metabuli/refseq_virus.tar.gz)

---

## Step 2 — Download RNA-seq reads (SRR14484345)

```bash
fasterq-dump --split-files SRR14484345
```

!!! tip
    Download SRA Toolkit containing `fasterq-dump` from [https://github.com/ncbi/sra-tools/wiki/02.-Installing-SRA-Toolkit](https://github.com/ncbi/sra-tools/wiki/02.-Installing-SRA-Toolkit).

---

## Step 3 — Classify reads

```bash
metabuli classify \
    SRR14484345_1.fq SRR14484345_2.fq \
    OUTDIR/refseq_virus \
    RESULT_DIR JOB_ID \
    --max-ram RAM_SIZE
```

Replace `RAM_SIZE` with the amount of RAM (in GiB) available on your machine.

---

## Step 4 — Inspect the report

Open `RESULT_DIR/JOB_ID_report.tsv` and look for a section like the following:

```
92.2331  510490  442     species  694009   Severe acute respiratory syndrome-related coronavirus
92.1433  509993  509993  no rank  2697049  Severe acute respiratory syndrome coronavirus 2
```

This shows that ~92% of reads were classified to SARS-CoV-2.

---

## Next Steps

- Use [`refine-results`](modules/refine-results.md) to filter or adjust the classification results.
- Use [`extract`](modules/extract.md) to pull out reads classified to a specific taxon.
- Browse the interactive taxonomy chart in `RESULT_DIR/JOB_ID_krona.html`.
