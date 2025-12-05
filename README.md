# Analysis of Street Tree Data Sets — 2015 to 2024

This repository contains data, analytic code, and findings that support portions of the article **“New York’s Trees Are Smaller Than San Francisco’s,”** published Month Date, Year. Please read that article, which provides essential context and reporting, before proceeding.

---

## Data

This analysis uses two public spreadsheets that document street trees in New York City and San Francisco.

### Sources

#### **NYC Open Data**
- **nyc_trees.csv**  
  Raw data from the *2015 NYC Street Tree Census*.  
  Includes species names, trunk diameter, coordinates, and planting information.

#### **DataSF**
- **sf_trees.csv**  
  Raw data from the *San Francisco Street Tree List*.  
  Includes species information, trunk diameter, maintenance notes, and coordinates.

### Relevant Columns

Each spreadsheet contains, among others, the following columns used in this analysis:

- **species** — common name of the tree species (standardized from original columns)  
- **dbh** — diameter at breast height, used to estimate tree size  
- **city** — label indicating whether the tree is from NYC or SF  

---

## Methodology

The notebook **tree_size_analysis.ipynb** performs the following steps:

### **Part 1: Data Loading, Cleaning, and Harmonization**
- Loaded both datasets using `pandas`.  
- Renamed columns (`spc_common` → `species`, `tree_dbh` → `dbh` for NYC; `qSpecies` → `species`, `DBH` → `dbh` for SF).  
- Converted `dbh` values to numeric and removed invalid entries.  
- Added a `city` column to identify each dataset’s origin.  
- Concatenated both datasets into a single table for side-by-side comparison.

### **Part 2: Tree Size Classification and Comparison**
- Created a new column, `size_class`, assigning trees to **small**, **medium**, or **large** categories based on diameter.  
- Used `groupby` to count trees by size within each city.  
- Calculated total tree counts per city and merged them using `pandas.merge` (similar to Excel’s VLOOKUP).  
- Computed percentages showing how each size class contributes to each city’s overall tree population.  
- Produced a final summary comparing NYC and SF using shared size categories.

---

## Outputs

The notebook generates the following output file:

- **output/tree_size_summary.csv**  
  Contains the final counts and percentages of tree size classes for each city.  
  Columns include:
  - `city`  
  - `size_class`  
  - `count`  
  - `total_trees`  
  - `percent`

---
