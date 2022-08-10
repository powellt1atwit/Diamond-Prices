# Diamond-Prices

## Introduction
For this project, I chose a data set on various numerical and categorical details of different diamonds (carat, cut, color etc.), I used this data in order to create multiple regression models which would predict the price of the diamond based on it's significant features. I chose these predictors and response because I believe it is the most useful to use in the real world, such as being able to tell if you're getting a fair price for your engagement ring or jewlery.

## Feature Selection
I began selecting the features to use in the model by creating a basic linear regression model and finding the p-values and confidence intervals of all of the features present in the data set. I initially chose to use p-values and the confidence interval in order to determine incompatibility of the feature with the null hypothesis<sup>1</sup>. The feature "y" was shown to have a p-value > .5, this shows me that it is probable that the feature has a higher probability of having no significant effect on predicting the response. During my examination of the confidence intervals, the feature "z" had a confidence interval that includes 0. This tells me that there is a good chance of finding no correlation between "z" and my response. Lastly, I used the variance inflation factor between the remaining predictors to determine if there was any co-linearity<sup>2</sup>, which I found there was between "carat" and "x", since I have already removed the other sizing variables I determined it would be the best to remove "x" in this case to increase the reliability of the model's statstical inferences.

## Linear Model
Using the remaining features, I constructed a linear model using k-fold cross validation<sup>3</sup>. I was able to get an R-squared value of 0.9160116, which represents that approximately 92% of the variance is explained by the model's inputs. Also, the model gave an RMSE<sup>4</sup> of 1156.737, which means the predicted price was on average $1156.74 off from the actual value, this doesn't appear very problematic because the prices are anywhere from the hundereds to ten-thousands, with more being in the thousands and ten thousands, so the distance is skewed by the larger prices. I also plotted a residual plot, this plot is somewhat concerning at the <8,000 fitted values where they seem to be grouped in the positive and trend towards the negative, however in the 8,000 - 20,000 range of fitted values the expected randomness is shown before the small amount of fitted values near 30,000 group up in the negative. This means that in certain ranges you could possible use one error to predict another, but the majority of fitted values you cannot. This could be do heteroscedasticity<sup>5</sup>, because of the large range of values in the predictors and the corresponding response. Lastly, I displayed Added-Variable Plots of each of the predictors to show the strength of their correlation with the response. Most of the predictors are shown to have a small negative or positive correlation while disregarding other predictors, but carat had a strong positive correlation with the predictor along with the clarity categories.

### Linear Model Equation
-4557.25 + 8895.19(carat) + 614.48(cutGood) + 877.66(cutIdeal) + 806.05(cutPremium) + 778.44(cutVeryGood) - 211.00(colorE) - 304.32(colorF) - 506.97(colorG) +
977.98(colorH) - 1438.28(colorI) - 2322.57(colorJ) + 5404.24(clarityIF) + 3567.75(claritySI1) + 2619.03(claritySI2) + 4525.42(clarityVS1) + 4210.14(clarityVS2) +
5061.75(clarityVVS1) + 4957.33(clarityVVS2) + 21.00(depth) - 24.79(table)

## Pruned Tree
In order to use a decision tree on my data, I had to implement encoding which turns all of the categorical predictors into numerical predictors because the decision tree model doesn't accept categorical predictors. I did this by adding a binary column for every unique categorical value in place of the categorical columns. 
After encoding, I constructed a decision tree from the predictors and then applied cross-validation to it in order to determine what leaves should be pruned. Out of the seven, only 5 of the leaves showed a significant effect on the predictor. After pruning the tree down to five leaves, the only relevant predictor was carat which follows the conclusion from the AV plot. I computed the RMSE, which came out to 1539.806, which means the predicted price was on average $1539.82 off from the actual value, which is a less than $400 difference from the linear model, so while it performs worse it's not a bad model in regards to the price.

## Random Forest
After reverting the dummy variables, I implemented a random forest using k-fold cross validation with differing mtry<sup>6</sup> and splitrules<sup>7</sup>. From this I was able to get a final model of mtry = 20 and splitrule = extratrees which gave me an RMSE of 564.222, which means the predicted price was on average $564.22 off from the actual value, which performed better than both the linear model and pruned tree. However, the R-squared value 0.9800124, which represents that approximately 98% of the variance is explained by the model's inputs meaning that the random forest could be somewhat overfit.

## Conclusion
Based on the implementation of the three regression models, I have come to the conclusion that the best one would be the linear model. This is due to it's lower RMSE along with it's high but not too high R-squared value because it offers a balance between an accurate model and one that best solves the bias-variance trade-off<sup>8</sup>. I have also determined that carat is the most important predictor in the price of a diamond, such that diamonds with larger carat sizes are more likely to be have a higher price. I have also determined that table and depth are the least important predictors in determining a carat's price.

## Appendex
1 - There is no significant difference between specified populations, any observed difference being due to sampling or experimental error

2 - Independent variables in a model are correlated

3 - Cross-validation is a resampling procedure used to evaluate machine learning models on a limited data sample. The procedure has a single parameter called k that       refers to the number of groups that a given data sample is to be split into. K = 5

4 - Root Mean Square Error is the standard deviation of the residuals (prediction errors)

5 - The standard deviations of a predicted variable, monitored over different values of an independent variable or as related to prior time periods, are non-constant

6 - The number of variables randomly sampled as candidates at each split

7 - Cut-point choice while splitting a tree node

8 - The property of a model that the variance of the parameter estimated across samples can be reduced by increasing the bias in the estimated parameters
