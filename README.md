# Home-pricing Models for the Ames-Iowa Market.
by p.Shyr/DSI5

A report of the model analysis performed on the Ames dataset is presented in this folder including 5 notebooks in total.

### Problem hypothesis:
In this study we are interested the health of high-end of the Ames housing market.  This may have positive implications for the Ames Chamber of Commerce and the possible prospects for future population growth.

### Findings
There is a reasonably good fit for the Ames housing market using a linear-regression model.  We present some evidence that the high-end of the Ames market is relatively healthy and strong.  This requires further investigation to separate the logarithmic-scale relationship in home prices, to test the possible effects at the top-end of the market.

### Research
There is supporting journal reports suggesting that the Ames market is strong at the high-end and in general.
"
The amount of individual households in Ames is projected to increase by about 4,000 through the next 30 years with most of the demand coming from high-income homeowners and renters making less than $40,00 a year, according to a forecast released Tuesday by the Iowa Finance Authority.
"
( http://www.amestrib.com/news/20180522/report-ames-to-add-4000-households-over-next-30-years )


# Summary of Methodology and Results

#### Cleaning and Exploration of Data

There were almost 10,000 misssing values in the training dataset.  The categorical nulls were imputed with "None."  There were two observation outliers for homes with high square-footage, but relatively low prices and were excluded from processing and modeling.  There was a value of 2207 for the Garage-Year-Built feature, that was imputed as 2007, the year after the home itself was built. For the missing Garage-Year-Built observations, imputation of the mean of (house) Year-Built was made.  The reason for this that in a home built in Iowa without a garage is as unlikely as a home built without a basement.  The utilities feature was dropped as a feature worth modeling.

#### Pre-processing of Data in advance of Modeling

Using cross-validation withing multiple-folds in the training dataset, there was evidence that outliers were evenly distributed throughout.

#### Three Models using Linear-Regression, Lasso- and Ridge-regularization

| Top-features | Lasso-coefficients |
| --- | --- |
| GrLivArea | 14294.207110352603 |
| OverallQual | 11739.032509777811 |
| TotalBsmtSF | 10411.628004244918 |
| YearBuilt | 10140.822485979115 |
| BsmtFinSF1 | 8982.256213496963 |

There were similar features with the strongest predictive power for homes prices.  Ground-Living-Area topped both "weighting" lists, but in the Lasso-based model, this predictore was much stronger that the second-best predictor of "Overall-Quality".
Interestingly, the Ridge-model found "Second-Floor Square-footage" among the strongest feature predictors, but not the Lasso-model's top-20 of feature predictors.  While overfit with 300+ features, the first linear-regression model did not have a list of top feature predictors matching the other tow models.

| Top-features | Ridge-coefficients |
| --- | --- |
| GrLivArea | 14294.207110352603 |
| YearBuilt | 11739.032509777811 |
| 2ndFlrSF | 10411.628004244918 |
| TotalBsmtSF | 10140.822485979115 |
| BsmtFinSF1 | 8982.256213496963 |

#### Statistical Metrics to Evaluate the Models

There is a pattern from error metrics that an overfit linear-regression model is the worst-fitting model of the three models.
Also, a regression model for smaller set of features using Ridge regularization is slightly better than one using Lasso regularization.

| metric | LinReg | Lasso_prod| Ridge_prod|
| --- | --- | --- | --- |
| score | 0.9441678745346292 | 0.9441865204471793 | 0.9442623563732895 |
| MSE | 350195921.98677963 | 350078969.2022968 | 349603303.4123507 |
| RMSE | 18713.522436644034 | 18710.397355542635 | 18697.681765725683 |
| mean-AE | 12831.536928371226 | 12810.758110519813 | 12805.973867902978 |
| medn-AE | 9302.135911006277 | 9309.497258766976 | 9242.662263545571 |
| r^2 | 0.9441678745346292 | 0.9441865204471793 | 0.9442623563732895 |

#### Kaggle Submission

Although the Ridge-regression supported by error-metrics appears to provide a better model fit based on 141 numerical and categorical features, the Lasso-regression scored higher in the Kaggle ranking for public data.

