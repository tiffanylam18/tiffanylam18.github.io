# Marine Conservation in the Coral Triangle

Analysis of marine protected area expansion across Indonesia, Philippines, Malaysia, Papua New Guinea, Timor-Leste, and Solomon Islands, examining whether current protection strategies will achieve 2030 global conservation targets.

**→ [View Live Project](https://tiffanylam18.github.io/project.html)**  
**→ [View Analysis Codebook](https://github.com/tiffanylam18/tiffanylam18.github.io/blob/13b7b3248af99376f18bb8271b80e8a387e2001b/PP434_project/analysis/Coral_Triangle_MPAs-Data_Analysis_Codebook.ipynb)**

---

## Project Overview

This analysis evaluates marine conservation progress in the Coral Triangle by:
- Quantifying protection gaps against international targets (10% by 2020, 30% by 2030)
- Identifying distinct MPA protection strategies through cluster analysis
- Analyzing governance structure variations across countries

**Key Finding:** All six countries fall catastrophically below global averages (<2% vs. 8.5% globally), requiring 53-1,537× acceleration to meet 2030 targets.

---

## Repository Structure
```
PP434_project/
├── analysis/
│   └── Coral_Triangle_MPAs-Data_Analysis_Codebook.ipynb    # Complete analysis codebook
├── data/                                                   # Processed datasets (ready for visualization)
│   ├── chart1_ct_choro.geojson                             # Choropleth map data
│   ├── chart2_cumulative_areas.json                        # Temporal growth data
│   ├── chart3_regression.json                              # 2030 projection data
│   ├── chart4_cluster_analysis.json                        # MPA archetype data
│   └── chart5_area_governance.json                         # Governance structure data
└── charts/                                                 # Vega-Lite visualization specifications
    ├── chart1_mpa-choro_vis.json
    ├── chart2_cumu-area_vis.json
    ├── chart3_ind-project_vis.json                         # Indonesia projection
    ├── chart3_phl-project_vis.json                         # Philippines projection
    ├── chart3_mys-project_vis.json                         # Malaysia projection
    ├── chart3_slb-project_vis.json                         # Solomon Islands projection
    ├── chart4_clust-analysis_vis.json
    └── chart5_gov-type_vis.json
```

---

## Data Sources

### Primary Dataset
**World Database on Protected Areas (WDPA)** - Protected Planet
- **Source:** https://www.protectedplanet.net/en/thematic-areas/marine-protected-areas
- **Files needed:** WDPA_Nov2025_Public_shp.zip (extract all 3 parts)
- **Description:** Global database of protected areas, including establishment dates, governance types, protection categories, and boundaries

### Supplementary Datasets
**Marine Exclusive Economic Zones (EEZ)** - Marine Regions
- **Source:** https://www.marineregions.org/downloads.php
- **File needed:** EEZ_land_union_v4_202410.shp
- **Purpose:** Maritime boundaries for calculating protection rates

**Global Protection Coverage** - Protected Planet
- **Source:** https://digitalreport.protectedplanet.net/?chapter=3
- **File needed:** global_wdpa_wdoecm_coverage_2000_2024.csv
- **Purpose:** Global benchmarking data (2000-2024)

---

## Replication Instructions

### Prerequisites
```bash
# Required Python packages
pip install pandas geopandas os requests json numpy scipy scikit-learn matplotlib seaborn
```

### Steps

1. **Download raw datasets** from sources listed above

2. **Update file paths** in analysis codebook (`analysis/Coral_Triangle_MPAs-Data_Analysis_Codebook.ipynb`):
```python
   # Configuration section (near top of codebook)
   DATA_DOWNLOAD_PATH = '[your_download_folder]/'
   DATA_UPLOAD_PATH = '[your_output_folder]/'
```

3. **Run analysis codebook** sequentially from top to bottom
   - All processing is automated after path configuration
   - No manual intervention required

4. **Generated outputs:**
   - 5 JSON files (charts 2-5)
   - 1 GeoJSON file (chart 1)
   - All exported to `DATA_UPLOAD_PATH`

### Processing Pipeline

The automated pipeline executes:
- **Filtering:** Coral Triangle countries, marine/coastal areas, operational status, valid years (1977-2025)
- **Deduplication:** Retains largest-area records for MPAs appearing across multiple files
- **Spatial joins:** Merges MPA statistics with EEZ boundaries
- **Temporal aggregation:** Calculates cumulative protection by country-year
- **Regression analysis:** Projects current trajectories to 2030 with 95% confidence intervals
- **K-means clustering:** Identifies 4 MPA groups based on size, age, protection intensity, IUCN category, and management plans

Every transformation is documented with inline comments in the codebook.

---

## Visualizations

Five interactive Vega-Lite visualizations:

1. **Geographic Distribution** (`chart1`) - Temporal choropleth map with year slider
2. **Growth Trends** (`chart2`) - Multi-line chart comparing countries to global averages
3. **2030 Target Projections** (`chart3`) - Regression analysis with confidence intervals (4 country panels)
4. **MPA Strategy Clusters** (`chart4`) - Interactive scatter plot with country filter
5. **Governance Structures** (`chart5`) - Stacked bar chart analyzing management types

**Interactive features:**
- Dropdown filters (country selection)
- Year slider (temporal exploration)
- Hover tooltips (detailed values)
- Clickable legends and datapoints (category highlighting)

---

## Technical Notes

### Data Processing
- **Deduplication strategy:** When same MPA appears across WDPA files, largest-area record retained
- **Geometry simplification:** EEZ boundaries simplified (0.05° tolerance) to reduce file size 85%
- **Filtering criteria:** Marine/coastal areas only, non-zero areas, operational status, valid establishment years

### Statistical Analysis
- **Regression:** Ordinary least squares with 95% CIs; countries with <5 observations excluded
- **Clustering:** K-means (k=4, random_state=0) on standardized features
- **Limitations:** Linear growth assumption may not capture sudden policy shifts; selection bias prevents biodiversity outcome assessment

### Automation Approach
Manual dataset downloads (not APIs) chosen for:
- Version consistency (WDPA releases annually)
- Complete geometry data without API pagination limits
- Simpler replication (download + run vs. API key management)

---

## Citation

If using this analysis, please cite:
```
Lam, T. (2025). Marine Conservation in the Coral Triangle: Progress, Patterns, and Priorities. 
Data Visualization Project, LSE. https://tiffanylam18.github.io/project.html
```

---

## Contact

Tiffany Lam  
[Email](tiffanykrystall8@gmail.com) | [LinkedIn](https://www.linkedin.com/in/lam-tiffany/) | [Portfolio](https://tiffanylam18.github.io/)

---

## License

Analysis code available for academic/non-commercial use. Data sources maintain original licenses.