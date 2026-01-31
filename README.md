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

