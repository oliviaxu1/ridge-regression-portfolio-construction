# Portfolio Return Prediction and Construction with Ridge Regression

A rolling-window machine-learning framework for predicting stock returns from financial characteristics and evaluating prediction-based portfolio signals.

## Overview

This project examines how Ridge regularisation affects out-of-sample return forecasts and the risk-adjusted performance of prediction-based signal portfolios. Models are estimated using rolling three-year training windows, used to predict the following 12 months, and retrained annually across 11 regularisation strengths from 10⁻⁵ to 10⁵.

Predicted returns are used directly as unnormalised portfolio signals. The analysis evaluates both realised performance and model-implied expected performance.

## Methodology

- Rolling correlations among book leverage, momentum and market beta
- Missing-value filtering and feature standardisation
- Ridge regression across 11 regularisation strengths
- Three-year rolling training windows with annual retraining
- Prediction-based signal construction
- Annualised realised and model-implied expected Sharpe ratios
- Expected-versus-realised comparison using the same alpha and signals

See [`portfolio_analysis.ipynb`](portfolio_analysis.ipynb) for the complete methodology, code and results.

## Key Results

| Evaluation criterion | Selected α | Annualised Sharpe ratio |
|---|---:|---:|
| Best realised performance | 1,000 | 0.309 |
| Best model-implied expected performance | 100,000 | 2.754 |

The regularisation strength favoured by the model's ex-ante assessment differed from the one that produced the strongest ex-post performance.

For an apples-to-apples comparison, the notebook fixes α = 100,000 and uses the same prediction-derived signals for both series. At this alpha, the model-implied expected Sharpe ratio is 2.754, while the realised Sharpe ratio is 0.108.

## Data

The dataset was provided through the University of Melbourne course environment. The raw data are not included in this repository.

Users with an authorised copy can place the source file at:

```text
data/raw/factor_and_ret_oos.csv
```

See [`data/README.md`](data/README.md) for the expected fields.

## Running the Notebook

```bash
pip install -r requirements.txt
jupyter notebook portfolio_analysis.ipynb
```

## Limitations

The analysis uses unnormalised prediction signals and does not incorporate transaction costs, turnover limits, leverage constraints or a risk-free rate. Feature standardisation follows the original full-sample analytical setup; a stricter out-of-sample design would estimate the transformation within each training window.

Results are historical and sample-specific and should not be interpreted as investment advice.

## Academic Context

This repository is a public portfolio adaptation of graduate coursework completed in *Applied Machine Learning in Finance* at the University of Melbourne. It has been reorganised and revised for public presentation.
