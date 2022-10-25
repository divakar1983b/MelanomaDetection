# Melanoma Detection Model 
> Melanoma is a type of cancer that can be deadly if not detected early. It accounts for 75% of skin cancer deaths. A solution that can evaluate images and alert dermatologists about the presence of melanoma has the potential to reduce a lot of manual effort needed in diagnosis.  
> The dataset consists of 2357 images of malignant and benign oncological diseases, which were formed from the International Skin Imaging Collaboration (ISIC). 

## The data set contains the following diseases:
* Actinic keratosis
* Basal cell carcinoma
* Dermatofibroma
* Melanoma
* Nevus
* Pigmented benign keratosis
* Seborrheic keratosis
* Squamous cell carcinoma
* Vascular lesion
> 
>

*![Book logo](/pricing1.jpg)

## Table of Contents
* [Objective](#Objective)
* [Data Exploration](#Data_Exploration)
* [MultiColinearity](#Multicolinearity)
* [Model Estimate](#Model_Estimate)
* [Conclusion](#Conclusion)

<!-- You can include any other section that is pertinent to your problem -->

## Objective
- To build a CNN based model which can accurately detect melanoma
- Model shall be used by dermatologists to alert them about the presence of melanoma and reduce the manual effort needed in diagnosis.
- 
<!-- You don't have to answer all the questions - just the ones relevant to your project. -->

## Data_Exploration
-  Variables
    -   The dataset "train.csv" has 80 features with 1460 records for predicting "SalePrice" of an Australian house. 
    -   "SalePrice" is our target variable for which the regression model needs to be built
    -   On going through the data it is found that some of the variables such as "Alley, PoolQC, Fence, MiscFeatures" are having most of the values as NAN. Hence can be dropped. 
    -   Variables such as "YearBuilt, YearRemodAdd, GarageYrBuilt" are transformed to respective ages from time of sale using formulas such as  "YrSold-YrBuilt, YrSold-YearRemodAdd, YrSold-GarageYrBuilt" resp. and the year variables are dropped. 
    -   Unimportant variables such as "ID" are also dropped
-   Continuous Variables
    -   Histogram of continuous variable gives us insight of some of the insignificant variables such as "ScreenPorch, PoolArea, MiscVal, MasVnrArea, LowQualFinSF, EnclosedPorch, BsmtFinSF2, 3SsnPorch" which can be dropped
*![Book logo](/cont1.PNG)
*![Book logo](/cont2.PNG)
*![Book logo](/cont3.PNG)
-   Categorical Variables
    -   Countplot of categorical variable gives us insight of some of the insignificant categorical variables such as "BsmtHalfBath, Utlities, Street, RoofMatl, Landslope, LandContour, Heating, GarageQual, GarageCond, Functional, Electrical, Condition2, Condition1, CentralAir, BsmtFinType2,BsmtCond,KitchenAbvGr, PavedDrive, ExternalCond" which can be dropped.
*![Book logo](/cat1.PNG)
*![Book logo](/cat2.PNG)
*![Book logo](/cat3.PNG)
*![Book logo](/cat4.PNG)
*![Book logo](/cat5.PNG)
*![Book logo](/cat6.PNG)
*![Book logo](/cat7.PNG)
-  Zones & Subclasses
    -   On going through the data_description and data we can understand that the houses are majorly categorized according to zones. 
    -   "MSZoning" variable contains the zones of each house as "RL, RM, RH, FV, C(all)". 
    -   The distribution of the house sold reveals that almost "79% of house sold are from "RL" Zone, followed by "15%" in "RM" Zone and 4% in "FV"zone and minor % in RH and C(all) zones.
    -   The Houses sold in each zone can be further sub classified into 1-Story newer, 1-Story older, 2-Story newer, 2-Story older...etc which is captured in variable "MSSubClass" with values 20 to 190 each representing a particular class.
    -   The distribution of House sold in each zone based on sub class reveals following: 
    -   In RL Zone: 44% of the houses are 1-Story newer, 24% are 2-Story newer, 8% are 1.5 Story finished and minor % in other classes
    -   In RM Zone: 23% are 1.5 Storey finished, 15% of old 1Storey and 2 Storey, 10% of Planned unit and minor % in other classes
    -   In FV Zone: 38% are 2 Storey Newer, 34% Planned unit, 20% 1Storey newer and 8% 1Storey PUD

*![Book logo](/zone1.PNG)
*![Book logo](/zone2.PNG)
-  Outliers   
    -   The Box plot distribution of "Saleprice" based on houses sold in different zones and Subclasses reveals the outliers in the data which are removed for better model prediction.

*![Book logo](/mssub1.PNG)
*![Book logo](/mssub2.PNG)
*![Book logo](/mssub3.PNG) 


## Multicolinearity
- To understand the multicollinearity amoung the different features, we shall plot the heat map between the variables, as well as use the variance_inflation_factor from statsmodels

*![Book logo](/corr1.PNG)
*![Book logo](/corr2.PNG)
*![Book logo](/vif1.PNG)
*![Book logo](/vif2.PNG)
    
- From the heatmap we can see many highly correlating features 
- Such Correlating Features are procedurally analysed through VIF function and dropped one by one to optimum number.

## Model_Estimate
- Once the Multicollinear features are removed to possible level using Correlation plot and vif, we move to LinearRegression model & RFE to eliminate further on the low priority features.
- Since the number of features are large we will not be able to continue with LR model & RFE techiniques to achieve the most suitable model with minimal overfitting and multicollinearity.
- Hence we switch to Ridge regresion model or Lasso regression model to easily find the best features and coefficients for our model.
- For building the Housing price model, the data were classfied based on Zones and each zone were modelled separetly.
    - The Models for RL, RM, RH and FV Zones were estimated separately and the outcomes are as follows

- Ridge Train & Test Trends:
*![Book logo](/ridgetr2.PNG)
*![Book logo](/ridgetst3.PNG)

- Ridge Train & Test Residuals:
- *![Book logo](/ridgetr1.PNG)
*![Book logo](/ridgetst1.PNG)
*![Book logo](/ridgetst2.PNG)

- Lasso Train & Test Trends:
*![Book logo](/lassotr2.PNG)
*![Book logo](/lassotst3.PNG)
     
- Lasso Train & Test Residuals:
*![Book logo](/lassotr1.PNG)
*![Book logo](/lassotst1.PNG)
*![Book logo](/lassotst2.PNG)
  
## Conclusion
   -   From the above models and prediction we can see that 
        - The "RL" Zone model and "FV" Zone model can predict better
        - The "RM" Zone model test score is comparatively less than train score. So predictions might be little unreliable.
        - The "RH" Zone model is poor at the train and test.
   -   "RL" Model top 5 predictors by Lasso
        - Stone- "Exterior Covering on house"   : 0.292
        - NoRidge- "Northridge locality"        : 0.2236
        - Gambrel- "Gabrel roof"                : 0.1635
        - LotArea- "Lot size in sq.ft"          : 0.1625
        - 1.5Unf- "1.5 story Unfinished"        : -0.16238
  -    "FV" Model top 5 predictors by Lasso
        - LotArea- "Lot size in sq.ft"          : 0.48728
        - BsmtFinSF1- "Type1 Finished sq.ft"    : 0.18799
        - Rec- "Avg.Rating of Basement finish"  :-0.17729
        - 2SPUD- "2Storey PUD"                  : -.17687
        - Builtin-"Garage location"             : 0.1554
<!-- You don't have to answer all the questions - just the ones relevant to your project. -->
