[![Dogs vs Cats Image Classification using ResNet | by Anubhav Shrimal | Anubhav Shrimal | Medium](https://tse1.mm.bing.net/th/id/OIP.-DsPwnCRCbAPc3rR2IayUgHaEK?pid=Api)](https://medium.com/anubhav-shrimal/dogs-vs-cats-image-classification-using-resnet-d2ed7e6db2bb)

Below are two concrete examples each for image‐based **classification** and **regression** tasks:

---

## 🐶🐱 Image Classification

**Problem:** Given an image, decide which discrete category it belongs to.

1. **Dogs vs. Cats**

   * **Task:** Classify each photo as “dog” or “cat.”
   * **Target:** One of two labels (dog, cat).
   * **Model output:** A probability for each class, e.g. P(dog) vs. P(cat), then pick the higher one.

2. **Handwritten Digit Recognition (MNIST)**

   * **Task:** Recognize which digit (0–9) a handwritten image represents.
   * **Target:** An integer class from 0 through 9.
   * **Model output:** A 10-way probability distribution over the digits.

---

## 🏠📈 Image Regression

**Problem:** Given an image, predict a continuous value.

1. **House Price Prediction from Photos**

   * **Task:** Estimate the market price of a house based solely on its image.
   * **Target:** A real-valued price (e.g. \$250,000).
   * **Model output:** A single continuous number.

2. **Age Estimation from Face Images**

   * **Task:** Predict a person’s age from their facial photo.
   * **Target:** A real-valued age (e.g. 28.4 years).
   * **Model output:** A regression score (the estimated age).

---

### Key Differences

| Aspect            | Classification                      | Regression                          |
| ----------------- | ----------------------------------- | ----------------------------------- |
| **Target type**   | Discrete labels (e.g. dog vs. cat)  | Continuous values (e.g. price, age) |
| **Loss function** | Cross-entropy, Gini impurity        | Mean squared error, MAE             |
| **Output**        | Class probabilities → class label   | Direct numerical prediction         |
| **Evaluation**    | Accuracy, Precision/Recall, ROC-AUC | RMSE, MAE, R²                       |

