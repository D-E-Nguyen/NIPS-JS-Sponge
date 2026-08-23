# NIPS-JS Sponge — Data & Analysis Code

This repository contains the dataset and the R scripts (R Markdown) used for the
statistical data analysis and visualization in the following research publications:

1. **Nonsolvent-Induced Phase Separation–Jet Spinning: An Innovative Technique for Producing
   Cellulosic Nanofilms, Suspensions, and Nanofilm-Based Sponges** (2025). *ACS Omega*,
   10 (31), 34389–34398.
   [https://doi.org/10.1021/acsomega.5c02353](https://doi.org/10.1021/acsomega.5c02353)

   📄 Open Access (CC-BY-NC-ND 4.0)

2. **Mechanically tunable nanofilm-based cellulose acetate sponges via crosslinker-free
   cryo-templating** (2025). *Polymer Journal*, 57, 1409–1420.
   [https://doi.org/10.1038/s41428-025-01083-z](https://doi.org/10.1038/s41428-025-01083-z)

   📄 Access: Subscription Required

---

## 📁 Repository contents

| File | Purpose |
|------|---------|
| `NIPS.Rmd` | The complete analysis notebook, organised as a pipeline: data overview → distributional checks (Shapiro–Wilk, Q–Q, Box–Cox) → per-factor boxplots → per-response regression & ANOVA → correlations (Pearson/Spearman) → multivariate analysis (PCA, multi-response models, MANOVA) → response-surface methodology (first-/second-order models of Shrinkage, canonical analysis, steepest descent) → Gibson–Ashby scaling. |
| `NIPS.csv` | **The study dataset** — 40 sponges, all fabrication factors and response variables. |
| `NIPS_validation.csv` | Three additional sponges (EtOH = 3 wt%) fabricated to validate the RSM prediction; not part of the n = 40 models. |
| `DATA_LICENSE.md` | License and citation terms for the datasets (CC BY 4.0). |
| `LICENSE` | MIT license for the analysis code. |

The dataset is a 3 × 3 full factorial design (n = 40 sponges): `SUS` (polymer suspension
concentration; 0.24, 0.3, 0.4 wt%) × `EtOH` (ethanol cosolvent concentration; 0.2, 0.5,
1 wt%), with 4–7 replicates per combination. A full column dictionary is included at the
top of `NIPS.Rmd`.

---

## 📊 Data

The dataset is included in this repository and is licensed **CC BY 4.0** (© 2025
De Nguyen) — see `DATA_LICENSE.md` for citation terms and full provenance.

- The geometry variables (`Weight` … `Shrinkage`) correspond to Table S1 of the ACS Omega
  Supporting Information; the mechanical variables (`Recovery` … `RS`) correspond to
  Table S1 of the Polymer Journal Supplementary Information. Both SI tables list the same
  40 sponges in the same row order.
- Primary measurements (`Weight`, `Diameter`, `Height`) are as recorded. The derived
  responses (`Volume`, `Density`, `Porosity`, `Shrinkage`) are stored at **full
  precision**, computed with the papers' equations (V = π/4·h·d²; ρ = m/V;
  Porosity = 100·(1 − ρ/1311); Shrinkage = 100·(1 − V/15 mL)); the SI tables print
  rounded values, and the published statistics were computed on the unrounded ones.
- Mechanical parameters come from a three-branch generalized Maxwell fit of the
  stress-relaxation curves: σ(t) = σₑ + Σ σᵢ·e^(−t/τᵢ) (`A0` = σₑ; `A1–A3` = σ₁–σ₃;
  `t1–t3` = τ₁–τ₃; `T` = τ = τ₁+τ₂+τ₃; `RS` = σᵣ, the normalized stress at test end;
  `Modulus` = apparent elastic modulus E\*).

### Correspondence to published results

Re-running these scripts on `NIPS.csv` reproduces the published statistics:

| Repository output | Published result |
|---|---|
| `NIPS.Rmd`: additive `lm`/`anova` for Height, Diameter, Shrinkage, Density | ACS Omega Table 1 and Tables S2–S5 |
| `NIPS.Rmd`: one-factor boxplots of those four variables | ACS Omega Figure 5 |
| `NIPS.Rmd`: interaction models for Modulus, RS, T, Recovery | Polymer Journal Table S2 |
| `NIPS.Rmd`: Spearman correlation analysis | Polymer Journal Figure S6 (subset Modulus, RS, T, Recovery) |
| `NIPS.Rmd`: Gibson–Ashby fit (nonlinear least squares) | Polymer Journal Figure 5b (C = 2.04, n = 2.48) |
| `NIPS.Rmd`: first-order `rsm` model of Shrinkage (response-surface section) | ACS Omega Table 2, Table S6, Figure 6j |

Note: the statistics involving `T` (characteristic relaxation time) in Polymer Journal
Table S2 and Figure S6 were derived from an earlier version of the Maxwell-fit
parameters; re-running the analysis on this final dataset yields slightly different
values for that one variable, with unchanged qualitative conclusions.

Other analyses in the repository (Pearson panel, PCA, MANOVA, multi-response models,
Box–Cox, second-order RSM) are exploratory work beyond the published set.

---

## ▶️ How to reproduce

1. Install the required packages:

   ```r
   install.packages(c("psych", "factoextra", "FactoMineR", "ggplot2", "dplyr",
                      "cowplot", "broom", "knitr", "MASS", "rsm", "emmeans",
                      "rmarkdown"))
   ```

2. Knit `NIPS.Rmd` (e.g. the **Knit** button in RStudio, or
   `rmarkdown::render("NIPS.Rmd")`). The document can be rendered to HTML, Word, or PDF.

Notes:

- Code chunks are hidden in the rendered reports (`echo = FALSE`); open the `.Rmd` files
  to read the code itself, which is commented throughout.
- Knitting `NIPS.Rmd` also writes two small output files next to the document
  (`spearman_correlation_matrix.csv`, `spearman_p_matrix.csv`), used for the papers'
  supplementary tables.

---

## 📜 Licensing

- **Code** (`NIPS.Rmd`): MIT License (`LICENSE`).
- **Data** (`NIPS.csv`, `NIPS_validation.csv`): CC BY 4.0 (`DATA_LICENSE.md`) — please
  cite the two publications above when reusing the data.
