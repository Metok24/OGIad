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
| `og_reference_ranges.csv` | Pre-computed OG reference ranges (5th–95th percentile) by variable and productivity class, derived from the UNESCO WH primary beech forests. Used as input to the public-use script. |

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

> **Note on the reference range:** The `og_reference_ranges.csv` provided here was derived from primary beech forests (Havesova, Kyjov, Stuzica, Life Prognoses primary plots, and other data sources; see Vanhellemont 2025). If your forests differ substantially in species composition or biogeographic region, consider whether this reference is appropriate for your application — see the manuscript discussion.

---

## Full Pipeline — Replicating the Analysis in Smith Metok et al.

The full pipeline (Steps 1–6) replicates the complete analysis from raw inventory data through to the final OGI scores and figures reported in the paper. Steps 1–3 translate the original SAS workflow into R and prepare the data; Steps 4–6 perform the OGI calculation itself and is what is included in the provided script.

### Data Availability

The raw input data (Winat inventory data and Life Prognoses plot data) currently embargoed until 2030 https://zenodo.org/records/15222927.

---

## Required R Packages

```r
install.packages(c("tidyverse", "FSA", "writexl", "patchwork", "scales"))
```

The scripts were developed and tested under **R version 4.5.2**. The public-use script (`OGI_calculation_Smith_Metok_et_al_2026_github.R`) requires only `tidyverse`.

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

> Smith Metok et al. *[Full citation to be added on publication]*

