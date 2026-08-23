# Data License

The dataset files in this repository —

- `NIPS.csv` — the 40-sponge characterisation dataset (fabrication factors, geometry,
  and stress-relaxation mechanical parameters), and
- `NIPS_validation.csv` — three additional sponges (EtOH = 3 wt%) used to validate the
  response-surface-methodology prediction

— are © 2025 De Nguyen and are licensed under the **Creative Commons Attribution 4.0
International License (CC BY 4.0)**: <https://creativecommons.org/licenses/by/4.0/>

You are free to share and adapt these data for any purpose, including commercially,
provided you give appropriate credit.

The **code** in this repository (`NIPS.Rmd`) is licensed separately under the
MIT License — see `LICENSE`.

## How to cite

If you use these data, please cite the publications in which they were originally
reported:

1. Nguyen, D.; Kinashi, K.; Nishikawa, Y.; Sakai, W.; Tsutsumi, N.
   *Nonsolvent-Induced Phase Separation–Jet Spinning: An Innovative Technique for
   Producing Cellulosic Nanofilms, Suspensions, and Nanofilm-Based Sponges.*
   ACS Omega **2025**, 10 (31), 34389–34398.
   <https://doi.org/10.1021/acsomega.5c02353>

2. Nguyen, D.; Kinashi, K.; Nishikawa, Y.; Sakai, W.; Tsutsumi, N.
   *Mechanically tunable nanofilm-based cellulose acetate sponges via crosslinker-free
   cryo-templating.* Polymer Journal **2025**, 57, 1409–1420.
   <https://doi.org/10.1038/s41428-025-01083-z>

## Provenance

The geometry variables (`Weight` … `Shrinkage`) correspond to Table S1 of the ACS Omega
Supporting Information; the mechanical variables (`Recovery` … `RS`) correspond to
Table S1 of the Polymer Journal Supplementary Information. Both SI tables list the same
40 sponges in the same row order. Primary measurements (`Weight`, `Diameter`, `Height`)
are as recorded; the derived quantities (`Volume`, `Density`, `Porosity`, `Shrinkage`)
are computed at full precision from the primary measurements using the equations given
in the papers (the SI tables print them rounded).
