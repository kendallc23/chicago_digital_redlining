# From Red Zones to Dead Zones: Analyzing Fiber Broadband Access in Chicago (Formal write up coming soon!)

> ⚠️ **Important Note**: The web scraping component of this project is now deprecated as AT&T seems to have updated their website with enhanced security measures. The scraping code is preserved for reference and educational purposes only. Previously scraped data (from Summer 2024) is provided and may be used with the notebooks for spatial autocorrelation and GWR/GWLR.

For more context on the history of racialized redlining in the United States, check out the [Mapping Inequality Project](https://dsl.richmond.edu/panorama/redlining/introduction).

## Research Questions

1. Do locational inequalities in access to fixed fiber optic broadband service
from AT&T, as reported by the FCC, follow historical patterns of redlining
in Chicago? Do the redlining boundaries have a significant relationship to the
spatial distribution of AT&T fibre service availability; if so, where does this
occur?

2. Within the study area, are there discrepancies in the relationship between
redlining and data reported by the FCC and data scraped from the
AT&T website?

## Data Sources

The analysis combines several key datasets:

- **FCC National Broadband Map Data**: Provider-specific fixed broadband availability data, updated December 31, 2023
- **AT&T Website Data**: Historical fiber availability data scraped from AT&T's broadband service checker tool
  - **National Address Database**: The web scraper input data consisted addresses, selected through stratified random sampling at the census block group
level.
- **HOLC Redlining Maps**: Historical neighborhood classifications from the Mapping Inequality Project
- **Census Data**: Demographic and boundary data from the 2018-2022 American Community Survey
- **Urban Displacement Project Data**: Gentrification and displacement risk indicators

## Methodology

The analysis employs the following spatial analysis techniques:

1. **Spatial Autocorrelation Analysis**
   - Global and local Moran's I statistics to identify clusters of high/low fiber availability
   - Gaussian kernel function with adaptive bandwidth for spatial weights

2. **Geographically Weighted Regression**
   - Analysis of relationships between redlining and fiber availability
   - Controls for demographic factors, broadband adoption rates, and gentrification
   - Different levels of granularity across data sources (individual addresses in the scraped data and census block groups in the FCC data)
     necessitate different regression models
     - Geographically weighted regression (GWR): designed for continuous dependent variables such as the proportion of locations in a census block group eligable for AT&T Fiber 
     - Grographically weighted logistic regression (GWLR): designed for binary dependent variables such as individual addresses that may or may not be eligable for AT&T Fiber
       
   - Note: It was necessary to aggregate the FCC data and census-block level controlsto the HOLC neighborhood level, before conducting GWR. geometries, I
     replicate the approach introduced by [Skinner et al. (2023)](https://doi.org/10.1177/08959048231174882).

## Results Summary

Key findings include:
- Historically redlined areas are observed to have fewer locations that are eligible for AT&T fibre, but the potential
  role of gentrification suggests a more complex relationship.
- Regression results are inconsistent across data sources (scraped vs FCC):
  - GWR results suggest a broadly negative relationship between an area having been redlined and the proportion of locations in that area
with access to AT&T fiber. On average, moving from a historically non-redlined area to a redlined area is
associated with a percentage point decrease in the proportion of locations eligible for AT&T fibre service of 8.20 (average coefficient of 0.082), holding all other variables
constant.
  - The redlining indicator variable is not significant for any location in the GWLR results.
- The current proportion of Black residents in a given area is significantly associated with lower odds of AT&T Fiber availability across both datasets.
  -  These findings support the conclusions drawn by [Markley and Holloway (2024)](https://www.tandfonline.com/doi/full/10.1080/24694452.2024.2350993), which state
     that while HOLC grades were initially strong predictors of disparities in property
     values, modern racial demographics are now much more strongly correlated with
     these disparities.



  
