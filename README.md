
# Determining 311 usage levels with socio-economic and spatial features

# Capstone Project for the Center of Urban Science and Progress at New York University in Collaboration with NYC 311

## Contributors:

###- Diego Garzon (http://dfgarzon.weebly.com/)

###- Juan Pablo Mora (https://github.com/jpmora69)

###- Nikhil Kishore (http://www.nikhilsprofile.com) - Web Developer

###-Yanchao Wu (https://github.com/yanchao1992)

##Project Supervisor:

###Stanislav Sobolevsky, PhD. (http://cusp.nyu.edu/people/stanislav-sobolevsky/)





# About our project:


311 is the defined support center created by the New York City government with the objective of
attending all nonemergency
inquiries and service requests from the general public to the local
administration; by definition, 311 has a large open database starting from 2010 that consolidates
all received citizen complaints regarding topics that range from housing, noise and transportation
to public health and services related to various local government departments, among many
others.


The main objective of our project is to generate an analytical model that can link several data sources containing
socioeconomic and demographic features of the population that resides within New York City and
asses their correlations with the number of service requests received by 311 in a specific period of
time to identify certain kinds of user profiles at defined geographical areas.


The expectation is that the model developed is not only limited to define these correlations, but
that can be a useful tool to also try to generate projections and estimations on the propensity and
number of service requests 311 is going to receive in the future based on those population
features, in a way to both identify population changes in the City, and also to validate if certain
demographic groups are being unattended or have lower probabilities of using the service in order
to guarantee a global reach of the service provided.


# Why this repo exists


This is the repo for our Machine Learning final group project at CUSP, NYU. It serves as a platform of code version control, code exchange, 
code safehouse and reproducibility.

DATASETS

Multiple data sources have been used throughout the project. Data sources used includes:


 311 Service Request Data (2014) (open source)


 ACS Demographics Data (2014) (open source)


 LEHD Data (open Source) (2014)


pluto data shape file for census tract


pluto Data shapefile NTA level (neighborhood level) (version 16v1)

3. VARIABLES FOR THE ANALYSIS:


Demographic Variables:


Age groups: population under 18, between 18 and 34, between 35 and 64, more than 65.


Population by Race: white, black, hispanic, asian, others


Family Households and non family households


Education Level: high school or less, bachelors, masters, PhDs


Owner and tenants


Mean of transportation: car, public, motorcycle, others


Household income: less than 40,000; between 40,000 and 75,000; and 75,000 and above


House value: less than 100,000; from 100,000 to 500,000; 500,000 and more.



Local Variables:

Median House Value, median age, median rent, median income, normalized cars, building density, percentage of commercial area, percentage of retail area, percentage of residential area, inbound commute density, population density, percentage of tenant population. 


 
4. FILES



The main repository of the project contains 2 folders (datasets and Outputs) and three ipython notebooks (LEHD_data_aggregation, Step 1 and Step 2)  where the calculations were performed. 



The folder datasets, contains all the data aggregations that are used in the calculations, and in the webtool, for the analysis and visualization of the results.


Datasets used in LEHD_data_aggregation:


'datasets/ny_od_main_JT00_2014.csv' from LEHD data, containing origin and destination census blocks for workers living inside New York State


'datasets/ny_od_aux_JT00_2014.csv' from LEHD data, containing origin and destination census blocks for workers living outside New York State


datasets/demographics_CT_NYC_residents.csv a compiled Data Frame with the selected demographic variables downloaded from 2014 American Community Survey for census tracts inside New York State


datasets/demographics_CT_outNY.csv  a compiled Data Frame with the selected demographic variables downloaded from 2014 American Community Survey for census tracts outside New York State


Datasets used in STEP 1: 


'datasets/demographics_nta_NYC_workers_compiled.csv' a compiled list with the selected demographic variables aggregated by NTA (Neighborhood Tabulation areas) as estimated using LEHD data on LEHD_data_aggregation


'datasets/Call by type without normalization - NTA level.csv' the number of 311 service requests for each type of request for the 2014 database


Datasets used in STEP 2:


'datasets/nta_census_shapefile/NTA_json.geojson' geojson file with the borders of each NTA in New York City


'datasets/nta_census_shapefile/neighborhood_nta_census.shp' folder containing the shapefile with the borders of each NTA in New York City, from the department of planning 


'datasets/location_features2.csv' a compiled Data Frame with the selected local variables downloaded from PLUTO data and ACS


The folder outputs, contains the results from the calculations that are later used on the  analysis and visualization of the results.


Outputs obtained in LEHD_data_aggregation:


'outputs/LEHD_analysis/LEHD_by_CT.csv' ‘outputs/LEHD_analysis/demographics_CT_origins.csv' 


'outputs/LEHD_analysis/demographics_CT_NYC_workers.csv' a compiled Data Frame with the values of the selected demographic variables as estimated for the working population using LEHD data, aggregated at the census tract level.

Outputs obtained in Step 1:


'outputs/table_1.csv' Data Frame containing the R squared values for each regression performed in step 1 (by type of request, and by group of variables)


'outputs/step1_coefficients_complete_table.csv' Coefficients from the regressions obtained in the first step (by type of request, and by each demographic variable)


'outputs/coefficients_std_complete_table.csv' Standard deviations for the coefficients from the regressions obtained in the first step (by type of request, and by each demographic variable)


'outputs/step1_intercepts.csv' Table with the intercepts from the regressions obtained in the first step (by type of request, and by 
each demographic variable)


'outputs/step1_avg_rsq.csv' average R squared value for every type of request in step 1


