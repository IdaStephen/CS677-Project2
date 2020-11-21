# SHAP - SHapley Additive exPlanations 

SHAP was introduced by Lundberg et al. who proposed a unified approach to interpreting and explaining model predictions. SHAP is based on Shapley Values which is a solution concept in co-operative game theory. 

![SHAP overview](https://github.com/IdaStephen/CS677-SHAP/blob/main/SHAP-equation.png)




## Shapley Values: ## 
Shapley values -- a method from coalitional game theory -- tells us how to fairly distribute the "payout" among the features. <br/>
The goal of SHAP is to explain the prediction of an instance by computing the contribution of each feature to the prediction. The feature values of a data instance act as players in a coalition. Shapley values tell us how to fairly distribute the "payout" (= the prediction) among the features. 

### Example:

A company with two employees Alice and Bob

● No employees, no profit [v({}) = 0]

● Alice alone makes 20 units of profit [v({Alice}) = 20]

● Bob alone makes 10 units of profit [v({Bob}) = 10]

● Alice and Bob make 50 units of profit [v({Alice, Bob}) = 50]

What shouuld the bonuses be?

![SHAP values](https://github.com/IdaStephen/CS677-SHAP/blob/main/shapvalues.png)

The axioms can be intuitively understood as follows;

[Efficiency] The bonuses add up to the total profit

[Dummy] An employee that does not contribute gets no profit

[Symmetry] Symmetric employees get equal profit

[Linearity] Suppose the total profit comes from two separate departments. Then the bonus allocated to each employee should be the sum of the bonuses that they would receive from each of the departments individually.

### Shapley Value algorithm

It is based on the concept of marginal contribution of an employee to the profit. Consider all possible orderings of employees. For each ordering, we introduce the employees in that order and note change in total profit at each step. The average marginal contribution of an employee across all orderings is the employee’s Shapley value.

Suppose there are three employees and the order is Alice, Bob, Carol. Then we first add Alice to the company and note the increase in profit. This is the marginal contribution of Alice.  Then we add Bob with Alice already present, and note the increase in profit. This is the marginal contribution of Bob, and so on. We repeat this for all possible orderings and compute the average marginal contribution.

![SHAP header](https://github.com/IdaStephen/CS677-SHAP/blob/main/shapleyvalues2.png)


![SHAP header](https://github.com/IdaStephen/CS677-SHAP/blob/main/shap_header.png)

## Why is SHAP more popular and reliable technique? ##
1. Local Accuracy
The explanation model should match the original model.

2. Missingness:
If the simplified inputs represent feature presence, then missingness requires features missing in the original input to have no impact.
Missingness says that a missing feature gets an attribution of zero. A missing feature could -- in theory -- have an arbitrary Shapley value without hurting the local accuracy property, since it is multiplied with x' = 0. The Missingness property enforces that missing features get a Shapley value of 0. In practice this is only relevant for features that are constant.

3. Consistency:
Consistency states that if a model changes so that some simplified input’s contribution increases or stays the same regardless of the other inputs, that input’s attribution should not decrease.

4. Efficiency:
As the foundation of SHAP values is based on computational game theory, this is the only method that can failry distribute the gain of the feature.

5. Global comparison:
SHAP values provide a way to compare the feature importance at a global level. You can also change the dataset from global to a subset dataset of interest.


## Benefits of SHAP: ##

1. The SHAP values can be calculated for any tree-based model, while other methods use linear regression or logistic regression models as the surrogate models.

2. SHAP connects LIME and Shapley values. This is very useful to better understand both methods. It also helps to unify the field of interpretable machine learning.

3. SHAP has a fast implementation for tree-based models. I believe this was key to the popularity of SHAP, because the biggest barrier for adoption of Shapley values is the slow computation

4. The fast computation makes it possible to compute the many Shapley values needed for the global model interpretations. The global interpretation methods include feature importance, feature dependence, interactions, clustering and summary plots. With SHAP, global interpretations are consistent with the local explanations, since the Shapley values are the "atomic unit" of the global interpretations. 

5. Local interpretability — each observation gets its own set of SHAP values. This greatly increases its transparency. We can explain why a case receives its prediction and the contributions of the predictors. Traditional variable importance algorithms only show the results across the entire population but not on each individual case. The local interpretability enables us to pinpoint and contrast the impacts of the factors.

## TreeSHAP

Lundberg et. al proposed TreeSHAP, a variant of SHAP for tree-based machine learning models such as decision trees, random forests and gradient boosted trees. TreeSHAP was introduced as a fast, model-specific alternative to KernelSHAP, but it turned out that it can produce unintuitive feature attributions.

TreeSHAP defines the value function using the conditional expectation instead of the marginal expectation. The problem with the conditional expectation is that features that have no influence on the prediction function f can get a TreeSHAP estimate different from zero. The non-zero estimate can happen when the feature is correlated with another feature that actually has an influence on the prediction.

## SHAP Feature Importance
The idea behind SHAP feature importance is simple: Features with large absolute Shapley values are important. Since we want the global importance, we average the absolute Shapley values per feature across the data. Next, we sort the features by decreasing importance and plot them. SHAP feature importance is an alternative to permutation feature importance. There is a big difference between both importance measures: Permutation feature importance is based on the decrease in model performance. SHAP is based on magnitude of feature attributions. 
The feature importance plot is useful, but contains no information beyond the importances. For a more informative plot, we will next look at the summary plot.

## SHAP Summary Plot
The summary plot combines feature importance with feature effects. Each point on the summary plot is a Shapley value for a feature and an instance. The position on the y-axis is determined by the feature and on the x-axis by the Shapley value. The color represents the value of the feature from low to high. Overlapping points are jittered in y-axis direction, so we get a sense of the distribution of the Shapley values per feature. The features are ordered according to their importance. In the summary plot, we see first indications of the relationship between the value of a feature and the impact on the prediction. But to see the exact form of the relationship, we have to look at SHAP dependence plots.

## SHAP Dependence Plot
SHAP feature dependence might be the simplest global interpretation plot: 
1) Pick a feature. 
2) For each data instance, plot a point with the feature value on the x-axis and the corresponding Shapley value on the y-axis. 

## Disadvantages of Using SHAP ##

1. KernelSHAP is slow. This makes KernelSHAP impractical to use when you want to compute Shapley values for many instances. Also all global SHAP methods such as SHAP feature importance require computing Shapley values for a lot of instances.

2. KernelSHAP ignores feature dependence. Most other permutation based interpretation methods have this problem. By replacing feature values with values from random instances, it is usually easier to randomly sample from the marginal distribution. However, if features are dependent, e.g. correlated, this leads to putting too much weight on unlikely data points. TreeSHAP solves this problem by explicitly modeling the conditional expected prediction.

3. TreeSHAP can produce unintuitive feature attributions. While TreeSHAP solves the problem of extrapolating to unlikely data points, it introduces a new problem. TreeSHAP changes the value function by relying on the conditional expected prediction. With the change in the value function, features that have no influence on the prediction can get a TreeSHAP value different from zero.

4. The disadvantages of Shapley values also apply to SHAP: Shapley values can be misinterpreted and access to data is needed to compute them for new data (except for TreeSHAP).


