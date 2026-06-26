---
name: data-science
description: Data science methodology — EDA, feature engineering, model selection, evaluation metrics, and production ML patterns.
---

# Data Science Skill

## Exploratory Data Analysis (EDA) Checklist
Every dataset should go through:
1. **Shape & Types**: rows, columns, dtypes — flag unexpected types
2. **Missing Values**: count, percentage, pattern (MCAR / MAR / MNAR)
3. **Distributions**: histogram for numeric, bar chart for categorical
4. **Outliers**: IQR method (Q1 - 1.5×IQR, Q3 + 1.5×IQR), Z-score > 3
5. **Correlations**: Pearson for numeric, Cramér's V for categorical
6. **Target Leakage**: features that could not be known at prediction time

## Feature Engineering Patterns
- **Numeric**: log-transform skewed features, standardise (μ=0, σ=1), bin into quantiles
- **Categorical**: one-hot encode (low cardinality), target encode (high cardinality), embeddings
- **Temporal**: extract hour/day/month/year, encode cyclically (sin/cos for hour, day-of-week)
- **Text**: TF-IDF for sparse, sentence embeddings for semantic tasks
- **Interactions**: multiply correlated features, polynomial features for nonlinear boundaries

## Model Selection Guide
| Problem Type    | Try First          | Also Consider              |
|-----------------|-------------------|---------------------------|
| Classification  | XGBoost / LightGBM | Logistic Regression, RF  |
| Regression      | XGBoost / LightGBM | Ridge, ElasticNet, SVR   |
| Time Series     | Prophet, ARIMA     | LSTM, N-BEATS, TFT       |
| Clustering      | K-Means            | DBSCAN, Hierarchical     |
| NLP             | Fine-tuned LLM     | TF-IDF + LR, FastText    |
| Recommendation  | Matrix Factorisation | Neural CF, Two-Tower    |

## Evaluation Metrics — Which One to Use
- **Classification (balanced)**: F1-Score, AUC-ROC
- **Classification (imbalanced)**: Precision-Recall AUC, F1
- **Regression**: RMSE (penalises large errors), MAE (robust to outliers), MAPE
- **Ranking**: NDCG, MAP, MRR
- **Clustering**: Silhouette Score, Davies-Bouldin

## Production ML Checklist
Before shipping a model:
- [ ] Train/validation/test split is time-based for temporal data
- [ ] No data leakage between folds
- [ ] Baseline model established (random, majority class, mean predictor)
- [ ] Calibration check for probability outputs
- [ ] Feature importance documented
- [ ] Monitoring plan: data drift (PSI), concept drift, latency SLA
- [ ] Rollback strategy defined

## Common Pitfalls to Flag
- Data leakage: using future information during training
- Class imbalance not addressed
- Feature scaling applied before train/test split (causes leakage)
- Evaluating on training set only
- Ignoring class weights for imbalanced targets
- Not baseline benchmarking before complex models
