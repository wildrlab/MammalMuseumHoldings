# Global Geography of Museum Specimen Holdings

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.XXXXXX.svg)](https://doi.org/10.5281/zenodo.XXXXXX)

## Overview

This repository contains the complete, reproducible analysis code for:

**Mills, M. W. (2025). Global Geography of Natural History Museum Specimen Holdings: A Time-Resolved Network Analysis of Mammal Collections, 1900–2020. *Biodiversity Data Journal***

### Citation

If you use this code or data, please cite:

```
Mills, M. W. (2025). Global Geography of Natural History Museum Specimen Holdings: 
A Time-Resolved Network Analysis of Mammal Collections, 1900–2020. 
Biodiversity Data Journal, XX:eXXXXX. https://doi.org/10.3897/BDJ.XX.eXXXXX
```

### Abstract

Natural history collections are foundational infrastructure for biodiversity science, but the global geography of specimen custody has rarely been quantified through time. We analyzed 253,131 preserved-specimen records from GBIF spanning 1900–2020 for three mammalian families (Canidae, Felidae, Mustelidae) to reveal:

- **Extreme concentration**: United States holds 55% of specimens; top 10 countries hold 90%
- **Divergent inequality trends**: Mustelidae showed U-shaped pattern (re-concentration), while Canidae and Felidae showed sustained democratization
- **Network contraction**: 23-29% decline in participating countries, 39-56% decline in flows
- **Low reciprocity**: <7.5% bidirectional exchange, indicating extractive flow patterns

---

## Repository Structure

```
.
├── README.md                          # This file
├── MuseumHoldings_Analysis.Rmd        # Main analysis R Markdown
├── data/                              # Data directory (not tracked)
│   └── README.md                      # Instructions for obtaining data
├── outputs/                           # Generated outputs
│   ├── figs/                          # All figures (PDF + PNG)
│   └── tables/                        # Summary statistics and test results
├── scripts/                           # Helper scripts
│   └── download_gbif_data.R           # Download data from GBIF
└── docs/                              # Documentation
    ├── ANALYSIS_GUIDE.md              # Detailed analysis walkthrough
    └── REPRODUCIBILITY_NOTES.md       # Notes on reproducing analysis
```

---

## Requirements

### Software

- **R version**: 4.3.1 or higher
- **RStudio**: Recommended for running R Markdown

### R Packages

All required packages are loaded automatically in the R Markdown file. Key dependencies:

| Package | Version | Purpose |
|---------|---------|---------|
| dplyr | 1.1.3 | Data manipulation |
| ggplot2 | 3.4.4 | Visualization |
| sf | 1.0-14 | Spatial data |
| igraph | 1.5.1 | Network analysis |
| ineq | 0.2-13 | Inequality metrics (Gini) |
| rnaturalearth | 0.3.4 | World map data |
| countrycode | 1.5.0 | Country code conversion |

Install all dependencies:

```r
install.packages(c(
  "dplyr", "tidyr", "purrr", "readr",
  "ggplot2", "scales", "ggrepel", "patchwork",
  "sf", "rnaturalearth", "countrycode",
  "igraph", "ineq"
))
```

---

## Data

### Source Data

All specimen data are from the Global Biodiversity Information Facility (GBIF):

**GBIF Downloads:**
- Canidae: https://doi.org/10.15468/dl.XXXXXX
- Felidae: https://doi.org/10.15468/dl.XXXXXX  
- Mustelidae: https://doi.org/10.15468/dl.XXXXXX

**Download date:** October 2025

### Data Access

1. **Option A - Use our processed data** (recommended):
   - Download from Zenodo: https://doi.org/10.5281/zenodo.XXXXXX
   - Place in `data/` directory

2. **Option B - Download fresh from GBIF**:
   - Run `scripts/download_gbif_data.R`
   - Requires GBIF account (free)

### Data Structure

The analysis expects a dataframe called `flows` with the following columns:

| Column | Type | Description |
|--------|------|-------------|
| family | character | Canidae, Felidae, or Mustelidae |
| decade | integer | Collection decade (1900, 1910, ..., 2020) |
| collecting_country | character | Country where specimen was collected |
| holding_country | character | Country where specimen is currently held |
| n | numeric | Number of specimens in this flow |

---

## Running the Analysis

### Quick Start

1. **Clone this repository:**
   ```bash
   git clone https://github.com/yourusername/museum-holdings-analysis.git
   cd museum-holdings-analysis
   ```

2. **Install R packages** (if not already installed):
   ```r
   source("scripts/install_packages.R")
   ```

3. **Obtain data:**
   - Download processed data from Zenodo (see Data section above)
   - OR run `source("scripts/download_gbif_data.R")`

4. **Run the analysis:**
   - Open `MuseumHoldings_Analysis.Rmd` in RStudio
   - Click "Knit" button
   - OR run: `rmarkdown::render("MuseumHoldings_Analysis.Rmd")`

### Expected Runtime

- **First run** (with fresh data): ~10-15 minutes
- **Subsequent runs** (with cache): ~2-3 minutes

### Outputs

All outputs are generated in the `outputs/` directory:

**Figures** (`outputs/figs/`):
- `fig1_holdings_over_time.{pdf,png}` - Stacked bar chart of top countries
- `fig2_network_maps_combined.{pdf,png}` - Network flow maps by period
- `fig3_metrics_panels.{pdf,png}` - Six-panel network metrics figure
- `fig4_net_importers_exporters.{pdf,png}` - Top importers/exporters
- `figS1_canidae_networks.{pdf,png}` - Supplementary: Canidae networks
- `figS2_felidae_networks.{pdf,png}` - Supplementary: Felidae networks
- `figS3_mustelidae_networks.{pdf,png}` - Supplementary: Mustelidae networks

**Tables** (`outputs/tables/`):
- `network_metrics_all_slices.csv` - Complete network metrics
- `gini_all_slices.csv` - Inequality measures
- `statistical_tests_summary.csv` - Statistical test results
- `summary_statistics.csv` - Dataset summary

---

## Key Findings

### 1. Extreme Geographic Concentration

- **United States** holds ~55% of all digitized specimens
- **Top 10 countries** account for ~90% of holdings
- **Source:Repository ratio** of 4:1 (178 origin countries → 44 holding countries)

### 2. Divergent Inequality Trajectories

| Family | Pattern | Gini (1900-1929) | Gini (1990-2020) | Change |
|--------|---------|------------------|------------------|--------|
| **Mustelidae** | U-shaped | 0.85 | 0.86 | **Re-concentration** |
| **Canidae** | Gradual decline | 0.87 | 0.81 | Moderate democratization |
| **Felidae** | Steep decline | 0.89 | 0.84 | Strong democratization |

### 3. Network Contraction

- **Network size**: Declined 23-29% from mid-century peak
- **Network complexity**: Declined 39-56% in number of flows
- **Peak period**: 1930-1959 to 1960-1989
- **Recent decline**: Genuine reduction + digitization lag

### 4. Extractive Flow Structure

- **Reciprocity**: <7.5% (mean across all periods)
- **Pattern**: Biodiversity-rich South → Museum-rich North
- **Persistent**: No improvement despite Nagoya Protocol (2014)

---

## Methods Summary

### Network Construction

1. **Nodes**: Countries (ISO3 codes)
2. **Edges**: Directed flows from collection country → holding country
3. **Weights**: Number of specimens
4. **Self-loops**: Excluded from topology metrics, included in inequality

### Metrics Calculated

| Metric | Definition | Interpretation |
|--------|-----------|----------------|
| **Network size** | Number of countries | Geographic breadth |
| **Network complexity** | Number of flows | Exchange diversity |
| **Density** | Fraction of possible edges | Connectedness |
| **Reciprocity** | Fraction bidirectional | Mutualism vs. extraction |
| **Giant component** | % in largest component | Network cohesion |
| **Gini coefficient** | Inequality in holdings | Concentration (0=equal, 1=total inequality) |

### Time Periods

Four 30-year bins chosen to align with historical phases:
- **1900-1929**: Colonial era and early systematic collecting
- **1930-1959**: Post-WWII museum expansion
- **1960-1989**: Decolonization and conservation biology
- **1990-2020**: Digital era and Nagoya Protocol

### Statistical Tests

- **Temporal trends**: Linear models (nodes, edges, density, reciprocity)
- **Gini trajectories**: Quadratic models (U-shaped test)
- **Family differences**: Mixed-effects models with pairwise comparisons
- **Early vs. Recent**: Welch's t-tests
- **Metric correlations**: Pearson correlation + linear regression

---

## Reproducibility

### Checksums

SHA256 checksums for key files:

```
MuseumHoldings_Analysis.Rmd: [to be added]
data/flows_processed.rds: [to be added]
```

### Session Info

The analysis was run with:
- R version 4.3.1 (2023-06-16)
- Platform: x86_64-apple-darwin20 (64-bit)
- OS: macOS 14.1

Full session info is included at the end of the rendered HTML output.

### Known Issues

1. **GBIF download timing**: Results may vary slightly if data are re-downloaded due to ongoing digitization
2. **Projection**: Robinson projection can introduce small visual distortions near poles
3. **Country code changes**: Historical country boundaries (e.g., Yugoslavia) mapped to modern ISO3

---

## Contributing

While this analysis is published, we welcome:
- **Bug reports**: Open an issue
- **Suggestions**: Open an issue or pull request
- **Extensions**: Fork and cite!

---

## License

### Code

All code in this repository is licensed under **MIT License**.

### Data

- **GBIF data**: See individual dataset licenses (typically CC0 or CC-BY)
- **Derived datasets**: Released under **CC-BY 4.0**

### Manuscript

The manuscript text and figures are © Mystyn Mills, published under CC-BY 4.0.

---

## Contact

**Mystyn Mills**  
WILDeR Lab  
Department of Geography  
California State University, Long Beach  
📧 mystyn.mills@csulb.edu  
🌐 [Lab website](https://example.com)

---

## Acknowledgments

This research used data from the Global Biodiversity Information Facility (GBIF). We thank the institutions and individuals who contributed specimen records to GBIF, making this analysis possible.

---

## Version History

- **v1.0.0** (2025-01-XX): Initial release accompanying BDJ publication

---

**Last updated:** January 2025
