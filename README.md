# `fpqr` package

## Introduction

`fpqr` is a Python package that solves fast partial quantile regression (fPQR) models. The fpqr is a new methodology suitable for solving high dimensional regression problems where the response can be either a vector or a full  matrix (this means that the response can have more than one dimension). Also, this methodology can deal with colinearity and outliers. It can be seen as an extension of partial least squares (PLS) to the quantile regression framework, as it shares some of the nice properties of PLS: it is a dimension reduction technique that obtains uncorrelated scores maximizing a quantile covariance between predictors and responses. But oposed to PLS fPQR is based on quantile regression, which makes it a robust, quantile based methodology suitable for dealing with outliers, heteroscedastic or heavy tailed datasets. The median estimator of the fPQR algorithm is a robust alternative to PLS, while other quantile levels can be computed and can provide additional information on the tails of the responses. A full description of the methodology can be seen in [this paper](https://www.sciencedirect.com/science/article/pii/S0169743922000442).

The current version of the package supports the computation of the fPQR algorithm based on three quantile metrics denoted here as 'li', 'dodge' and 'choi' (based on the main authors of the papers where the metrics were proposed). The best results both in terms of prediction and computation time are generally obtained with the 'li' metric, which is the default value.

## Requirements 
The package makes use of some basic functions from `scikit-learn` `numpy` and `asgl`.

## Usage example:
In the following example we will solve a synthetic dataset where the response is multidimensional.

```
import fpqr
from sklearn.datasets import make_regression

# Generate a dataset with 1000 observations, 10 predictive variables and 2 response variables.
x, y, true_beta = make_regression(n_samples=1000, n_features=10, n_informative=10, n_targets=2,
                                  bias=10.0, noise=2.0, shuffle=True, coef=True, random_state=None)

fpqr_li = fpqr.FPQRegression(quantile=0.5, n_components=3, metric='li')
fpqr_li.fit(x, y)

print(fpqr_li.coef_)
print(fpqr_li.intercept_)

predictions = fpqr_li.predict(x)
```

### Citing
___
If you use fPQR for academic work, we encourage you to [cite our paper](https://www.sciencedirect.com/science/article/pii/S0169743922000442). Thank you for your support and we hope you find this package useful!
