# Melanoma Detection Model 
> Melanoma is a type of cancer that can be deadly if not detected early. It accounts for 75% of skin cancer deaths.  

<img src="mela.jpg" width="200" height="200">

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
<!-- You don't have to answer all the questions - just the ones relevant to your project. -->

## Data_Exploration
-  The dataset consists of 2357 images of malignant and benign oncological diseases, which were formed from the International Skin Imaging Collaboration (ISIC).

### The data set contains the following diseases:
* Actinic keratosis
* Basal cell carcinoma
* Dermatofibroma
* Melanoma
* Nevus
* Pigmented benign keratosis
* Seborrheic keratosis
* Squamous cell carcinoma
* Vascular lesion
<img src="skin_disease.PNG" width="600" height="600">

## Data Imbalance
- **Class Distribution:**
>By calculating the % of each class in the training dataset, we can see that "Seborrheic keratosis" has least numbers, followed by "dermatofibroma", "actinic >keratosis", "vasular lesion","squamous cell carcinoma", "nevus", "basal cell carcinoma", "melanoma" and "pigmented benign keratosis".

**Class Domination:**
>Four classes namely Pigmented Benign keratosis, Melanoma, Basal Cell carcinoma and Nevus occupy nearly 72.9% of the training dataset

- actinic keratosis 		    : 5.13
- basal cell carcinoma 		    : 17.24
- dermatofibroma 		        : 4.30
- melanoma 			            : 19.64
- nevus 				        : 15.46
- pigmented benign keratosis    : 20.65
- seborrheic keratosis 		    : 3.24
- squamous cell carcinoma 	    : 7.92
- vascular lesion 		        : 6.42

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
