# Building and occupant characteristics as predictors of temperature-related health hazards in American homes

[Arfa Aijazi](https://github.com/anaijazi), [Stefano Schiavon](https://github.com/stefanoschiavon), and [Duncan Callaway](https://github.com/duncancallaway)

## Background
Many cities and regions are making significant investments towards planning for extreme temperature and in particular extreme heat. Heat vulnerability indices (HVI) are used to track spatial variation in extreme temperature risk to target mitigation interventions. Most HVI focus on demographic characteristics, which generally relate to vulnerability, and lack information about the building stock, which mediate the occupant´s exposure to extreme temperatures. In this study, we use the Energy Information Administration´s (EIA) Residential Energy Consumption Survey (RECS) to estimate prevalence of temperature-related illness in the United States and develop machine learning models using climate, demographic, and building characteristics to predict them. Temperature-related illness affects approximately 2 million households annually, around 1% of the total population. The models we develop predict temperature-related illness with up to 85% accuracy. The most important feature is energy insecurity, which describes the household´s ability to maintain and operate heating, ventilation, and air conditioning (HVAC) systems. Our results offer guidance for municipalities to improve both 1) data collection, enabling them to better identify at-risk households and 2) interventions, such as by targeting factors that could mitigate temperature-related health hazards. 

## Code
This repository contains all the data files and source code to reproduce the forthcoming paper. All code is written in R and follows the `{tidyverse}` syntax. 

The project directory is structured as follows:

```
+-- doc
    +-- 20240305_Draft2 # manuscript file
    +-- figures
        +-- ...  # final versions of figures that appear in the manuscript
+-- code
    +-- RECSThermalMorbidity.Rproj # RStudio project file
    +-- 01_DataDownload.Rmd # Downloads the 2015 and 2020 RECS data set, prepares variables for merging, and selects subset of variables 
    +-- 02_DataExploration.Rmd # Explores correlation between subset of variables
    +-- 03_DataProcessing.Rmd # Checks for near-zero variance, highly correlated variables, and linear combinations
    +-- 04_PopulationEstimate.Rmd # calculates population estimates based on sample weights
    +-- 05_MachineLearning_x.Rmd # trains machine learning algorithms from the pre-processed output of 03_DataProcessing.Rmd. Divided the main for loop into 10 files in order to manually spread out computation over 10 machines
    +-- 06_ResultsAnalysis.Rmd # plots results of machine learning
    +-- 07_VariableImportance.Rmd # calculates variable importance for best machine learning algorithm and class imbalance handling scheme combination. Requires running concurrently with 06_ResultsAnalysis.Rmd in order to identify best MLMethod and imbalance scheme and to complete plot
    +-- 08_ResultsPlot.Rmd # combines plots from 06_ResultsAnalysis.Rmd and 07_VariableImportance.Rmd
    +-- DMwR_0.4.1.tar # archived package downloaded from CRAN which contains functions for SMOTE
+-- data
    +-- recs2015_public_v4.csv # 2015 RECS microdata, downloaded from eia.gov
    +-- recs2020_public_v5.csv # 2020 RECS microdata, downloaded from eia.gov
    +-- recs_subset.csv # merged subset of RECS microdate, output from '01_DataDownload.Rmd'
    +-- recs_standardized.csv # output from '03_DataProcessing.Rmd'
    +-- variables.csv # input variables under consideration
    +-- results_compiled_x.csv # output of '05_MachineLearning_x.Rmd'
    +-- plot_top.rdata # output of '06_ResultsAnalysis.Rmd'
    +-- varImp_compiled.csv # output of '07_VariableImportance.Rmd'
    +-- plot_varImp.rdata # output of '07_VariableImportance.Rmd'
+-- references
    +-- recs2015_public_codebook_v4.xlsx
    +-- recs2020_public_codebook_v5.xlsx
    +-- thresh15.xlsx
    +-- thresh20.xlsx
    +-- materials
        +-- calc_thermalMass.xlsx  # final versions of figures that appear in the manuscript
        +-- Roof.AsphaltShingle.pdf
        +-- Roof.CeramicClayTile.pdf
        +-- Roof.ConcreteTile.pdf
        +-- Roof.Metal.pdf
        +-- Roof.WoodShingleShake.pdf
        +-- Wall.Brick.pdf
        +-- Wall.ConcreteBlock.pdf
        +-- Wall.Wood.pdf
```
Knitting the R markdown files in the 'code' directory in sequence is important to generate all necessary input parameters. 

1. '01_DataDownload.Rmd'
2. '02_DataExploration.Rmd'
3. '03_DataProcessing.Rmd'
4. '04_PopulationEstimate.Rmd'
5. '05_MachineLearning_x.Rmd'
6. '06_ResultsAnalysis.Rmd'
7. '07_VariableImportance.Rmd'
8. '08_ResultsPlot.Rmd'

## Acknowledgements
At the time of the study, Arfa Aijazi was supported by a Doctoral Completion Fellowship through the Graduate Division at the University of California, Berkeley. This research was also in part funded by the Center for the Built Environment (CBE) at University of California, Berkeley with which some of the authors are affiliated. This research used the Savio computational cluster resource provided by the Berkeley Research Computing program at the University of California, Berkeley (supported by the UC Berkeley Chancellor, Vice Chancellor for Research, and Chief Information Officer). The authors also thank Dr. Matias Quintana with the Singapore-ETH Center for his assistance with developing machine learning modeling methodology. We also thank William McNary with the Energy Information Administration (EIA) for providing context into the RECS survey design and implementation. 