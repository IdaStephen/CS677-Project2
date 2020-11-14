# SHAP - SHapley Additive exPlanations 

<h3>Summary:</h3><br/>
SHAP was introduced by Lundberg et al. who proposed a unified approach to interpreting and explaining model predictions. SHAP is based on Shapley Values which is a solution concept in co-operative game theory. 
<br/>
A prediction can be explained by assuming that each feature value of the instance is a "player" in a game where the prediction is the payout. Shapley values -- a method from coalitional game theory -- tells us how to fairly distribute the "payout" among the features. <br/>
The goal of SHAP is to explain the prediction of an instance by computing the contribution of each feature to the prediction. The feature values of a data instance act as players in a coalition. Shapley values tell us how to fairly distribute the "payout" (= the prediction) among the features. A player can be an individual feature value, e.g. for tabular data. A player can also be a group of feature values. For example to explain an image, pixels can be grouped to super pixels and the prediction distributed among them. n SHAP, feature importance is assigned to every feature which is equivalent to mentioned contribution. Let take auto loan (car loan) as an example. We have “New Driver”, “Has Children”, “4 Door” and “Age”.
Theoretically, number of combination is 2^n, where n is number of feature. Given that we want to know the Shapley value of the “Age”. We will predict all of the following combination with and without “Age” feature. There is some optimization mentioned. <br/>

By using the the Shapley formula, SHAP will compute all above scenario and returning the average contribution. <br/>

SHAP connects LIME and Shapley values. This is very useful to better understand both methods. It also helps to unify the field of interpretable machine learning.


