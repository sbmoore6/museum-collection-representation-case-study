# Cultural Representation in American Art Museums  
**Analyzing Global Representation in Major U.S. Museum Collections**

<p align="center">
  <img src="docs/images/aic_museum.avif" height="250" />
  <img src="docs/images/world_map.jpg" height="250" />
</p>

This project analyzes **cultural representation patterns** across two major U.S. art museum collections using publicly available metadata. The goal is to evaluate how well different global regions are represented and identify potential imbalances in collection composition.

The study examines collections from the **Metropolitan Museum of Art (MET)** and the **Art Institute of Chicago (AIC)**, analyzing representation at both the **country** and **continent** level and comparing museum representation against **global population** and **landmass distribution**.

This repository serves as a **portfolio companion** to the [original academic project](https://github.com/mollykstark/SIADS-Milestone-1/tree/main) and highlights the data engineering, cleaning, and analytical methodology used.

---

## Motivation

Large U.S. art museums often aim to present a globally representative collection. However, prior research suggests significant imbalance.  
A study by *Topaz et al. (2019)* found that among ~10,000 identifiable artists across 18 U.S. museums, **75.7% were white men**, indicating heavy concentration in North American and European art.

This project investigates whether similar patterns appear in the collections of the MET and AIC and identifies regions that may be underrepresented.

---

## Objectives

1. Extract and standardize country-of-origin data for each artwork  
2. Analyze representation by country and continent:
   - Per museum
   - Combined dataset  
3. Compare museum representation against:
   - Global population distribution
   - Continental landmass distribution  

These objectives were designed to surface potential **collection bias** and **acquisition imbalance**.

---

## Data Sources

### Metropolitan Museum of Art – Open Access Dataset  
- ~450,000 catalogued objects (partial collection)
- Key variables:
  - Country
  - Culture
  - Artist Nationality
  - Region
  - Acquisition Date
- Format: CSV (~303 MB)

### Art Institute of Chicago – Public API Data  
- ~130,000 catalogued artworks
- Key variables:
  - Title
  - Artist
  - Place of Origin
  - Acquisition Date
- Format: JSON (~688 MB total)

Both datasets required **extensive preprocessing** to standardize geographic origin information.

---

## Methodology

### MET Data Cleaning
**Key steps:**
1. Ranked multiple columns by likelihood of containing geographic origin  
2. Combined fields using prioritized fallback logic  
3. Built a country normalization dictionary (alternate names, demonyms)  
4. Applied regex-based cleaning for punctuation and noise  
5. Manually reviewed unmapped values  
6. Converted countries to continents using `pycountry-convert`

- Final missing country rate: **~8.6%**
- Due to size constraints, a **random sample of 150,000 records** was used for analysis

---

### AIC Data Cleaning
**Key steps:**
1. Removed rows missing location data (~7%)  
2. Direct-mapped known country values  
3. Converted non-country locations using OpenStreetMap (via `geopy`)  
4. Extracted country names via regex parsing  
5. Standardized naming through dictionary mapping  
6. Converted countries to continents  

Special handling was required due to **API rate limits** and **inconsistent geographic naming**.

---

### Dataset Integration
1. Standardized shared columns:
   - Title
   - Department
   - Accession Year
   - Country
   - Continent  
2. Added museum indicator column  
3. Combined datasets using pandas concatenation  
4. Built aggregated views grouped by:
   - Museum + Country
   - Museum + Continent  

---

## Key Findings

### Continent-Level Representation
- Strongly skewed toward **North America and Europe**
- **Asia** shows moderate representation (especially at the MET)
- **Africa, South America, and Oceania** are significantly underrepresented  

<p align="center">
  <img src="figures/continents_bar_chart.png" height="400">
</p>

> South America’s population (~443M) is comparable to North America (~608M), yet representation is disproportionately lower.

---

### Country-Level Representation
- United States dominates both collections
- France is the second most represented country
- Notable non-Western strengths:
  - Egypt (MET)
  - Japan (AIC)
- Several African countries show **zero representation** in the combined dataset

<p align="center">
  <img src="figures/country_bar_chart.png" height="400">
</p>

---

### Combined Dataset Analysis
- Europe and North America dominate despite comparable landmass and population to other continents
- Asia shows moderate but uneven representation
- Africa, South America, and Oceania remain consistently underrepresented  

<p align="center">
  <img src="figures/continent_choropleth.png" height="250" />
  <img src="figures/country_choropleth.png" height="250" />
</p>

---

## Interpretation Notes

Observed imbalance does **not necessarily imply institutional bias**. Contributing factors may include:
- Colonial acquisition history
- Archaeological and trade agreements
- Preservation and survival bias
- Classification differences (art vs. artifact)
- Logistical and legal acquisition constraints

---

## My Contributions
- Designed research question and project scope
- Identified and evaluated museum datasets
- Built MET data cleaning and normalization pipeline
- Researched historical cultures and geographic mappings
- Developed country and continent standardization dictionary
- Created analytical visualizations
- Authored final reporting narrative and presentation materials

---


## Limitations
- Datasets represent only digitally catalogued portions of collections
- MET dataset required sampling due to size constraints
- Some historical cultures do not map cleanly to modern nation-states

---

## Future Work
- Representation trends over time (using accession dates)
- Department-level diversity analysis
- Inclusion of additional U.S. museum datasets
- Acquisition trends correlated with historical events or leadership changes

---

## Technical Stack
- Python
- Pandas
- Regex
- PyCountry-Convert
- GeoPy
- OpenStreetMap API
- Jupyter Notebooks

---

## Post-Mortem 
- Cloud computing would have been preferable for large-scale MET data processing
- Modular `.py` scripts would improve reproducibility over notebook-only workflows
- Fuzzy matching could replace some manual normalization steps
- Choropleth color schemes should prioritize perceptual accuracy over branding

---

## Portfolio Note
The original work was completed as a [collaborative academic project](https://github.com/mollykstark/SIADS-Milestone-1/tree/main).  
This repository highlights **data cleaning strategy, analytical reasoning, and reproducible workflow design** for portfolio purposes.

