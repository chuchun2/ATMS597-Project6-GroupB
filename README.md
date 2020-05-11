# ATMS 597 Project 6 Group B
### Group Members: Carolina Bieri, Chu-Chun Chen, Jeffrey Thayer

### Overview:
These notebooks use a deep neural network model and two regression techniques (multiple linear and random forest) from the sklearn package and <b>two slowly-evolving factors</b> (Madden-Julian Oscillation, or MJO, and soil moisture) to predict regionally-averaged daily accumulated precipitation from 1996-2019 in southeastern South America (SESA). This region was chosen in part since past work has shown influence by the MJO and soil moisture on precipitation (e.g., Ruscica et al 2014; Grimm 2019). 

### Data sources:
The daily precipitation data is provided by the [Global Precipitation Climatology Project (GPCP)](https://climatedataguide.ucar.edu/climate-data/gpcp-daily-global-precipitation-climatology-project) 
and was averaged over the region from 25-30S/50-55W in SESA. <br>

The MJO index data (OLR+U850+U200) is provided by the [Japan Meteorological Agency](https://ds.data.jma.go.jp/tcc/tcc/products/clisys/mjo/moni_mjo.html), with phase and amplitude used as features for prediction. <br>

Daily soil moisture from the first two ground levels (0-7cm and 7-28cm) averaged over 25-30S/50-55W is provided by [ERA5 reanalysis](https://rda.ucar.edu/datasets/ds630.0/) and used as features. The MJO and ERA5 data are lagged at 5-day intervals from 5-30 days to test the predictability at a broad range of lead times relevant for the two selected slowly-evolving factors. The lagged data are used as features. Year, month, and day are also added as features. 

### Methods:
Data are randomly split 70-30 into training and testing datasets. The accuracy of the neural networks and each regression technique is determined by the root mean squared error (RMSE) or Brier Skill Score (BSS). <br>

We selected <b>multiple linear regression</b> and <b>random forest regression</b> as our baseline models. <br>

For the <b>multiple linear regression</b>, we used the default hyperparameters, and we calculated the RMSE to determine the prediction skill. <br>

For the <b>random forest regression</b>, hyperparameter optimization was performed using RandomizedSearchCV for 300 random hyperparameter combinations. The prediction skill (i.e. RMSE) was then determined after running RandomForestRegressor using the best hyperparameter combination.

For the <b> neural networks (NN) </b>, both regression and classification models were created. The NN regression model was run with a suite of hyperparameters to determine the hyperparameter values which yielded the best prediction. The same was done with the NN classification model. <br>

To address the relatively high RMSEs in the regression task, the NN classification task was attempted. The goal of this task was to predict a class value related to precipitation amount. In this case, the task was prediction of whether precipitation would exceed 0.75 standard deviations or not based on the MJO and soil moisture predictors. 

### References:
[TensorFlow documentation](https://www.tensorflow.org/api_docs/python/tf)
