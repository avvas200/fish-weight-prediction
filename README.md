# Predicting Fish Weight from Body Measurements

> A comparison of linear and non-linear regression models on the Fish Market dataset (159 samples, 6 features + species). Motivated by the physical prior that fish weight should scale with length³.

![Python](https://img.shields.io/badge/python-3.10-blue)
![scikit--learn](https://img.shields.io/badge/scikit--learn-1.x-orange)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 📌 Overview

**Problem.** Given physical measurements of a fish (species and five body dimensions), predict its weight in grams.

**Approach.** After establishing two baselines (a mean predictor and the naive univariate linear regression used in the original tutorial), I compared five regression models — multivariate linear, Ridge, Lasso, polynomial features + Ridge, and Random Forest — using 5-fold cross-validation and residual diagnostics.

**Key result.** *TODO — fill in after running the notebook. Example: "Random Forest achieved test R² = 0.97, RMSE = 63 g, improving on the univariate baseline (R² = 0.83, RMSE = 145 g) by using all measurements plus species information."*

---

## 🧠 Motivation

An object's mass equals its volume × density. Volume scales with length³, so from first principles we expect **Weight ≈ k · Length³** for a fish of roughly constant density. This gives us a testable physical prior:

- A single-feature *linear* model should systematically under-predict for the largest fish and over-predict for the smallest.
- The slope of `log(Weight)` vs `log(Length)` should be close to 3.
- Adding polynomial features or using a non-linear model should meaningfully improve fit.

The project tests each of these predictions empirically.

---

## 📊 Dataset

- **Source:** [Fish Market dataset](https://www.kaggle.com/datasets/aungpyaeap/fish-market), Aung Pyae, Kaggle.
- **Size:** 159 samples across 7 species.
- **Target:** `Weight` (grams).
- **Features:** `Species` (categorical), `Length1`, `Length2`, `Length3`, `Height`, `Width` (all in cm).
- **License:** CC0 (public domain).

---

## 🛠️ Methods

- **Preprocessing.** One-hot encoded species (7 categories → 6 dummy features). Dropped rows with `Weight == 0`. Standardized features for regularized models.
- **Baselines.**
  1. Mean predictor (`DummyRegressor`).
  2. Univariate linear regression on `Length1` only (matches the original tutorial).
- **Candidate models.** Multivariate linear regression, Ridge (α=1), Lasso (α=1), polynomial features (degree=2) + Ridge, Random Forest (200 trees).
- **Evaluation.** 80/20 train/test split with `random_state=42`, plus 5-fold cross-validation on the best model. Metrics: R², RMSE, MAE.
- **Diagnostics.** Predicted-vs-actual plot, residuals-vs-predicted plot, residual distribution, and Random Forest feature importance.

---

## 📈 Results

*TODO — replace this table with your actual numbers after running the notebook.*

| Model | Test R² | RMSE (g) | MAE (g) |
|---|---|---|---|
| Mean baseline | 0.00 | — | — |
| Linear (Length1 only) | 0.83 | — | — |
| Linear (all features) | — | — | — |
| Ridge | — | — | — |
| Lasso | — | — | — |
| Polynomial (deg=2) + Ridge | — | — | — |
| **Random Forest** | — | — | — |

**Key finding from log-log plot:** the fitted slope of `log(Weight)` vs `log(Length)` was *TODO*, which is *TODO — close to / far from* the theoretical value of 3.

*(Add screenshots of your key plots here as `figures/residuals.png`, `figures/comparison.png`, etc.)*

---

## 🔁 Reproducibility

1. Download `Fish.csv` from [Kaggle](https://www.kaggle.com/datasets/aungpyaeap/fish-market) and place it in a `data/` folder (or update `DATA_PATH` in the notebook).
2. Open `Fish_Weight_Regression.ipynb` in Google Colab or a local Jupyter environment.
3. Run all cells top to bottom. Random seeds are fixed (`SEED = 42`).

**Requirements:** `numpy`, `pandas`, `matplotlib`, `seaborn`, `scikit-learn`.

---

## 🚧 Limitations and future work

- **Small sample size** (~159 rows) — the CV standard deviation gives a realistic sense of uncertainty; single point estimates should not be over-interpreted.
- **No hyperparameter tuning.** A `GridSearchCV` sweep over Ridge `alpha`, Random Forest `n_estimators` and `max_depth` would likely improve results.
- **Heteroscedasticity.** The residuals likely grow with predicted weight; a log-transformed target would give more uniform error and match the physical scaling.
- **Physics-informed feature engineering.** Explicitly fitting the power law `log(Weight) = a + b·log(Length)` gives an interpretable exponent that can be compared to the theoretical 3.
- **Generalization.** The model is trained on 7 species and will not extrapolate to unseen species.

---

## 📚 References

1. Fish Market dataset — Aung Pyae, Kaggle. [https://www.kaggle.com/datasets/aungpyaeap/fish-market](https://www.kaggle.com/datasets/aungpyaeap/fish-market)
2. Hastie, T., Tibshirani, R., & Friedman, J. (2009). *The Elements of Statistical Learning* (2nd ed.). Springer. — Chapter 3 (linear methods) and Chapter 15 (random forests).

---

## 👤 Author

**Your Full Name**
- 🎓 [Your affiliation / current institution]
- 🌐 [Personal website] · [Google Scholar] · [LinkedIn]
- ✉️ your.email@example.com

If you find this useful, please star the repo ⭐

---

## 📄 License

MIT License — see [`LICENSE`](LICENSE) for details.
