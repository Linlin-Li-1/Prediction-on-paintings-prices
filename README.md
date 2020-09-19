# Prediction on the prices of paintings sold in Paris in the late 18th century
This is a group project on predicting painting prices that were sold from 1764 to 1780. Based on our analysis, we identify undervalued/overvalued paintings in the dataset. 

Author:
- Linlin Li
- Bingruo Wu
- Cole Juracek
- Vidvat Ramachandran

Based on EDA (part-I), we found the following potential predictors from the graphs:
- `prevcoll`
- `lrgfont`
- `diff_origin`
- `finished`
- `engraved`
- `lands_sc`
- `portrait`
- `paired`
- `still_life`
- `lands_elem`
- `Interm`
- `figures`
- `discauth`
- `othgenre`
- `year`
- `origin_author`

We stated from building a linear model with some transformed variables. We then utlized AIC criterion to reduce the complexity of the initial model. Furthermore, we use Bayesian Model Averaging to improve the accuracy. 

#### Model Evaluation

Our model is explaining approximately 66% of the variation in the log price of paintings. It is important to note that an $R^2$ cannot be used in a vacuum to tell if the model is good or bad, but it's useful to note. We observe an RMSE of 1538.9, and a coverage of 0.956(using a 95% prediction interval). As stated previously from the residual plot, it looks like all of the assumptions for MLR have been satisfied, so our standard errors + confidence intervals will be appropriate.

#### Model Testing

For the testing data, we obtained a bias of 220.59. Relative to other groups, this seems like a reasonable bias. We could attempt to include more variables, but we think we already captured the relevant variables associated with log price. Adding more variables here could be beneficial, but likely wouldn't result in too much of a bias improvment. The other statistics here seem reasonable as well:

- Our coverage is 0.956, which is very good
- Our maxDeviation is 13429.63, almost half of some of the other groups. Therefore there are no egregiously different values that our model is predicting.
- Our MeanAbsDeviation is 455.68.
- Finally, our RMSE is 1262.07. For some reason, the RMSE is lower on the test data than the training data. It's possible that this is due to the smaller sample size of the test data. Or it could have "easier" cases to predict.

We believe this model is reasonable due to its large improvement over the null model (no predictors).

#### Model Result

- The dealer for ALL of the top 10 predicted paintings is R.
- Only one painting was not sold in 1769 or 1777. This observation was only different by one year (1776). These years must have had a good market, or R might have been dealing more than the others.
- One author has 2 paintings in the top 10: Rembrandt Harmenszoon van Rijn. This is the famous Rembrandt, so it's expected. One of the paintings, Arquebusiers / Ronde de nuit, is "The Night Watch", a very famous painting. The other is difficult to find due to the French subject with a incorrectly translated character. It's likely one of the "Holy Family" paintings, a series of 5 famous paintings.
- Most of the endbuyers were collectors that all used dealers as intermediaries.
- All of the top predicted paintings had artists that were either of Dutch/Flemish or French origin. For these, the dealer's catalog also correctly labeled their origin.
- All of these paintings had "lrgfont": the dealer devotes an additional paragraph to each painting


### Conclusion

`Dealer`, `Year`, `Endbuyer` and `Origin_author`(when the author is unknown) seem to impact the price of the paintings most(in terms of the coefficient values). We found that the people involved are more important than the painting features, when the people are unknown, the features may become more important though. For example, when the artist in unknown, painting price drops a lot. We also found that certain dealers were more active in certain years. We were also surprised that whether the author was living or not was not important to the price.

If we just want to focus on the features of the paintings and not the people involved, the best features for a painting to have are highly polished finishing, an additional paragraph and engravings done after the painting. The worst features a painting could have are if it is described as a plain landscape, if it is described as a portrait and if its description indicates still life elements. It would be advisable to look for the presence(or absence) of these features to get an idea about the price, however, our model also includes the effects of the people involved in the sale, so we need to be careful if we look at these features on their own. A model to just predict the price of the painting using the features may be better if we only want to look at their effects, but this model would not consider facts such as the reputation of the artist or the dealer etc.

On the old test dataset, we tried various different models including tree models and found that using BMA followed by lasso on the best predictive model gave us a model that could give us reasonable insight into the training data while also not poorly predicting on the test data. 

On the new dataset, we used just the BMA model without adding any constraints using lasso. If we had more time, we could have tested tree models like random forests to see if the results are any better. Since, we are just using categorical variables in our model anyway, a tree model might be better suited to this problem in terms of predictions since it can capture many more interactions than a linear model can. The BMA model is still useful as it can give easily interpretable results and we can compare the effects of various predictors.
