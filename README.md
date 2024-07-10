# Overview

## Project goal

Develop a model that predicts asking prices of houses in Madrid, Barcelona, and Valencia, leveraging open-source data from Idealista and additional external data sets.


## Authors
- Maya Grape
- Teresa Villa de Freitas
- Carlotta Hanten
- Mohamed Amine Bakkoury
- Sami Boustani


## Project structure

The key steps of the project are implemented in separate notebooks. 
The key steps include EDA, data cleaning, feature engineering, and model training and prediction.
After each key step, the resulting data is saved to the respective folder.

- **Files included in main directory of project:**
  - README: This file, with the goal to give an overview of the project
  - pyproject.toml: Dependencies required to run project

- **Files included in directory "data":**
  - 1_raw_idealista_data: Raw data sets as received from Idealista and downloaded from the R package
  - 2_raw_idealista_data_incl_polygon: Idealista data sets in their raw version, but merged for each city
  - 3_external_data: All external data sets that were used for feature engineering
  - 4_data_cleaned: Idealista data after implementation of data cleaning
  - 5_cleaned_and_feature_engineering: Cleaned Idealista data, enriched with engineered features

- **Files included in directory "notebooks":**
  - Notebook 1: Merging of raw Idealista sales data with raw Idealista data on polygons
  - Notebook 2: Exploratory data analysis (EDA) of raw Idealista data incl. polygons
  - Notebook 3.1: Generation of zip codes of closest metro station using external API
  - Notebook 3.2: Data cleaning, categorical encoding and merging of zip codes (to enable feature engineering)
  - Notebooks 4: Feature engineering using both the Idealista data and external datasets
  - Notebook 5.1: Choice of model and hyperparameters, optimization of transformation of target variable PRICE
  - Notebooks 5.2-5.7: Running the optimized base model with each engineered feature seperately, incl. creation of spatial lag
  - Notebook 5.8: Final model with features that improved performance

## Deep dive into feature engineering of census data

### 1. Collect Data from INE

#### API Collection

- Use the INE API to fetch demographic and economic data at the census section level.

#### Web Scraping

- For data not available through the API, employ web scraping techniques using libraries like BeautifulSoup and requests.
- Ensure compliance with INE's terms of service and scraping policies.

### 2. Process the Data

- Clean and preprocess the data to handle missing values, standardize formats, and correct any inconsistencies.
- Transform the data into a suitable format for further analysis and integration.

### 3. Use QGIS Software for Coordinates

- Utilize QGIS software to obtain geographic coordinates for census section centroids.
- Import the census section shapefile into QGIS.
- Use QGIS tools to calculate the centroids of each census section and export the results.

### 4. Map Post Codes to Closest Centroid

- Use the geopy library to map postal codes to the nearest census section centroid.
- Calculate distances between postal codes and centroids and assign the closest centroid to each postal code.

### 5. Join INE Data with Real Estate Data

- Integrate the INE data with real estate information using postal codes as the key.
- Ensure the data from both sources are compatible and align correctly.

The final step of the project is implemented in the attached Python script (`final_join.py`). This script performs the data merging and final adjustments needed to combine the INE and real estate datasets effectively.