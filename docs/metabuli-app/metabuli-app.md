# Metabuli App

Metabuli App is the desktop application for Metabuli. Built with Vue.js and Electron, it provides an easy interface for running metagenomic classification jobs and visualizing the results.

<video width="100%" controls>
  <source src="../../assets/metabuli-app-demo.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>


!!! NOTE
    The `NCBI` and `Assemblies` buttons in the Sankey subtree view do not work when searching against a GTDB-based database. We will make a button for GTDB soon.

## End-to-end functionalities
- **Download** pre-built **databases**
- **Create or update databases**
- Raw-read **quality control (QC)**
- Run **taxonomic classification**
- **Upload and browse** classification results
- **Extract reads** classified under a specific taxon
- Explore results with interactive **Sankey** and **Krona** plots.

## Platforms Supported
- macOS (`.dmg`)
- Windows (`.exe`)
- Linux (`.AppImage`)

---

## Installation

- Visit the [GitHub Releases](https://github.com/steineggerlab/Metabuli-App/releases) page for the latest builds.
- The application is pre-built for **macOS**, **Windows**, and **Linux**.
- Simply download the executable for your platform from the Releases section.

!!! note
    If you encounter a security warning when opening the app, follow the instructions below to bypass the warning:
    
    - **macOS**: Refer to [this guide](https://support.apple.com/en-gb/guide/mac-help/mh40616/15.0/mac/15.0) on how to open apps from unidentified developers.
    
    - **Windows**: Click 'More info' and then 'Run anyway' to continue.

---

## References
The development of the Metabuli Desktop Application has been inspired by and leverages the following tools:

- **Pavian**: Elements of the table layouts and visualizations in Metabuli were inspired by Pavian for metagenomic data analysis. ([Pavian GitHub Repository](https://github.com/fbreitwieser/pavian)).
  
- **Krona**: The Krona tool is embedded in the results page for hierarchical data visualization. ([Krona GitHub Repository](https://github.com/marbl/Krona/wiki)).

- **fastp**: Ultrafast one-pass FASTQ data preprocessing, quality control, and deduplication software. ([fastp GitHub Repository](https://github.com/OpenGene/fastp))

- **fastplong**: `fastp` for long reads. ([fastplong GitHub Repository](https://github.com/OpenGene/fastplong))


We would like to acknowledge the authors of these tools for their excellent work, which has significantly contributed to the development of Metabuli App.


