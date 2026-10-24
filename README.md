# Driving data and documentation for Manuscript 01

These materials accompany *Upcoming Road Grade and Control-Energy Responses in Naturalistic Heavy-Truck Operation*. They provide four illustrative driving excerpts and their source information for inspecting the recorded operating signals. The excerpts are a data illustration, not the full analysis-anchor dataset or a package for reproducing model-performance results.

## Contents

- `driving_cycles.csv`: four excerpts, each with 600 consecutive samples at 1 s spacing (elapsed time 0-599 s).
- `cycle_summary.csv`: source-file codes, exact row ranges, class and original split, basic speed/grade summaries and missing-signal counts.
- `source_files.csv`: the 55 source files used in the study and their original file-level training/evaluation assignment.
- `SHA256SUMS.txt`: checksums for the four content files.

## Source and excerpt selection

Source dataset: LiveWire, `covar/medium-heavy-truck-duty-cycles`, https://livewire.energy.gov . Dataset metadata: https://livewire.energy.gov/api/datasets/covar/medium-heavy-truck-duty-cycles . Source filenames are recorded in `source_files.csv`.

One excerpt is selected for each Class 6/Class 8 and training/evaluation combination. Within each combination, source files are visited in ascending `source_file_code`. The first 600-row interval with consecutive 1 s timestamps, finite filtered speed and grade, and a starting speed of at least 20 km/h is selected. Selection uses recorded signals and the source split only. No model outputs or performance scores enter selection. The excerpts illustrate different operating records; their small-sample distributions do not replace the full-study coverage statistics.

`source_row_start_0based` and `source_row_end_0based` refer to data rows in the named source CSV, excluding its header. Source signal text and precision are copied unchanged. No additional filtering, interpolation, imputation or unit conversion is applied. `elapsed_s` is relative time within each excerpt. The source-provided speed channel is already filtered. These excerpts are continuous recording segments, not the overlapping 60-step anchors used by the analysis.

## Fields

| Exported field | Meaning and source column |
|---|---|
| `cycle_id` | Excerpt key linking the two cycle tables |
| `elapsed_s` | Seconds from the first exported sample |
| `filtered_speed_kmh` | `Filtered Speed (km/hr)`, in km/h |
| `grade_fraction` | `Road Grade (%/100)`, rise/run; 0.01 means 1% grade |
| `fuel_rate_pct` | `Engine Fuel Rate (%)`, source percentage signal |
| `flywheel_power_pct` | `Flywheel Power (%)`, source percentage signal |
| `torque_pct` | `Torque (%)`, source percentage signal |

The three engine-related signals retain the source percentage scale and are not absolute fuel flow or energy measurements. Any source missing values are retained; missing-signal counts are listed per excerpt. The current four excerpts have complete values for these channels. The CSV files can be inspected with a spreadsheet or a standard CSV reader. This data package contains no reconstruction, calibration or prediction implementation and no fitted parameter sets.
