![alt text](https://github.com/dylanlee91/DSI-Ames-Housing/blob/main/ga_logo.png?raw=true) 
# General Assembly Data Science Immersive Project 2: Using machine learning to predict sale prices of residential property in Ames, Iowa
## Introduction: What factors are most likely to affect housing prices in the data, and can we make useful predictions with a model?
In this project, data from Ames, Iowa for houses sold between 2006 and 2010 are used to create a model that may explain sale prices in Ames. 
This project is split into 2 notebooks:
Notebook 1 contains an initial visualisation of the data, data cleaning and imputing of missing values, an exploratory data analysis and finally feature engineering in preperation for regession.
Notebook 2 contains the regression models used to create the prediction. The models used were ridge regression, lasso regression and elastic net regression. Features were dropped until the 30 features with the largest coefficients on sales price were left.

#### Problem statement
This project is intended to investigate how house sale prices in Ames, Iowa, might be explained by characteristics of houses being sold, and how much new houses entering the property market might expect to be sold for. 

# Data Cleaning Process
The data was first inspecting for missing values which were compared to the data dictionary. Null values which corresponded to a lack of the feature were imputed with 'none' for better processing by the dataframes and regression models. Problematic columns with very few non-0 features were removed from the data set, as well as two outlier houses with a very high sale price and lot size. The numerical data was then visualised to check for correlations, whereupon numerical features with low correlation were not used in the final exported dataset. Similarly, categorical data was plotted on bar plots to check for any categories that could be safely removed. Two part features such as external covering of the house 1 and 2 were combined into a single category before dummy variables were created. A final processed dataset was then exported using all the features marked for investigation.

# Modelling and Methodology
To produce the predictions, 4 regression models were used to evaluate the training data:
- Linear Regression
- Ridge Regression
- Lasso Regression
- Elastic Net Regression

The data was processed in the following steps: 

The data was run through each regression type to produce coefficients
The coefficients were sorted in order of magnitude of effect
Features were eliminated until 75 remained
A further round of regression and ordering by coefficients was performed
Features were eliminated until 30 remained
These features were used to predict sale prices in the Kaggle test data set, using an Elastic net model fitted on the training data and the 30 features.

***
#### Kaggle Scores
The Kaggle score of each submission was approximately 32k, matching previous observations in the second stage of regression where the RMSE of each model was very similar (and Kaggle scores are granted based on RMSE of predictions).

### Conclusion

The models produced unfortunately had very large residuals, indicating that the method of estimation is imprecise and any prediction had a large confidence interval. The outputs produced may be useful for taking a rough stab at initial estimation of house prices, however as noted in 'Modeling Home Price Using Realtor Data" by Pardoe, expert opinion still plays a significant factor in giving reasonable estimates of house prices. More accurate predictions are not possible without a significant improvement in experiment design and a narrowing of the problem statement, which we shall discuss below.

As for the used experimental model, 'none' categorical variables should have been omitted during dummy encoding. One such example is bsmtexposure : none, which shows up in the final model.

### Limitations in the data
Limited predictive power outside of the geographical constraint and time period

In general, housing price data reflects the local nature of housing markets and results are not applicable outside of the metropolitan area it is investigating.

The data's time collection frame also happens to include the 2007 to 2008 financial crisis, which was in part precipitated by the bursting of an American housing price bubble. Any houses sold in this period may well be explained by extraordinary circumstances such as foreclosures or otherwise homeowner bankruptancy, resulting in severely depressed housing prices. Blind application of these results outside of the time period may result in wildly undervalued housing sale value predictions.

##### Limitations in experiment design
Instead of blindly trying to regress on large, unconstrained set of features and then picking the ones that stood out the most, there may be much more analytical value in controlling for certain subsets of features and seeing how certain treatments such as different roofing or external house coverings explain variability in prices. 

It did occur that certain selected features used in the final model were not present in the unseen data. This reflects the inability of the model to generalise on unseen features and that it also loses explanatory power if features included in the model are not present. One potential fix is not to attempt to estimate house prices as a whole, but instead investigate the treatment effect of universal house metrics on sale prices, while attempting to hold other features constant.

##### Limitations in experiment methodology
Firstly, additional features could have been used, such as polynomialising all the independent variables, or checking for interaction effects. For example, values such as basement exposure which appear in the final model may have little to no explanatory power

The data could have also been regressed on log sales prices, which may have increased explanatory power if the true effect of housing characteristics on sale price is exponential. 

Secondly, as noted by David Pasta in "Learning When to be Discrete", there are measures that can be taken to counteract the loss of explanatory power when applying a continuous scale to ordinal variables with uncertain distance between categories.
