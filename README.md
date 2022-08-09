# Diamond-Prices

## Introduction
For this project, I chose a data set on various numerical and categorical details of different diamonds (carat, cut, color etc.), I used this data in order to create multiple regression models which would predict the price of the diamond based on it's significant features. I chose these predictors and response because I believe it is the most useful to use in the real world, such as being able to tell if you're getting a fair price for your engagement ring or jewlery.

## Feature Selection
I began selecting the features to use in the model by creating a basic linear regression model and finding the p-values and confidence intervals of all of the features present in the data set. I initially chose to use p-values and the confidence interval in order to determine incompatibility of the feature with the null hypothesis (there is no significant difference between specified populations, any observed difference being due to sampling or experimental error). The feature "y" was shown to have a p-value > .5, This shows me that it is probable that the feature has a higher probability of having no significant effect on predicting the response. During my examination of the confidence intervals, the feature "z" had a confidence interval that includes 0. This tells me that there is a good chance of finding no correlation between "z" and my response. Lastly, I used the variance inflation factor between the remaining predictors to determine if there was any co-linearity (independent variables in a model are correlated), which I found there was between "carat" and "x", since I have already removed the other sizing variables I determined it would be the best to remove "x" in this case to increase the reliability of the model's statstical inferences.

## Linear Model
Using the remaining features, I constructed a linear model using k-fold cross validation. I was able to get an R-squared value of 0.9160116, which represents that approximately 92% of the variance is explained by the model's inputs. Also, the model gave an RMSE () of 1156.737, which means the predicted price was on average $1156.74 off from the actual value, this doesn't appear very problematic because the prices are anywhere from the hundereds to ten-thousands, with more being in the thousands and ten thousands, so the distance is skewed by the larger prices. I also plotted a residual plot, this plot is somewhat concerning at the <8,000 fitted values where they seem to be grouped in the positive and trend towards the negative, however in the 8,000 - 20,000 range of fitted values the expected randomness is shown before the small amount of fitted values near 30,000 group up in the negative. This means that in certain ranges you could possible use one error to predict another, but the majority of fitted values you cannot. This could be do heteroscedasticity(), because of the large range of values in the predictors and the corresponding response. Lastly, I displayed Added-Variable Plots of each of the predictors to show the strength of their correlation with the response. Most of the predictors are shown to have a small negative or positive correlation while disregarding other predictors, but carat had a strong positive correlation with the predictor along with the clarity categories.

## Pruned Tree

