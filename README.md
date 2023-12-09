# Model for prediction of the result of LOL games

Eric Chen, Ruijia Xiao

## Framing the Problem

<!--Clearly state your prediction problem and type (classification or regression). If you are building a classifier, make sure to state whether you are performing binary classification or multiclass classification. Report the response variable (i.e. the variable you are predicting) and why you chose it, the metric you are using to evaluate your model and why you chose it over other suitable metrics (e.g. accuracy vs. F1-score).-->

In this webpage, we present our result of the model we design to predict the game result for a LOL game. For our model, we choose decision tree classifier, and we are performing binary classification. The response variable is "result", the reason why we choose it is because it shows the result of the game. The metric we choosed is accuracy, and the reason why we choose it over f1 score is we believe in this case True Positives and True negatives is more important. 

## Baseline Model

<!--Describe your model and state the features in your model, including how many are quantitative, ordinal, and nominal, and how you performed any necessary encodings. Report the performance of your model and whether or not you believe your current model is “good” and why.-->

For the baseline model, we use decision tree classifer, and the features we used in our model are "totalgold" and "dragon", they are both quantitative. They are already quantitative and after checking they don't contain missing value, we believe we don't have to do any necessary encodings to it. We split our data set to train and test sets, and we use train set to train the model, and the accuracy on the test set is 0.7037751004016064. For this performance, we believe this model is not a bad model because it passes the threshold of 70% accurancy, but we also consider it still cannot be considered as a model because the performance is not even near 95%.

## Final Model

<!-- State the features you added and why they are good for the data and prediction task. Note that you can’t simply state “these features improved my accuracy”, since you’d need to choose these features and fit a model before noticing that – instead, talk about why you believe these features improved your model’s performance from the perspective of the data generating process.

Describe the modeling algorithm you chose, the hyperparameters that ended up performing the best, and the method you used to select hyperparameters and your overall model. Describe how your Final Model’s performance is an improvement over your Baseline Model’s performance. -->

For this final model, we added two new features "teamkills" and "teamdeaths". Adding these two new features into our model can improve our accuracy of model because in games, the teams can obtain more advantages by eliminating the opponents and preventing killing by opponents, which can be directly showed in teamkills and teamdeaths data. And the team that hvae more advantages are more likely to win the game, so we believe it can improve our accuracy. As the baseline model, we also choose decision tree classifer, and since our two new features are also quantitative. So after checking they don't contain missing value, we believe we don't have to do any necessary encodings to it. After we do some grid search on hyperparameters max_depth and criterion, we find out the best parameter are max_depth=7 and criterion=gini. Therefore, we use DecisionTreeClassifier(max_depth = 7, criterion='gini') as our classifier of model. For our final model, it has a 0.9561445783132531 accuracy on the test set. The accuracy of this final model is much more high compared to the accuracy of the baseline model, so the performance of model is improved. 

## Fairness Analysis

<!-- Clearly state your choice of Group X and Group Y, your evaluation metric, your null and alternative hypotheses, your choice of test statistic and significance level, the resulting p-value, and your conclusion.

Optional: Embed a visualization related to your permutation test in your website.

Tip: When making writing your conclusions to the statistical tests in this project, never use language that implies an absolute conclusion; since we are performing statistical tests and not randomized controlled trials, we cannot prove that either hypothesis is 100% true or false.-->

For fairness analysis, we want to find out that iIs our model fair worse for long game than for short game. In this part, we defined out two groups as: Long game (game length>=1800s) and Short game(game length<1800s), the evaluation metric is accuracy. Null hypothesis is "Our model is fair for long game(game length>=1800s) and short game(game length<1800s)", and alternative hypotheses is "Our model is worse for long game(game length>=1800s) than for short game(game length<1800s)". Our test statstic is if the prediction is the same as the result, and our siginificance level is 0.05, the resulting p-value is 0.0. Therefore, our conclusion is that we are more likely to believe that our model perform worse for long game than short game. 