# Modules Overview

Metabuli provides the following command-line modules:

| Module | Description |
|--------|-------------|
| [`classify`](classify.md) | Classify metagenomic reads against a reference database |
| [`refine-results`](refine-results.md) | Refine classification results with additional filtering options |
| [`extract`](extract.md) | Extract reads classified under a specific taxon |
| [`build`](build.md) | Build a custom reference database |
| [`updateDB`](update-db.md) | Add new sequences to an existing database |

---

## General Usage

```
metabuli <module> [options]
```

Run `metabuli` without arguments or `metabuli --help` to see a list of all available modules.
