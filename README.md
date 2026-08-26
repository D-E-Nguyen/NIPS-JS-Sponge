# NIPS-JS Sponge — Data & Analysis Code

📝 **Author:**

De Nguyen ([ORCID 0000-0001-5479-5927](https://orcid.org/0000-0001-5479-5927)),
Kyoto Institute of Technology.

Kenji Kinashi ([ORCID 0000-0003-4342-3516](https://orcid.org/0000-0003-4342-3516)),
Kyoto Institute of Technology.


🔗 **Browse the full rendered analysis online:**
<https://d-e-nguyen.github.io/NIPS-JS-Sponge/> (English) ·
[Bản tiếng Việt](https://d-e-nguyen.github.io/NIPS-JS-Sponge/vi.html) (Vietnamese) ·
[日本語版](https://d-e-nguyen.github.io/NIPS-JS-Sponge/ja.html) (Japanese)

This repository contains the dataset and the R Markdown analysis notebook behind the
statistical data analysis and visualization in the following research publications:

1. **Nonsolvent-Induced Phase Separation–Jet Spinning: An Innovative Technique for Producing
   Cellulosic Nanofilms, Suspensions, and Nanofilm-Based Sponges** (2025). *ACS Omega*,
   10 (31), 34389–34398.
   [https://doi.org/10.1021/acsomega.5c02353](https://doi.org/10.1021/acsomega.5c02353)

   📄 Open Access (CC-BY-NC-ND 4.0)

2. **Mechanically tunable nanofilm-based cellulose acetate sponges via crosslinker-free
   cryo-templating** (2025). *Polymer Journal*, 57, 1409–1420.
   [https://doi.org/10.1038/s41428-025-01083-z](https://doi.org/10.1038/s41428-025-01083-z)

   📄 Access: subscription required

---

## 📁 Repository contents

| File | Purpose |
|------|---------|
| `NIPS.Rmd` | The complete analysis notebook, organized as a pipeline: data overview → distributional checks (Shapiro–Wilk, Q–Q, Box–Cox) → per-factor boxplots → per-response regression & ANOVA → correlations (Pearson/Spearman) → multivariate analysis (PCA, multi-response models, MANOVA, ASCA) → response-surface methodology (first-/second-order models of Shrinkage, canonical analysis, extrapolation test) → Gibson–Ashby scaling. Figures are vector SVG with a consistent color system. |
| `NIPS.vi.Rmd`, `NIPS.ja.Rmd` | The same notebook with all prose translated into Vietnamese (Tiếng Việt) and Japanese (日本語). The R code is byte-identical to `NIPS.Rmd`, so all language versions produce identical figures and statistics. |
| `NIPS.csv` | **The study dataset** — 40 sponges, all fabrication factors and response variables. |
| `NIPS_validation.csv` | Three additional sponges (EtOH = 3 wt%) fabricated to validate the RSM prediction; not part of the *n* = 40 models. |
| `DATA_LICENSE.md` | License and citation terms for the datasets (CC BY 4.0). |
| `LICENSE` | MIT license for the analysis code. |
| `docs/` | The rendered notebooks (`index.html` English, `vi.html` Vietnamese, `ja.html` Japanese), the two CSVs, and `sitemap.xml`, served as a website via GitHub Pages. The CSVs here are copies of the root files — re-copy them whenever the data change, so the in-page download links keep working. |
| `head-meta.html`, `head-meta.vi.html`, `head-meta.ja.html` | Injected into the rendered pages' `<head>` at knit time (search-engine metadata, dataset markup, site-verification tag, `hreflang` language alternates); required for knitting — do not delete. |

The dataset is a 3 × 3 full factorial design (*n* = 40 sponges): `SUS` (polymer suspension
concentration; 0.24, 0.3, 0.4 wt%) × `EtOH` (ethanol cosolvent concentration; 0.2, 0.5,
1 wt%), with 4–7 replicates per combination (counted from the shipped dataset; the
Polymer Journal Experimental section quotes 3–5). A full column dictionary is included at the
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
  Porosity = 100·(1 − ρ/1311 kg·m⁻³); Shrinkage = 100·(1 − V/15 mL)); the SI tables print
  rounded values, and the published statistics were computed on the unrounded ones.
- Mechanical parameters come from a three-branch generalized Maxwell fit of the
  stress-relaxation curves: σ(t) = σₑ + Σ σᵢ·e^(−t/τᵢ) (`A0` = σₑ; `A1–A3` = σ₁–σ₃;
  `t1–t3` = τ₁–τ₃; `T` = τ = τ₁+τ₂+τ₃; `RS` = σᵣ, the normalized stress at test end;
  `Modulus` = apparent elastic modulus E\*).

### Correspondence to published results

Re-running the notebook on `NIPS.csv` reproduces the published statistics:

| Repository output | Published result |
|---|---|
| `NIPS.Rmd`: additive `lm`/`anova` for Height, Diameter, Shrinkage, Density | ACS Omega Table 1 and Tables S2–S5 |
| `NIPS.Rmd`: one-factor boxplots of those four variables | ACS Omega Figure 5 |
| `NIPS.Rmd`: interaction models for Modulus, RS, T, Recovery | Polymer Journal Table S2 |
| `NIPS.Rmd`: Spearman correlation analysis | Polymer Journal Figure S6 (subset Modulus, RS, T, Recovery) |
| `NIPS.Rmd`: Gibson–Ashby fit (nonlinear least squares) | Polymer Journal Figure 5b (*C* = 2.04, *n* = 2.48) |
| `NIPS.Rmd`: first-order `rsm` model of Shrinkage (response-surface section) | ACS Omega Table 2, Table S6, Figure 6j |

Note: the statistics involving `T` (characteristic relaxation time) in Polymer Journal
Table S2 and Figure S6 were derived from an earlier version of the Maxwell-fit
parameters; re-running the analysis on this final dataset weakens the
suspension-concentration effect on `T` to borderline, while the other conclusions for
that variable (and all results for every other variable) are unchanged. The notebook
discusses this in its opening section.

Other analyses in the repository (Pearson panel, PCA, MANOVA, ASCA, multi-response
models, Box–Cox, second-order RSM) are exploratory work beyond the published set.

---

## 🌐 Browse the notebook online

The full analysis is browsable online — no R required — in three languages:

- **English:** <https://d-e-nguyen.github.io/NIPS-JS-Sponge/>
- **Tiếng Việt:** <https://d-e-nguyen.github.io/NIPS-JS-Sponge/vi.html>
- **日本語:** <https://d-e-nguyen.github.io/NIPS-JS-Sponge/ja.html>

Each page links to the others at the top. All are rendered from the same R code, so every
figure, table, and statistic is identical; only the prose differs. (Figure and table labels
stay in English in every version, matching the publications.)

Reading aids built into the page:

- A **floating table of contents** for jumping between sections;
- **§ Anchor links** on every heading, so any section can be linked to directly;
- The whole analysis is a **single page**, so the browser's find-in-page (Ctrl/Cmd+F)
  searches every interpretation, table, and result at once;
- A **Code ▾ → Download Rmd** button (top right) that hands the reader the complete
  source file.


---

## ▶️ How to reproduce

1. Install the required packages:

   ```r
   install.packages(c("psych", "factoextra", "FactoMineR", "ggplot2", "dplyr",
                      "cowplot", "broom", "knitr", "MASS", "car", "rsm", "emmeans",
                      "svglite", "rmarkdown"))
   ```

2. Knit `NIPS.Rmd` (e.g. the **Knit** button in RStudio, or
   `rmarkdown::render("NIPS.Rmd")`); knitting `NIPS.vi.Rmd` or `NIPS.ja.Rmd` the same way
   produces the Vietnamese or Japanese version. HTML and Word output work for all three.
   PDF output works for the English notebook; the translations need a Unicode-capable
   engine (add `latex_engine: xelatex` and a CJK-capable `mainfont` to the `pdf_document`
   block first).

3. To regenerate the published site, render each notebook into `docs/` under a UTF-8
   locale:

   ```r
   rmarkdown::render("NIPS.Rmd",    output_dir = "docs", output_file = "index.html")
   rmarkdown::render("NIPS.vi.Rmd", output_dir = "docs", output_file = "vi.html")
   rmarkdown::render("NIPS.ja.Rmd", output_dir = "docs", output_file = "ja.html")
   ```

   `docs/` also serves `NIPS.csv` and `NIPS_validation.csv` so the in-page download links
   work on the live site; re-copy them if the data ever change.

Notes:

- Code chunks are hidden in the rendered reports (`echo = FALSE`); open the `.Rmd` file
  to read the code itself, which is commented throughout.
- Knitting `NIPS.Rmd` also writes two small output files next to the document
  (`spearman_correlation_matrix.csv`, `spearman_p_matrix.csv`), used for the papers'
  supplementary tables.
- **Render in a UTF-8 locale.** RStudio's **Knit** button already does this. When knitting
  non-interactively (`Rscript`, CI, `make`), set the character locale explicitly —
  `LC_CTYPE=en_US.UTF-8 Rscript -e 'rmarkdown::render("NIPS.Rmd")'` — otherwise R escapes
  the non-ASCII characters in table headers (`Optimal λ`, `*R*²`) as literal
  `<U+03BB>` / `<U+00B2>` text in the output. Leave `LC_COLLATE=C` so sort orders stay
  byte-reproducible.
- Figures are rendered as vector graphics (`dev = "svglite"`), so the self-contained
  HTML stays under 6 MB and every figure stays sharp at any zoom level. For Word or
  PDF output, switch `dev` to `"png"` in the `setup` chunk.
- All figures share one color system: blues encode the suspension-concentration levels
  (light → dark = low → high) and warm reds encode the ethanol levels, so hue identifies
  the factor and darkness the level throughout the document.

---

## 📖 For readers

Each analysis section is followed by an **Interpretation** block explaining what the
output means, why that method was chosen, and what its limitations are. The notebook is
therefore usable as a worked example of a factorial-design analysis, not only as a
reproduction script. Topics covered along the way include:

- Why marginal normality tests can fail on perfectly well-behaved factorial data;
- What standardizing does and does not make comparable in a boxplot;
- Sequential (Type I) versus order-free (Type II) sums of squares in an unbalanced design;
- How to read PCA loadings, contributions and biplot ellipses — and why overlapping
  ellipses can mean a small effect rather than no effect;
- Why canonical eigenvalues must be read on coded, not raw, factor scales;
- A concrete demonstration that a first-order surface extrapolated better than a
  second-order one outside the design region;
- A self-contained, fully executed ASCA (ANOVA–simultaneous component analysis) written
  out step by step rather than imported from a package;
- Why the Gibson–Ashby prefactor *C* is intrinsically hard to estimate from a narrow
  density window, and how to report scaling constants honestly.

The mechanistic interpretation of the results (cell-wall thickening, ice-templating
control, nanofilm delamination and slippage) belongs to the two papers cited above; this
notebook covers the statistical side and points to them for the materials science.

---

## 📚 How to cite

If this repository's data or analyses are useful in your research, please cite the
corresponding publication(s):

```bibtex
@article{Nguyen2025NIPSJS,
  author  = {Nguyen, De and Kinashi, Kenji and Nishikawa, Yukihiro and
             Sakai, Wataru and Tsutsumi, Naoto},
  title   = {Nonsolvent-Induced Phase Separation--Jet Spinning: An Innovative
             Technique for Producing Cellulosic Nanofilms, Suspensions, and
             Nanofilm-Based Sponges},
  journal = {ACS Omega},
  year    = {2025},
  volume  = {10},
  number  = {31},
  pages   = {34389--34398},
  doi     = {10.1021/acsomega.5c02353}
}

@article{Nguyen2025Sponges,
  author  = {Nguyen, De and Kinashi, Kenji and Nishikawa, Yukihiro and
             Sakai, Wataru and Tsutsumi, Naoto},
  title   = {Mechanically tunable nanofilm-based cellulose acetate sponges via
             crosslinker-free cryo-templating},
  journal = {Polymer Journal},
  year    = {2025},
  volume  = {57},
  pages   = {1409--1420},
  doi     = {10.1038/s41428-025-01083-z}
}
```

---

## 📜 Licensing

- **Code** (`NIPS.Rmd`, `NIPS.vi.Rmd`, `NIPS.ja.Rmd`): MIT License (`LICENSE`).
- **Data** (`NIPS.csv`, `NIPS_validation.csv`): CC BY 4.0 (`DATA_LICENSE.md`) — please
  cite the two publications above when reusing the data.
