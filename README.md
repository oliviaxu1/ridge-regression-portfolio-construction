# Portfolio Return Prediction and Construction with Ridge Regression

A rolling-window machine-learning framework for predicting stock returns from financial characteristics and translating those predictions into portfolios.

## Overview

This project examines how Ridge regularisation affects out-of-sample return forecasts and the risk-adjusted performance of prediction-weighted portfolios. Models are trained on the previous three years of observations, used to forecast the following 12 months, and retrained annually across 11 regularisation strengths.

The analysis separates two concepts:

- **Realised performance:** prediction-derived weights multiplied by subsequent realised returns.
- **Model-implied expected performance:** the same weights multiplied by predicted returns.

The central finding is that the regularisation strength that appears strongest ex ante is not the one that performs best ex post.

## Methodology

1. Examine time-varying correlations among book leverage, momentum and market beta.
2. Remove characteristics with at least 25% missing observations.
3. Standardise retained characteristics and replace remaining missing values with zero.
4. Estimate Ridge regression models using rolling three-year training windows.
5. Predict the following 12 months and retrain annually.
6. Evaluate 11 values of $\alpha$ from $10^{-5}$ to $10^5$.
7. Use predicted returns as portfolio weights.
8. Compare annualised realised and model-implied expected Sharpe ratios.

## Portfolio Construction

For firm $i$ in month $t$, the predicted return is used as the portfolio signal:

$$w_{i,t}(\alpha)=\hat r_{i,t}(\alpha).$$

The realised portfolio return is:

$$r^{\mathrm{realised}}_{p,t+1}=\sum_i w_{i,t}r_{i,t+1},$$

while the model-implied expected return is:

$$r^{\mathrm{expected}}_{p,t+1}=\sum_i w_{i,t}\hat r_{i,t}=\sum_i \hat r_{i,t}^{2}.$$

These are signal portfolios rather than constrained, fully invested long-only portfolios.

## Key Results

The archived course run produced:

| Evaluation criterion | Selected alpha | Annualised Sharpe ratio |
|---|---:|---:|
| Best realised performance | 1,000 | 0.309 |
| Best model-implied expected performance | 100,000 | 2.754 |

Moderate regularisation produced the strongest realised risk-adjusted performance, while much stronger regularisation produced the highest model-implied expected Sharpe ratio. This divergence highlights the difference between model confidence and realised investment outcomes.

For the expected-versus-realised comparison, the notebook fixes the expected-Sharpe winner, $\alpha=100{,}000$, and uses the same prediction-derived weights for both return series. This makes the comparison apples-to-apples.

## Data

The original dataset contains monthly firm-level financial characteristics and forward returns covering approximately 1970–2000. It was supplied through a restricted University of Melbourne course environment and is not redistributed here.

Authorised users can place the source file at:

```text
data/raw/factor_and_ret_oos.csv
```

See [`data/README.md`](data/README.md) for the required structure. Do not commit the raw dataset to a public repository.

## Repository Structure

```text
ridge-regression-portfolio-construction/
├── README.md
├── portfolio_analysis.ipynb
├── requirements.txt
├── data/
│   └── README.md
└── figures/
    └── README.md
```

## Running the Notebook

Create a Python environment and install the dependencies:

```bash
pip install -r requirements.txt
jupyter notebook portfolio_analysis.ipynb
```

The notebook will explain how to supply an authorised data copy if the expected file is missing.

## Technologies

Python, pandas, NumPy, scikit-learn, Matplotlib, seaborn and Jupyter.

## Limitations

- The restricted source data are not included, so full reproduction requires authorised access.
- The analysis does not incorporate transaction costs, turnover limits, leverage constraints or a risk-free rate.
- Raw prediction signals are used as weights and are not normalised to sum to one.
- Global feature standardisation preserves the original analytical convention; a production system should estimate transformations within each training window.
- Results are historical and sample-specific and should not be interpreted as investment advice.

## Academic Context

This project is a portfolio adaptation of graduate coursework completed in Applied Machine Learning in Finance at the University of Melbourne. It has been independently reorganised and revised for public presentation. Course materials and restricted data are not included.

## Author

Olivia Xu — [GitHub profile](https://github.com/oliviaxu1)

