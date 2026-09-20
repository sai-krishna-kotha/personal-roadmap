# AI Interview Notes

## Table of Contents
- [AI Fundamentals](#ai-fundamentals)
- [AI vs ML vs Deep Learning](#ai-vs-ml-vs-deep-learning)
- [Types of Learning](#types-of-learning)
- [Features and Labels](#features-and-labels)
- [Training Validation and Test Data](#training-validation-and-test-data)
- [Model Training](#model-training)
- [Overfitting and Underfitting](#overfitting-and-underfitting)
- [Generalization](#generalization)
- [Inference](#inference)
- [Important AI Interview Q&A](#important-ai-interview-qa)
- [AI Project Connection](#ai-project-connection)
- [AI Interview Traps](#ai-interview-traps)
- [Final Checklist](#final-checklist)

<a id="table-of-contents"></a>

<a id="ai-fundamentals"></a>
## AI Fundamentals

[Back to Table of Contents](#table-of-contents)

Artificial Intelligence is the broader field of building systems that perform tasks associated with human-like capabilities such as perception, reasoning, prediction and decision-making.

Example:
- Spam filtering
- Recommendation systems
- Face detection
- Chatbots
- Route planning

Interview answer:
"AI is the broad field. Machine learning is one major approach where systems learn patterns from data instead of relying only on explicitly programmed rules."

<a id="ai-vs-ml-vs-deep-learning"></a>
## AI vs ML vs Deep Learning

[Back to Table of Contents](#table-of-contents)

Think of the relationship as:

```text
Artificial Intelligence
└── Machine Learning
    └── Deep Learning
```

- AI: broad field.
- ML: algorithms learn patterns from data.
- Deep Learning: ML based on multi-layer neural networks.

Example:
A handwritten-digit recognizer is an AI application. If it learns from labeled examples using a neural network, it is ML; if it uses a deep neural network, it is deep learning.

<a id="types-of-learning"></a>
## Types of Learning

[Back to Table of Contents](#table-of-contents)

Supervised learning:
- learns from input-output examples
- classification and regression are common tasks

Unsupervised learning:
- finds structure without target labels
- clustering and dimensionality reduction are common tasks

Reinforcement learning:
- an agent interacts with an environment
- receives rewards/penalties
- learns a policy for actions

Simple example:
- Predict house price -> supervised regression.
- Group customers -> unsupervised clustering.
- Learn game actions from rewards -> reinforcement learning.

<a id="features-and-labels"></a>
## Features and Labels

[Back to Table of Contents](#table-of-contents)

Features are input variables used by the model.

Label/target is what the model is trained to predict.

Example:

```text
hours_studied, attendance -> exam_passed
5, 90%             -> 1
2, 50%             -> 0
```

Here:
- features = hours_studied, attendance
- label = exam_passed

<a id="training-validation-and-test-data"></a>
## Training Validation and Test Data

[Back to Table of Contents](#table-of-contents)

Training data:
- used to learn model parameters.

Validation data:
- used during development for model selection and hyperparameter tuning.

Test data:
- used for final evaluation on unseen data.

Critical point:
Do not tune repeatedly on the test set, because it can leak information about the final evaluation.

<a id="model-training"></a>
## Model Training

[Back to Table of Contents](#table-of-contents)

Typical flow:

```text
data
  ↓
preprocess
  ↓
split
  ↓
train model
  ↓
validate/tune
  ↓
final test
  ↓
deploy
```

A model learns parameters that reduce an objective/loss function.

Example:
For linear regression:

```text
prediction = w*x + b
```

Training updates w and b to reduce prediction error.

<a id="overfitting-and-underfitting"></a>
## Overfitting and Underfitting

[Back to Table of Contents](#table-of-contents)

Overfitting:
- model learns training data too specifically
- training performance is strong
- unseen-data performance is poor

Underfitting:
- model is too simple or insufficiently trained
- training and test performance are both poor

Typical remedies for overfitting:
- more representative data
- regularization
- simpler model
- data augmentation where appropriate
- early stopping
- better validation

<a id="generalization"></a>
## Generalization

[Back to Table of Contents](#table-of-contents)

Generalization means performing well on unseen data from the intended data distribution.

Example:
A disease classifier trained on one hospital should not be assumed to generalize to another hospital without checking differences in equipment, patient population and data distribution.

<a id="inference"></a>
## Inference

[Back to Table of Contents](#table-of-contents)

Inference is using a trained model to produce predictions on new inputs.

Training:
```text
learn parameters
```

Inference:
```text
use learned parameters
```

Interview distinction:
Training is usually compute-intensive learning. Inference is the prediction stage used by the application.

<a id="important-ai-interview-qa"></a>
## Important AI Interview Q&A

[Back to Table of Contents](#table-of-contents)

### What is the difference between AI and ML?

AI is the broader field; ML is a data-driven approach within AI.

### What is supervised learning?

Learning from labeled examples where the desired target is known.

### What is overfitting?

When a model fits training data too closely and loses generalization to unseen data.

### Why do we split data?

To train, tune and evaluate models without relying on the same data for every stage.

### What is inference?

Running a trained model on new data to obtain predictions.

### What is a feature?

An input variable used by a model.

### What is a label?

The target value the model attempts to predict.

<a id="ai-project-connection"></a>
## AI Project Connection

[Back to Table of Contents](#table-of-contents)

For a computer-vision project such as PCOS detection:

```text
dataset
  ↓
image preprocessing
  ↓
model training
  ↓
validation
  ↓
test
  ↓
inference on new image
  ↓
prediction
```

Interview explanation:
"The model is trained on representative labeled examples. During inference, a new image is transformed using the same required preprocessing and passed to the trained model to produce a prediction."

<a id="ai-interview-traps"></a>
## AI Interview Traps

[Back to Table of Contents](#table-of-contents)

- AI and ML are not exact synonyms.
- A test set should not become a tuning set.
- High training accuracy does not prove good generalization.
- Inference is not the same as training.
- More complex models are not automatically better.
- A model's accuracy depends on data quality and task definition.

<a id="final-checklist"></a>
## Final Checklist

[Back to Table of Contents](#table-of-contents)

Know:
- AI
- ML
- deep learning
- supervised learning
- unsupervised learning
- reinforcement learning
- features and labels
- train/validation/test split
- training vs inference
- overfitting
- underfitting
- generalization
