---
layout: post
math: true
toc: true
---
## Overview
Decision trees are a type of supervised machine learning algorithm used for classification and regression tasks with a tree-like model. The basic structure of a tree
consists of the root node, decision node, and leaf node. The general procedure is that it starts at the root, splits based on the best attribute, and repeats until 
meeting stopping criteria (e.g., all instances in a leaf node belong to the same class).
![Capture](https://github.com/zhiweilin27/zhiweilin27.github.io/assets/111717798/b0cbb83a-e5e7-4296-95b8-49ade8546f0c)


There are various splitting criteria used by the regression tree and the classification tree
- Gini impurity: a measure of variance across the K classes of the qualitative response. It is widely used in classification trees.\\
$$
Gini\ Index = \sum_{i} p_{i}(1-p_{i})
$$\\
For a two-class problem, the Gini impurity for a given node can be written as:\\
$$
Gini\ Impurity = p_{1}(1-p_{1}) + p_{2}(1-p_{2})
$$
- Entropy: a measure similar to the Gini index.\\
$$Entropy = -\sum_{i} p_{i} \log_{2}(p_{i})$$\\
For a two-class problem, the entropy for a given node can be written as:\\
$$Entropy = -p \log_{2}(p) - (1 - p) \log_{2}(1 - p)$$\\
- Sum of Squared Error (SSE): Unlike the previous two metrics, SEE is widely used in a regression task.\\
$$SSE = \sum_{i \in S_{1}} (y_{i} - \bar{y}_{1})^{2} + \sum_{i \in S_{2}} (y_{i} - \bar{y}_{2})^{2}$$

**Procedure**
1. Encode categorical variables, and handle missing values.
2. Build the Tree
   - use an appropriate metric to find the best splits, and split based on the attribute that results in the most significant reduction in heterogeneity.
3. Limit the tree depth to prevent overfitting.
4. Use cross-validation to assess the model's performance (optional).
5. Use the trained model on test data

## Emsemble Models
Ensemble models combine the results of multiple models to achieve a better result. The core idea is that the aggregation of multiple models can often outperform a single model. There are 
some advantages over individual trees such as improved accuracy, reduced overfitting, increased robustness, insights into feature importance, and flexibility. Random Forest and Gradient Boosting are popular examples of ensemble decision trees that are highly effective in various domains.

### Bootstrap
Bootstrapping is a fundamental technique in ensemble modeling. It involves generating additional samples by repeatedly sampling from the existing observations with **replacement**, as new samples are available, the accuracy of statistical estimates (bias and variance) can be assessed. 
More specifically, each subset has the same size as the original dataset, and random sampling aids in estimating the mean and standard deviation by resampling from the dataset.

#### Bagging
Bagging is based on the bootstrap. It combines the results of multiple models to obtain a more generalized and robust prediction. It creates subsets (bags) from the original dataset using random sampling with replacement, and each subset is used to train a base model or weak model independently. These models run in parallel and are independent of each other.
**Random Forst** is a variant of bagging that seeks to further improve the prediction accuracy of a tree-based model. While bagging involves averaging identically distributed and possibly correlated trees, random forests seek to make the bagged trees less correlated via an additional degree of randomization - every split is allowed to use only m predictors instead of the full set of p predictors. 

#### Boosting
Boosting uses a different approach to ensemble learning than bagging and random forest. Instead of making independent bootstrapped samples, fitting a decision tree to each bootstrapped sample separately, and averaging the predictions of these trees to reduce variance, boosting builds a sequence of inter-dependent tress, each fitted to the residuals of the preceding tree and a scaled down version of the current tree's prediction is subtracted from the preceding tree's residual to from the new residual. 
Through this iterative process, boosting aims to convert a collection of weak learners into a stronger and more accurate model. The final model is a weighted combination of all the models.

well-known boosting models:

1. **Gradient Boosting Machines (GBM):** A powerful boosting technique that builds trees sequentially, with each tree learning and correcting errors made by the previous one. GBM minimizes a loss function (e.g., mean squared error for regression, cross-entropy for classification) by using gradients.

2. **XGBoost (Extreme Gradient Boosting):** A highly efficient and scalable implementation of gradient boosting. It introduces several regularization techniques to prevent overfitting and improve performance.
   
3. **LightGBM:** Another high-performance gradient boosting framework developed by Microsoft. It's known for its speed and memory efficiency, making it suitable for large datasets. LightGBM uses a novel technique called Gradient-based One-Side Sampling (GOSS) to handle large datasets more effectively.

4. **CatBoost:** Developed by Yandex, CatBoost is a gradient-boosting library that works well with categorical features without the need for one-hot encoding or preprocessing. It employs techniques like ordered boosting and oblivious trees to improve performance.

[XGBoost](https://arxiv.org/pdf/1603.02754.pdf), [LightGBM](https://proceedings.neurips.cc/paper_files/paper/2017/file/6449f44a102fde848669bdd9eb6b76fa-Paper.pdf), and [CatBoost](https://arxiv.org/pdf/1706.09516.pdf) are very popular models, providing high accuracy. 
