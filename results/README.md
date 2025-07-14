# 📊 Results

This folder contains the key output files generated during the *Salmonella Typhi* AMR profiling pipeline. These results represent major stages of the bioinformatics workflow, from quality control to genome annotation and AMR gene prediction.

## Files Included

| File Name           | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| `fastqc.html`       | Quality control report of raw reads generated using **FastQC**              |
| `quast_report.html` | Assembly quality metrics generated using **QUAST**                          |
| `salmonella.faa`    | Predicted protein sequences output by **Prokka** annotation                 |
| `amr_output.tsv`    | Antimicrobial resistance gene predictions generated using **AMRFinderPlus** |

## Notes

- All files were generated as part of a reproducible workflow (see root `README.md` for details).
- Reports are in human-readable HTML or TSV format for inspection and validation.
- Results are not post-processed or filtered, they reflect raw outputs from each tool stage.
