# Update Log

### v1.2.0
#### Major updates
- New k-mer format introduced.
    - Older databases are still compatible, but not recommended.
    - Older Metabuli versions are not compatible with the new database format.
- New options in `build` module
    - `--syncmer`: Use syncmers instead of all k-mers.
        - It reduces the database size and classification speed.
        - Reduction rate `(k - s + 1) / 2` can be specified using `--smer-len` to set `s`.
        - As k-mers are subsampled, sensitivity in remote homology detection is decreased. 
    - `--space-mask`: Use spaced k-mers instead of contiguous ones.
    - `--custom-metamer`: Specify k-mer length and customize a translation table.


### v1.1.1
- `--validate-input` option added for FASTA/Q validation.
- `--validate-db` option added for database validation.
- `classifiedRefiner` module added to refine classification results.

### v1.1.0
- Fix errors in v1.0.9
- Custom DB creation became easier
- Improve updateDB command

### v1.0.9
- DB creation process improved
- `updateDB` module to add new sequences to an existing database.
- Users can provide CDS information to skip Prodigal's gene prediction.
- `--max-ram` parameter added to build module.
- Compatibility with taxdump files generated using taxonkit.

### v1.0.8
- Added `extract` module to extract reads classified into a certain taxon.

### v1.0.7
- Metabuli became faster 🚀
    - Windows: 8.3 times faster
    - MacOS: 1.7 times faster
    - Linux: 1.3 times faster
    - Test details are in GitHub release note.
- Fixed a bug in score calculation that could affect classification results.