'outputs/predicted_values.csv' predicted values for types of request in each NTA, with R squared value bigger than 0.2,  by the regressions in step 1


‘outputs/observed_values.csv' observed values for types of request in each NTA, with R squared value bigger than 0.2, by the regressions in step 1.


Outputs obtained in Step 2:


'outputs/error_table.csv' table with errors between predicted values in step 1 and observed values for each type of request


'outputs/phase2_spatial_autocorrelation.csv' Moran’s I spatial autocorrelation values for the relative error between the observed values and the predicted values for step 1


'outputs/phase2_coefficients.csv' regression coefficients for each local variables as obtained by the second step


‘outputs/phase2_predicted.csv' predicted values for types of request in each NTA, with R squared value bigger than 0.2, by the regressions in step 2


‘outputs/phase2_regressions.csv' average R squared and best Lasso coefficient for the cross validation in step 2

## INSTRUCTIONS TO RUN THE PROGRAMS
 
In order to reproduce the analytical experiment, the three notebooks should be run in sequence:

### LEHD_data_analysis:


The main purpose of this notebook, is to get the approximate statistics on certain demographic features of New York City workers by Census tracts, based on their residence location.
LEHD dataset provides information about the number of workers comming from a given census block to each census block in New York City. Specifically, the datasets used in our analysis are: 'ny_od_main_JT00_2014.csv' (information about workers in New YorkThe State with residence in New York State) and 'ny_od_aux_JT00_2014.csv' (information about workers in New York State with residence outside the State).


As a first step, an exploratory analysis is performed. The goal of this exploration is to find from which states and counties the working population is comming to work in NYC everyday. Using the geocode of this counties, socio-demographic features are downloaded from Social Explorer (Census Data) and then merged again with the LEHD data set.
Each pair of census blocks (residence CB and workplace CB) has the information about the number of workers. This data is aggregated by census tract and then a weighted sum is performed for each feature and each census block.
Let  w _ geo be the geocode of the working place and  h _ geo  be the geocode of the residence place. The goal is to get an approximate of each of the demographic features for each  w_ geo.


### Step 1


This notebook will focus on the analytical part of the 311 demographics analysis: that is, multilinear regressions between resident and working population socio-demographic attributes and the number of 311 calls by type per capita, at the NTA level will be performed and analyzed


The first step of this process, is to perform linear regression with the demographical features as variables and the types of 311 services requests as dependant variables.
Outcomes and variables of this notebook:


1) regresions_filtered is an internal dictionary: the types of requests are the keys, and the group of variables which after the cross validation got an R square value greater than 0.2 are elements of each key.


2) outcomes/table_1.csv is a csv fail, containing the type of service request, the group of variables and the R square value of the OLS regression after the cross validation


3)results_phase1 is an internal dictionary. The structure is: results_phase1[type_of_request][group_of_variables] and contains the R square value of each regression as well as a table with the values of the coefficients of the regression associated with each variable under the category (coefficients under the 'mean' column and the standard deviation, obtained from the width of the confidence intervals, under the std_dv column)


4) outcomes/user_profiles.csv and outcomes/user_profiles_coefficients.csv contain a table each with the type of requests as index and the group of complain as column. The value on each cell represents the variable associated with the highest coefficient on the OLS regression (in the file user_profiles.csv) and the value of this coefficient (in the file user_profiles_coefficients.csv )


5) OLS_regressions is an internal dictionary. It follows the structure OLS_regressions[type_of_request][group_of_variables]['total_var' or 'prediction']. 'total_var' contains the standard deviation of the group of variables (sum of the stand. dev from the results_phase1 dictionary), while 'prediction' containing a table comparing the observed values and the predicted values for the number of requests for each type of request, following the regression values obtained for each group of variables.


6) At the end of the notebook, avg_predicionts_dict is a dictionary that averages the different predictions for each type of request. avg_predicionts_dict[type_of_request] gives access to a table with the observed and averaged predicted number of requests for each NTA.


7) In order to provide a better way to understand and to communicate the findings of step 6, outputs/predicted_values.csv and outputs/observed_values.csv are two files that contain the predicted number of requests for each type as predicted by our model, and the observed values.


### Step 2


After having obtained a prediction for the number of requests for each type of 311 service request, we are going to try calculate the relative error for the predictions and find clusters of similar errors. The goal of cluster the errors is to detect areas where the demographic features are not enough to predict the number of 311 requests and, instead, there are more features (about the neighborhood itself instead of its population) that affect the volume of 311 requests.
This notebook contain 4 analysis:


1) the error is calculated for each type of complain


2) We analyze first a specific case for spatial distribution of the error: service requests about 'Noise' and its spatial autocorrelation (using the Moran's I).


3) Then, we repeat the process for each type of requests, we filter for those types of requests that are statistically significant and we take the one with the highest Moran's I (that means, with the highest spatial autocorrelation) for analysis.


OUTPUT: outputs/phase2_spatial_autocorrelation.csv stores the Moran's I for those types of requests with statistically significant Moran's I value for further analysis at the end of the notebook


4) Feature selection and regression is performed for those types of complains with Moran's I values greater than 0.2


OUTPUTS:


outputs/phase2_coefficients.csv with the coefficients obtained after running the LASSO over the features with high spatial autocorrelation


outputs/phase2_predicted.csv with the predicted number of calls for the complains after running the LASSO over the features with high spatial autocorrelation



Some python libraries used in the notebooks are:


Pandas
Numpy 
sklearn
matplotlib
Statsmodels
Seaborn
geopandas
mplleaflet
pysal


## Web Application Instruction

Access to the Web Application: nk1877.github.io/Capstone/prototype


