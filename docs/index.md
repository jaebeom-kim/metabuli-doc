# Metabuli - Sensitive and Specific Taxonomic Classification

***Sensitive and Specific.***
Metabuli integrates DNA- and amino acid-level searches. It leverages AA conservation for sensitive homology detection and DNA mutations for specific differentiation between closely related taxa.

***A laptop is enough.***
Metabuli operates within user-specified RAM limits, allowing it to search any database that fits in storage. A PC with 8 GiB of RAM is sufficient for most analyses.

***A few clicks are enough.***
[Metabuli App](https://github.com/steineggerlab/Metabuli-App) is available for Windows, macOS, and Linux. With just a few clicks, you can run Metabuli and browse the results with Sankey and Krona plots on your PC.

***Short reads, long reads, and contigs.***
Metabuli can classify all types of sequences.

---
## 🖥️ [Metabuli App](https://github.com/steineggerlab/Metabuli-App) for Windows, macOS, and Linux
- Run **taxonomic classification** and explore results with **interactive Sankey and Krona** plots.
- Download the app for your OS. No separate Metabuli installation needed.

<video width="100%" controls>
  <source src="assets/metabuli-app-demo.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Installation
Three easy options:

1. Install via **conda**: `conda install -c conda-forge -c bioconda metabuli`
2. Download **ready-to-use binaries** at [https://mmseqs.com/metabuli](https://mmseqs.com/metabuli).
    - Linux, macOS, and Windows builds available.
3. **Compile** from source
    ```
    git clone --recurse-submodules https://github.com/steineggerlab/Metabuli.git
    cd Metabuli
    mkdir build && cd build
    cmake -DCMAKE_BUILD_TYPE=Release ..
    make -j
    ```

---

## Modules

| Module | Description |
|--------|-------------|
| [`classify`](modules/classify.md) | Classify metagenomic reads against a reference database |
| [`refine-results`](modules/refine-results.md) | Refine classification results with additional filtering options |
| [`extract`](modules/extract.md) | Extract reads classified under a specific taxon |
| [`build`](modules/build.md) | Build a custom reference database |
| [`updateDB`](modules/update-db.md) | Add new sequences to an existing database |
| [`databases`](modules/databases.md) | Download pre-built databases |

---

## Publications and Citations

- Jaebeom Kim and Martin Steinegger. *Metabuli: sensitive and specific metagenomic classification via joint analysis of amino acid and DNA.* Nature Methods (2024). [Journal](https://doi.org/10.1038/s41592-024-02273-y), [PDF](https://www.nature.com/articles/s41592-024-02273-y.epdf?sharing_token=je_2D5Su0-xVOSjuKSAXF9RgN0jAjWel9jnR3ZoTv0M7gE7NDF_xi_3sW8QdRiwfSJNwqaXItSoeCvr7cvcoQxKLt0oROgWc6urmki9tP80cXEuHPN0D7b4y9y3i8Yv7sZw8MxxhAj7W6p9eZE2zaK3eozdOkXvwADVfso9cXIM%3D), [ISMB 2023 talk](https://www.youtube.com/watch?v=vz2fuRcVwyk)
- SunJae Lee and Jaebeom Kim et al. *Easy and interactive taxonomic profiling with Metabuli App*. Bioinformatics (2025). [Journal](https://doi.org/10.1093/bioinformatics/btaf557)
- Jaebeom Kim and Martin Steinegger. *Sensitive and scalable metagenomic classification using spaced metamers, reduced alphabets, and syncmers*. bioRxiv (2026). [Preprint](https://doi.org/10.64898/2026.03.13.711249 )

