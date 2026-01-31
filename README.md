# Cultural Representation in American Museums
<p align="center">
  <img src="figures/aic_museum.avif" height="250" />
  <img src="figures/world_map.jpg" height="250" />
</p>

## Project Overview

This project analyzes cultural representation patterns across two major U.S. art museum collections using publicly available collection metadata. The goal was to evaluate how well different regions are represented and identify potential imbalances in collection composition. This study investigates collections from the [Metropolitan Museum of Art](metmuseum.org) and the [Art Institute of Chicago](artic.edu). The analysis evaluates representation at both the country and continent level and compares museum representation against real-world population and landmass distribution.

 This repository is a portfolio companion to the [original academic project](https://github.com/mollykstark/SIADS-Milestone-1/tree/main) and demonstrates the data engineering, cleaning, and analytical methodology used.

 ## Motivation

 Most large art museumds in the United States aim to provide a global array of artwork, but we aimed to see how well rounded that array of artwork truly is. A limited study by Topaz et al. (2019) found that of the approximately 10,000 identifiable artists across 18 U.S. museums, 75.7% were white men. This suggests that the cultural representation in these museums is heavily skewed toward North American and European artists. This project seeks to analyze the collections at the MET and the Art Institute of Chicago to see if there is a similar imbalance there and highlight areas for improvement. 

 ## Objectives

1) Extract and standardize country-of-origin data for each artwork.
2) Analyze representation by country and continent:
   - Per museum
   - Combined
 3) Compare museum representation to:
    - Global population distribution
    - Continental landmass distribution

These objectives were designed to provide insight into collection diversity patterns and potential acquisition bias.

## Data Sources
### [Metropolitan Museum of Art Open Access Dataset](https://github.com/metmuseum/openaccess)
- Partial collection inventory
- ~450,000 catalogued objects
- Key Variables
  - Country
  - Culture
  - Artist Nationality
  - Region
  - Acquisition Date
 - Format: CSV (~303 MB)
### [The Art Institute of Chicago Public API Data](https://github.com/art-institute-of-chicago/api-data/tree/master/json/artworks)
- ~130,000 catalogued artworks
- Key Variables
  - Title
  - Artist Title
  - Place of Origin
  - Acquisition Date
- Format: JSON (~688 MB total)

Both datasets required extensive preprocessing to standardize geographic origin data.

## Methodology
### Data Cleaning: MET Data
Key Steps:
1) Ranked multiple columns by likelihood of containing geographic origin
2) Combined columns using prioritized fallback logic
3) Built country normalization dictionary (alternate names, demonyms)
4) Applied regex cleaning for punctuation and noise removal
4) Manual review for unmapped entries
5) Converted country to continent using pycountry-convert

Approximate missing country data after cleaning was ~8.6%

Due to file size constraints, a random sample of 150,000 rows was used for analysis.

### Data Cleaning: AIC Data
Key Steps:
1) Removed rows missing location data (~7% removed)
2) Matched known country values directly
3) Converted non-country locations using geolocation API (OpenStreetMap via geopy)
4) Extracted country names using regex parsing
5) Standardized naming via dictionary mapping
6) Converted country to continent

Special handling was required due to API rate limits and inconsistent geographic naming.

### Dataset Integration
1) Standardized shared columns:
   - Title
   - Department
   - Accession Year
   - Country
   - Continent
2) Added museum indicator column
3) Combined datasets using pandas vertical concatenation
4) Built aggregated datasets grouped by:
   - Museum + Country
   - Museum + Continent
  
## Key Findings
### Continent Level Analysis
- Heavily skewed toward North America and Europe
- Asia shows moderate representation (particularly at the MET)
- Africa, South America, and Oceania are significantly underrepresented
  - South America’s population (South America ~443M vs North America ~608M) suggests representation should be closer than observed.

<p align="center">
  <img src="figures/continents_vis_combo.png" height="400">
</p>
 
 ### Country Level Analysis
 - United States dominates both collections
 - France is the second most represented country across both museums
 - Notable non-Western collection concentrations:
   - Egypt (MET)
   - Japan (AIC)
 - Some African countries show zero representation in the combined dataset

<p align="center">
  <img src="figures/country_vis_combo.png" height="400">
</p>

### Combined Datasets Analysis
- Europe and North America dominate representation despite similar landmass/population to other continents
- Portions of Asia are moderately represented
- Africa, South America, and Oceania show disproportionately low representation
  - Oceania's low representation may be partially explained by lower land mass and population
<p align="center">
  <img src="figures/continent_choropleth.png" height="250" />
  <img src="figures/country_choropleth.png" height="250" />
</p>

### Interpretation Considerations
Representation imbalance does not necessarily imply institutional bias but may be influenced by:
- Archaeological and trade agreements between countries
- Survival and preservation bias
- Acquisition logisitics
- Colonialism and acquisitions history
- Art vs artifact bias (Some objects may be classified artifact rather than art)

## Limitations
- Datasets were only the digitally documented portions of their collections and not representative of the full collections
- MET data required sampling due to data size and project restrictions
- Some cultural identifiers cannot be mapped cleanly to modern country boundaries

## Future Work
- Representation trends over time using accession date
- Department-level cultural diversity analysis
- Inclusion of additional U.S. museum datasets
- Acquisition trend analysis tied to historical events or leadership changes

## Technical Stack
- Python
- Pandas
- Regex
- PyCountry-Convert
- GeoPy
- OpenStreetMap API
- Jupyter Notebooks

## My Contributions
- Designed project concept and research direction
- Identified and evaluated data sources
- Built MET data cleaning and normalization notebook
- Extensively researched historic cultures and countries to match with current countries and continents
- Developed geographic standardization dictionary
- Created exploratory visualizations
- Built reporting narrative and final presentation materials

## Post Mortem
- Excel was used to sample the MET dataset due to its size, but looking back I would have used a hosting website and possibly utilized SQL to handle the large dataset
- .py should have been used to streamline operations and make the results more reproducable
- Fuzzymatch would have been a cleaner option to handle some of the spelling and format country name discrepencies

## Portfolio Note
The original project was completed as a [collaborative academic project](https://github.com/mollykstark/SIADS-Milestone-1/tree/main). This repository is intended to demonstrate data cleaning methodology, analytical reasoning, and reproducible workflow design.

