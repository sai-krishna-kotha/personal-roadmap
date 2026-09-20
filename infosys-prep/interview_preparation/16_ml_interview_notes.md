# ML Interview Notes

## Table of Contents
- [Machine Learning Workflow](#machine-learning-workflow)
- [Classification vs Regression](#classification-vs-regression)
- [Common Algorithms](#common-algorithms)
- [Linear Regression](#linear-regression)
- [Logistic Regression](#logistic-regression)
- [Decision Trees](#decision-trees)
- [Random Forest](#random-forest)
- [K-Nearest Neighbors](#k-nearest-neighbors)
- [K-Means](#k-means)
- [Feature Scaling](#feature-scaling)
- [Normalization vs Standardization](#normalization-vs-standardization)
- [Loss and Cost Functions](#loss-and-cost-functions)
- [Gradient Descent](#gradient-descent)
- [Learning Rate](#learning-rate)
- [Bias Variance Tradeoff](#bias-variance-tradeoff)
- [Regularization](#regularization)
- [Classification Metrics](#classification-metrics)
- [Confusion Matrix](#confusion-matrix)
- [Precision Recall and F1](#precision-recall-and-f1)
- [ROC AUC](#roc-auc)
- [Class Imbalance](#class-imbalance)
- [Cross Validation](#cross-validation)
- [Data Leakage](#data-leakage)
- [Feature Engineering](#feature-engineering)
- [Hyperparameters](#hyperparameters)
- [Important ML Interview Q&A](#important-ml-interview-qa)
- [Project Connections](#project-connections)
- [ML Interview Traps](#ml-interview-traps)
- [Final Checklist](#final-checklist)

<a id="table-of-contents"></a>

<a id="machine-learning-workflow"></a>
## Machine Learning Workflow

[Back to Table of Contents](#table-of-contents)

A practical workflow:

```text
problem definition
→ data collection
→ cleaning/preprocessing
→ train/validation/test split
→ feature engineering
→ model training
→ evaluation
→ tuning
→ deployment
→ monitoring
```

First define the prediction target and evaluation metric. Choosing a model before understanding the problem often leads to poor decisions.

<a id="classification-vs-regression"></a>
## Classification vs Regression

[Back to Table of Contents](#table-of-contents)

Classification predicts a discrete class.

Examples:
- spam / not spam
- disease / no disease

Regression predicts a numerical value.

Examples:
- house price
- demand
- temperature

<a id="common-algorithms"></a>
## Common Algorithms

[Back to Table of Contents](#table-of-contents)

| Algorithm | Typical use |
|---|---|
| Linear Regression | numerical prediction |
| Logistic Regression | binary/multiclass classification |
| Decision Tree | classification/regression |
| Random Forest | robust tree ensemble |
| KNN | similarity-based prediction |
| K-Means | clustering |
| Naive Bayes | text/classification baselines |
| SVM | classification/regression |
| Gradient Boosting | strong tabular modeling |

Know the intuition and main trade-off rather than memorizing formulas only.

<a id="linear-regression"></a>
## Linear Regression

[Back to Table of Contents](#table-of-contents)

Predict a continuous value:

```text
y_hat = w1*x1 + w2*x2 + b
```

Example:
Predict salary from years of experience.

Training chooses parameters that minimize an error such as mean squared error.

Strength:
Simple, interpretable baseline.

Limitation:
A basic linear model cannot represent arbitrary nonlinear relationships.

<a id="logistic-regression"></a>
## Logistic Regression

[Back to Table of Contents](#table-of-contents)

Despite its name, logistic regression is commonly used for classification.

It computes a score and maps it to a probability using the sigmoid function:

```text
sigmoid(z) = 1 / (1 + e^-z)
```

Example:
Probability that an email is spam.

A threshold is then used to turn probability into a class decision.

<a id="decision-trees"></a>
## Decision Trees

[Back to Table of Contents](#table-of-contents)

A decision tree recursively splits data using feature-based rules.

Example:

```text
attendance < 60%?
  ├── yes -> likely fail
  └── no  -> check marks
```

Advantages:
- easy to explain
- handles nonlinear relationships
- little feature scaling required

Risk:
Deep trees can overfit.

<a id="random-forest"></a>
## Random Forest

[Back to Table of Contents](#table-of-contents)

Random Forest combines many decision trees and aggregates their predictions.

The trees are trained using randomized subsets of data/features.

Why it helps:
Individual trees have high variance; averaging many trees can improve robustness.

<a id="k-nearest-neighbors"></a>
## K-Nearest Neighbors

[Back to Table of Contents](#table-of-contents)

KNN predicts based on nearby training examples.

For classification:
- find k closest points
- use their class votes

Feature scaling matters because distance is sensitive to feature magnitude.

<a id="k-means"></a>
## K-Means

[Back to Table of Contents](#table-of-contents)

K-Means is an unsupervised clustering algorithm.

Basic process:
1. choose k centroids
2. assign points to nearest centroid
3. recompute centroids
4. repeat until convergence

Example:
Group customers based on spending and frequency.

Limitation:
You must choose k, and results can be sensitive to initialization and scale.

<a id="feature-scaling"></a>
## Feature Scaling

[Back to Table of Contents](#table-of-contents)

Scaling puts numerical features on comparable scales.

Important for:
- KNN
- K-Means
- SVM
- gradient-based models

Often less important for tree-based models.

<a id="normalization-vs-standardization"></a>
## Normalization vs Standardization

[Back to Table of Contents](#table-of-contents)

Normalization often refers to mapping values to a bounded range such as [0,1].

Standardization typically transforms:

```text
z = (x - mean) / standard_deviation
```

Fit preprocessing on training data and apply the learned transformation to validation/test data.

<a id="loss-and-cost-functions"></a>
## Loss and Cost Functions

[Back to Table of Contents](#table-of-contents)

A loss function measures error for an example or batch.

Common examples:
- MSE for regression
- cross-entropy/log loss for classification

A cost/objective is often the aggregate objective optimized during training.

<a id="gradient-descent"></a>
## Gradient Descent

[Back to Table of Contents](#table-of-contents)

Gradient descent updates parameters in the direction that reduces the objective:

```text
parameter = parameter - learning_rate * gradient
```

Variants:
- batch
- stochastic
- mini-batch

<a id="learning-rate"></a>
## Learning Rate

[Back to Table of Contents](#table-of-contents)

Learning rate controls update size.

Too large:
- training can diverge or oscillate.

Too small:
- training may be very slow.

<a id="bias-variance-tradeoff"></a>
## Bias Variance Tradeoff

[Back to Table of Contents](#table-of-contents)

High bias:
- model is too simple
- tends toward underfitting

High variance:
- model is too sensitive to training data
- tends toward overfitting

The practical goal is a model that generalizes well.

<a id="regularization"></a>
## Regularization

[Back to Table of Contents](#table-of-contents)

Regularization discourages overly complex models.

Common forms:
- L1: encourages sparse parameters
- L2: penalizes large parameter values
- dropout: randomly disables neural-network activations during training

<a id="classification-metrics"></a>
## Classification Metrics

[Back to Table of Contents](#table-of-contents)

Accuracy:

```text
correct / total
```

For imbalanced data, inspect precision, recall, F1 and confusion matrix rather than relying only on accuracy.

<a id="confusion-matrix"></a>
## Confusion Matrix

[Back to Table of Contents](#table-of-contents)

Binary classification outcomes:
- TP
- TN
- FP
- FN

```text
                 Actual
              positive negative
Pred positive    TP       FP
Pred negative    FN       TN
```

<a id="precision-recall-and-f1"></a>
## Precision Recall and F1

[Back to Table of Contents](#table-of-contents)

Precision:

```text
TP / (TP + FP)
```

"Of predicted positives, how many were actually positive?"

Recall:

```text
TP / (TP + FN)
```

"Of actual positives, how many did we find?"

F1 is the harmonic mean of precision and recall.

<a id="roc-auc"></a>
## ROC AUC

[Back to Table of Contents](#table-of-contents)

ROC examines true-positive rate against false-positive rate across thresholds.

AUC summarizes ranking quality across thresholds.

<a id="class-imbalance"></a>
## Class Imbalance

[Back to Table of Contents](#table-of-contents)

Example:
99% normal, 1% fraud.

Always predicting normal gets 99% accuracy while detecting no fraud.

Possible approaches:
- class weighting
- resampling
- threshold tuning
- appropriate metrics
- collecting more minority examples

<a id="cross-validation"></a>
## Cross Validation

[Back to Table of Contents](#table-of-contents)

K-fold cross-validation:
- split training data into k folds
- train on k-1 folds
- validate on the remaining fold
- repeat
- aggregate results

Keep the final test set separate from repeated model-selection decisions.

<a id="data-leakage"></a>
## Data Leakage

[Back to Table of Contents](#table-of-contents)

Leakage occurs when information unavailable at prediction time influences training.

Example:
Scaling the whole dataset before splitting lets test statistics influence training.

Correct:
- split first
- fit preprocessing on training data
- transform validation/test with learned parameters

<a id="feature-engineering"></a>
## Feature Engineering

[Back to Table of Contents](#table-of-contents)

Feature engineering transforms raw data into useful inputs.

Examples:
- date -> day of week
- transaction history -> average transaction value
- text -> TF-IDF features
- image -> normalized/learned features

<a id="hyperparameters"></a>
## Hyperparameters

[Back to Table of Contents](#table-of-contents)

Model parameters are learned from data.

Hyperparameters are chosen by the practitioner/training procedure.

Examples:
- learning rate
- tree depth
- number of trees
- k in KNN
- regularization strength

Tuning methods include grid search, random search and Bayesian optimization.

<a id="important-ml-interview-qa"></a>
## Important ML Interview Q&A

[Back to Table of Contents](#table-of-contents)

### Why is scaling important for KNN?

KNN depends on distance. A feature with a much larger numeric scale can dominate the distance.

### Why can a decision tree overfit?

A deep tree can keep splitting until it models noise and peculiarities of training examples.

### Why does Random Forest reduce variance?

It averages diverse trees, reducing sensitivity to any one training sample.

### Precision vs recall?

Precision focuses on false positives. Recall focuses on false negatives.

### What is data leakage?

Using information during training that would not legitimately be available when making the prediction.

### What is cross-validation?

Repeated train/validation splits used to estimate and compare model performance.

<a id="project-connections"></a>
## Project Connections

[Back to Table of Contents](#table-of-contents)

For PCOS detection, discuss:
- classification vs detection
- train/validation/test split
- augmentation
- class imbalance
- precision/recall
- confusion matrix
- overfitting
- CNN feature learning
- YOLO-style object detection
- XGBoost for tabular/feature-based modeling

Be ready to explain the target, preprocessing, metric and model choice.

<a id="ml-interview-traps"></a>
## ML Interview Traps

[Back to Table of Contents](#table-of-contents)

- 99% accuracy does not always mean a good model.
- Scaling is not equally necessary for all algorithms.
- Correlation is not causation.
- Test data should not guide repeated tuning.
- More complex models do not automatically generalize better.
- Precision and recall answer different questions.

<a id="final-checklist"></a>
## Final Checklist

[Back to Table of Contents](#table-of-contents)

Know:
- workflow
- classification vs regression
- common algorithms
- linear/logistic regression
- trees and Random Forest
- KNN and K-Means
- scaling
- loss
- gradient descent
- learning rate
- bias/variance
- regularization
- confusion matrix
- precision/recall/F1
- ROC-AUC
- class imbalance
- cross-validation
- leakage
- feature engineering
- hyperparameters
