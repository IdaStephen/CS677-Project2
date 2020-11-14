# SHAP - SHapley Additive exPlanations 

SHAP was introduced by Lundberg et al. who proposed a unified approach to interpreting and explaining model predictions. SHAP is based on Shapley Values which is a solution concept in co-operative game theory. 


## Shapley Values: ## 
Shapley values -- a method from coalitional game theory -- tells us how to fairly distribute the "payout" among the features. <br/>
The goal of SHAP is to explain the prediction of an instance by computing the contribution of each feature to the prediction. The feature values of a data instance act as players in a coalition. Shapley values tell us how to fairly distribute the "payout" (= the prediction) among the features. A player can be an individual feature value, e.g. for tabular data. A player can also be a group of feature values. For example to explain an image, pixels can be grouped to super pixels and the prediction distributed among them.  <br/>

## Benefits of SHAP: ##
The first one is global interpretability — the collective SHAP values can show how much each predictor contributes, either positively or negatively, to the target variable. This is like the variable importance plot but it is able to show the positive or negative relationship for each variable with the target (see the SHAP value plot below).
The second benefit is local interpretability — each observation gets its own set of SHAP values (see the individual SHAP value plot below). This greatly increases its transparency. We can explain why a case receives its prediction and the contributions of the predictors. Traditional variable importance algorithms only show the results across the entire population but not on each individual case. The local interpretability enables us to pinpoint and contrast the impacts of the factors.
Third, the SHAP values can be calculated for any tree-based model, while other methods use linear regression or logistic regression models as the surrogate models.

By using the the Shapley formula, SHAP will compute all above scenario and returning the average contribution. <br/>

SHAP connects LIME and Shapley values. This is very useful to better understand both methods. It also helps to unify the field of interpretable machine learning.


