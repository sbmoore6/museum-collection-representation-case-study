# Cultural Representation in American Museums

## Project Overview

This project analyzes cultural representation patterns across two major U.S. art museum collections using publicly available collection metadata. The goal was to evaluate how well different regions are represented and identify potential imbalances in collection composition. This study investigates collections from the [Metropolitan Museum of Art](metmuseum.org) and the [Art Institute of Chicago](artic.edu). The analysis evaluates representation at both the country and continent level and compares museum representation against real-world population and landmass distribution.

 This repository is a portfolio companion to the original academic project and demonstrates the data engineering, cleaning, and analytical methodology used.

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

Approximate missing country data after cleaning: ~8.6%
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
 
 ### Country Level Analysis
 - United States dominates both collections
 - France is the second most represented country across both museums
 - Notable non-Western collection concentrations:
   - Egypt (MET)
   - Japan (AIC)
 - Some African countries show zero representation in the combined dataset

