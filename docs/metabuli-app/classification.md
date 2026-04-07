# Classification
Metabuli App provides two taxonomic profiling modes in **Search Settings** panel: **New Search** and **Upload Report**.

## New Classification
#### You can perform taxonomic classification on one or more samples using a specified database.
### Required Fields:
1. **Mode:** Select the analysis mode among single-end, paired-end, or long-read.
2. **Enable Quality Control:** Check it to enable quality control for the input reads. 
    - `fastp` and `fastplong` are used for short and long reads, respectively.
    - Please see QC documentation for more details.
3. **Job ID:** Enter a unique identifier for the job.
4. **Query Files:** Specify your query sample(s) to classify.
    - FASTA/FASTQ and their gzipped versions are supported.
    - `ADD ENTRY` to upload **multiple samples** to process using the same settings.
5. **Database Folder:** Select the folder of Metabuli database.
6. **Output Folder:** Specify the folder where the results will be saved.
    - Result files are saved in `Job ID` folder under the specified output folder.
    - When **multiple samples** are processed, results are saved in `Job ID/sample_name` directories.
7. **Max RAM:** Specify the maximum RAM (in GiB) to allocate for the job. (all available RAM by default)

### Advanced Settings (Optional): 
- `--precise`: Use presets for precise mode. `1`: short-read, `2`: HiFi long-read.
- `-e`: Ignore matches with larger E-value (1.0 by default, 0 to disable).
- `--priority-taxid`: Favors these and child taxa instead of LCA in case of a tie. (Comma-separated list of tax IDs.)
- `--syncmer`: Set `1` to use syncmers instead of all k-mers.
- `--smer-len`: *s*-mer length used for syncmer selection. Compression factor = (*k*-*s*+1)/2.
- `--min-score`: Reads with scores below this threshold are remained unclassified to avoid overconfident calls.
- `--min-sp-score`: Reads with scores below this threshold are assigned to higher ranks to avoid overconfident calls.
- `--threads`: Specify thread count for the job. (all threads by default)
- `--validate-db`: Check if files in database folder are valid.
- `--validate-input`: Vaidate query FASTA/FASTQ file format.
- `--lineage`: Set `1` to print full lineage.

### Start Analysis: 
- Click the `Run Metabuli` button to start the metagenomic classification process.
- You can track the progress and see real-time backend output in the logs.

### View Results: 
   - Once the analysis is complete, you can view the results in three different forms:
     - **Table**: View the raw classification data in a table format.
     - **Sankey Diagram**: A flow diagram representing the lineage information of the displayed taxa.
     - **Krona Chart**: A hierarchical interactive chart that visualizes classification results.

### Generated Result Files: 
Documented in [Output File Formats](../modules/classify.md/#output-file-formats) section of the classify module.

## Upload Report

To visualize results from a previously completed job:

1. Navigate to the **Upload Report** tab.
2. Upload the `report.tsv` file from a prior job.
3. View the uploaded results directly in the **Results** tab. For this job type, results are provided in:
   - **Table**: The raw data in table format.
   - **Sankey Diagram**: A flow diagram representing the lineage paths for the displayed taxa (without the Krona chart).
   