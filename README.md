# SHAP - SHapley Additive exPlanations 

Summary:
Model Interpreation and Explainability are important. SHAP was introduced by Lundberg et al. who proposed a unified approach to interpreting model predictions. SHAP is based on Shapley Values which is a solution concept in co-operative game theory. 

Let take a development team as an example. Our target is going to deliver a deep learning model which needs to finish 100 line of codes while we have 3 data scientists (L, M, N). 3 of them must work together in order to deliver the project. Given that:
![solarized palette](https://github.com/IdaStephen/CS677-SHAP/blob/main/Image1.png)
Contribution among coalition
Image for post
Marginal Contribution by different orders
We have 3 player so the total combination is 3! which is 6. The above tables show the contribution according to different order of coalition.
Image for post
According to the Sherley value formula, we have the above tables. Although the capability of M is 6 times greater than N (30 vs 5), M should get 41.7% of reward while N should get 24.17% reward.
