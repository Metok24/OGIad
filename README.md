# OGIad
The simplified calculation script for Old-Growth Index adjusted for the EU Guideline criteria

# Old-Growth Indicator (OGI adjusted) — R Code Repository

This repository contains the R scripts used to calculate the Old-Growth Indicator (OGI adjusted) in:

> Smith Metok et al. (2026). *[Full citation to be added on publication]*. [Journal name]. [DOI link]

The OGI adjusted method is based on Meyer et al. (2021, *Ecological Indicators* 125:107575) and compares bootstrapped forest structural measurements against a reference range derived from primary beech forests across Europe.

---

## Repository Contents

| File | Description |
|------|-------------|
| `LProg_OGI_Step1_Compile_Reference_Values_Eastern_Slovakia.R` | Calculates structural indicators (stem density, basal area, deadwood, regeneration, habitat trees) from the Winat inventory data for the eastern Slovak old-growth plots |
| `LProg_OGI_Step2_Compile_Reference_Values_Eastern_Slovakia.R` | Derives the final OGI variable values for the Slovak old-growth reference plots before bootstrapping |
| `LProg_OGI_Step3_OGI_Variables_Stratum.R` | Calculates OGI variables from the Life Prognoses dataset and assigns plots to strata; appends the Slovak reference plots |
| `LProg_OGI_Step4_Bootstrapping_ValueSpans_OGI_Variables_Strats.R` | Bootstraps plot data within strata (and OG reference plots overall) to derive 5th–95th percentile value ranges per variable |
| `LProg_OGI_Step5_OGI_adjusted_Calculation_Strats.R` | Compares each stratum's bootstrapped range against the OG reference range and calculates per-variable OGI scores (0–1) |
| `LProg_OGI_Step6_OGI_adjusted_weighted_Strats.R` | Weights and aggregates variable scores to group-level and overall OGI; produces summary tables and figures |
| `OGI_calculation_Smith_Metok_et_al_2026_github.R` | **Public-use script.** Runs Steps 4–6 on user-supplied plot data using the pre-computed OG reference ranges. Start here if you want to apply the OGI to your own data. |
| `og_reference_ranges.csv` | Pre-computed OG reference ranges (5th–95th percentile) by variable and productivity class, derived from the Slovak primary forests and Life Prognoses primary plots. Used as input to the public-use script. |

---

## Quick Start — Applying the OGI to Your Own Data

If you want to calculate the OGI adjusted for your own forest plots, you only need two files:

- `OGI_calculation_Smith_Metok_et_al_2026_github.R`
- `og_reference_ranges.csv`

**Steps:**

1. Install the required R packages (see below).
2. Prepare your plot data as a CSV file following the format described in the header of the script. The key columns are `plot_id`, `site_id`, `stratum`, `prod`, `ha`, `npfl_stratum`, `hapfl_stratum`, and the nine OGI variable columns.
3. Open the script and edit the paths and settings in the **CONFIGURATION** section at the top (file paths, number of bootstrap iterations).
4. Run the script. Results are written to an `output/` folder.

The script includes input validation, informative warnings, and notes explaining each step. See the **NOTES FOR USERS** section at the bottom of the script for guidance on stratum design, productivity classes, and small datasets.

> **Note on the reference range:** The `og_reference_ranges.csv` provided here was derived from primary beech forests (Havesova, Kyjov, Stuzica, and Life Prognoses primary plots). If your forests differ substantially in species composition or biogeographic region, consider whether this reference is appropriate for your application — see the manuscript discussion.

---

## Full Pipeline — Replicating the Analysis in Smith Metok et al.

The full pipeline (Steps 1–6) replicates the complete analysis from raw inventory data through to the final OGI scores and figures reported in the paper. Steps 1–3 translate the original SAS workflow into R and prepare the data; Steps 4–6 perform the OGI calculation itself.

The scripts are designed to be run sequentially. Each script expects the R objects created by the previous step to be present in your session. The recommended workflow is to run them in order within a single R session, or to save and reload intermediate objects between sessions.

### Expected Folder Structure

```
project-root/
├── raw data/
│   ├── natroh_winlist.csv
│   ├── natroh_winlig.csv
│   ├── natroh_winnvg.csv
│   ├── natroh_winstg.csv
│   ├── nataus_win_gw_22.csv
│   ├── nataus_win_gw_23.csv
│   ├── nataus_win_gw_24.csv
│   ├── nataus_win_lfm_22.csv
│   ├── nataus_win_lfm_23.csv
│   ├── nataus_win_lfm_24.csv
│   ├── nwaus_life_prog_plots.csv
│   ├── nwaus_life_prog_trees.csv
│   ├── nwaus_life_prog_summary.csv
│   ├── nwaus_life_prog_microh.csv
│   └── nwaus_life_prog_lyingdead.csv
├── output/                   ← created automatically by the scripts
├── LProg_OGI_Step1_...R
├── LProg_OGI_Step2_...R
├── ...
└── og_reference_ranges.csv
```

### Data Availability

The raw input data (Winat inventory data and Life Prognoses plot data) cannot be shared publicly. For data access enquiries, please contact [contact name/email or data repository link to be added].

---

## Required R Packages

```r
install.packages(c("tidyverse", "FSA", "writexl", "patchwork", "scales"))
```

The scripts were developed and tested under **R version [X.X.X — to be confirmed]**. The public-use script (`OGI_calculation_Smith_Metok_et_al_2026_github.R`) requires only `tidyverse`.

---

## OGI Variables

The nine OGI variables used in this analysis, their units, and their thematic groups are:

| Variable | Description | Unit | Group |
|----------|-------------|------|-------|
| `vha_ls` | Volume of living trees (dbh ≥ 10 cm) | m³/ha | Old or large trees |
| `nha_gtree` | Very large trees per ha (dbh ≥ 60–80 cm depending on productivity) | n/ha | Old or large trees |
| `vha_tg` | Total coarse woody debris volume | m³/ha | Deadwood |
| `nha_hoe` | Trees with cavities per ha | n/ha | Habitat trees |
| `nha_pilz` | Trees with perennial polypore fungi per ha | n/ha | Habitat trees |
| `diqr` | Interquartile range of stem diameter | cm | Structural complexity |
| `vwep` | Number of forest development stages present | count | Structural complexity |
| `sukdn` | Successional status (weighted: climax = 3, intermediate = 2, pioneer = 1) | index | Indicator species |
| `pnaut` | Proportion of native tree species | % | Native species |

Each variable receives equal weight within its group; each group receives equal weight (1/6) in the final aggregated OGI score. See the manuscript and Meyer et al. (2021) for full methodological details.

---

## Citation

If you use these scripts or the reference ranges in your work, please cite the paper:

> Smith Metok et al. (2026). *[Full citation to be added on publication]*

You may also cite the code repository directly:

> Smith Metok et al. (2026). *OGI adjusted — R code repository*. GitHub. [URL] [DOI via Zenodo — to be added]

---

## License

[To be decided — e.g. MIT License or CC BY 4.0]

---

## Contact

For questions about the code or method, please open an issue on this repository or contact [corresponding author name, email].
