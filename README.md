<h1><span style="color:#58a6ff;">🎯 Regression Project</span></h1>
<h3><span style="color:#d2a8ff;">Predicting Deaths Caused by Cancer</span></h3>

---

## ⚙️ <span style="color:#79c0ff;">Run</span>

```bash
python3 main.py
```

---

## 📊 <span style="color:#ffa657;">Possible Metrics</span>

### <span style="color:#a5d6ff;">Regression</span>

* 🧮 <span style="color:#c9d1d9;">RMSE</span>
* 📏 <span style="color:#c9d1d9;">MAE</span>
* 📈 <span style="color:#c9d1d9;">R²-score</span>

### <span style="color:#ffa657;">Classification</span>

* ✅ <span style="color:#c9d1d9;">Accuracy</span>
* 🎯 <span style="color:#c9d1d9;">Precision</span>
* 🔁 <span style="color:#c9d1d9;">Recall</span>
* ⚖️ <span style="color:#c9d1d9;">F1-score</span>
* 🧠 <span style="color:#c9d1d9;">AUC-ROC</span>

---

## 🧩 <span style="color:#56d364;">Pipeline Algorithm (`main.py`)</span>

### 🪜 <span style="color:#d2a8ff;">Step 1 — Split the Dataset</span>

| Split                                             | Purpose                                     | Portion |
| :------------------------------------------------ | :------------------------------------------ | :------ |
| 🧠 <span style="color:#79c0ff;">Training</span>   | Train the model                             | 60%     |
| 🔍 <span style="color:#79c0ff;">Validation</span> | Tune hyperparameters / detect bias-variance | 20%     |
| 🧾 <span style="color:#79c0ff;">Test</span>       | Final evaluation                            | 20%     |

> 💡 <span style="color:#8b949e;">Use stratified splitting for imbalanced classes or cross-validation for small datasets.</span>

---

### ⚗️ <span style="color:#d29922;">Step 2 — Baseline Model</span>

Start with simple, interpretable baselines:

* Regression → <span style="color:#58a6ff;">Linear Regression</span> (`λ = 0`, `degree = 1`)
* Classification → <span style="color:#58a6ff;">Logistic Regression</span> or Decision Tree

Evaluate both:

* <span style="color:#79c0ff;">Training Error</span> → fit quality
* <span style="color:#79c0ff;">Validation Error</span> → generalization

> 🎯 Establish this baseline before refinement.

---

### 🔄 <span style="color:#ff7b72;">Step 3 — Cross-Validation for Hyperparameter Tuning</span>

Use **k-fold cross-validation** on training data.

Tune:

1. <span style="color:#d2a8ff;">Regularization strength λ</span>
2. <span style="color:#d2a8ff;">Model complexity (degree)</span>

```text
1️⃣  Split training set into k folds (k = 5)
2️⃣  Train on k−1 folds, validate on 1 fold
3️⃣  Compute average validation error
```

**Output:** best combination (e.g., λ = 0.1, degree = 3).

---

### 🧪 <span style="color:#a5d6ff;">Step 4 — Validate on Validation Set</span>

| Case                                                           | Symptom                                      | Fix                              |
| :------------------------------------------------------------- | :------------------------------------------- | :------------------------------- |
| ⚠️ <span style="color:#ff7b72;">High Bias (Underfit)</span>    | High training & validation errors            | ↑ degree / add features          |
| ⚠️ <span style="color:#79c0ff;">High Variance (Overfit)</span> | Low training error but high validation error | ↑ λ / ↓ degree / remove features |

> 🔧 *Minor Adjustments:*
>
> * Decrease λ slightly → bias fix
> * Increase λ slightly → variance fix
>   If no improvement → Step 5.

---

### 🧱 <span style="color:#ff7b72;">Step 5 — Major Adjustments</span>

#### 5.1 🔧 Large λ Changes

* High bias → drastically lower λ
* High variance → drastically raise λ
* Re-run cross-validation (Step 3 → 4)

#### 5.2 📉 Optimize Training Set Size

If only variance high:
Plot training vs validation error over increasing data sizes.

* 🧨 *Large gap* → add data (70 : 10 : 20)
* 🔹 *Small gap* → move to feature optimization

#### 5.3 🧠 Optimize Features

| Type          | Strategy                            |
| :------------ | :---------------------------------- |
| High Bias     | Add interaction/polynomial features |
| High Variance | Remove redundant features           |

Then redo Steps 3–4.

---

### 🧾 <span style="color:#56d364;">Step 6 — Evaluate on Test Set</span>

If failure → report cause.
Else:

```text
Train on (Training + Validation)
Evaluate final performance on Test Set
```

---

## 🧮 <span style="color:#a5d6ff;">Notes — Linear Regression Variants</span>

### 1️⃣ <span style="color:#79c0ff;">Ridge / Tikhonov Regression</span>

[
||\theta X − y||_2^2 + ||M \theta||_2^2
]
If ( M = \alpha I ) → standard L2 regularization.

> 🧩 Adds stability against multicollinearity.

---

### 2️⃣ <span style="color:#ff7b72;">Lasso Regression</span>

[
||\theta X − y||_2^2 + \alpha ||\theta||_1
]

> ⚡ Encourages sparse feature weights.

---

### 3️⃣ <span style="color:#d2a8ff;">Polynomial Regression</span>

[
y = \sum_i β_i X'(x_i), \quad X'(x_i) = [1, x_i, x_i^2, …, x_i^m]^T
]

> 🎢 Nonlinear extension with univariate polynomial terms (no cross terms).
