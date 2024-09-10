## Model fitting: Scikit-learn

1. Regression
```
from sklearn import linear_model
from sklearn.ensemble import AdaBoostRegressor

# OLS
regr = linear_model.LinearRegression(fit_intercept=True)
# Lasso
regr = linear_model.Lasso(alpha=2*sigma/n)    # alpha is lambda
# CV Lasso
regr = linear_model.LassoCV(cv=5, random_state=0)
# ridge
regr = linear_model.Ridge(alpha=1.0)
# CV ridge
regr = linear_model.RidgeCV(cv=5)

# AdaBoost
regr = AdaBoostRegressor()

# model fitting
regr.fit(X, y)  # X: 2d array or df; y: 1d array or Series

# for linear models
regr.coef_    # numpy array of X coefficients
regr.intercept_    # intercept

# prediction
predicted = regr.predict(new_X)
```
2. Classification
```
from sklearn import linear_model
from sklearn.ensemble import AdaBoostClassifier

# logistic regression
regr = linear_model.LogisticRegression(
	penalty = 'l2',    # regularization, {‘l1’, ‘l2’, ‘elasticnet’, None}
	C = 1,             # regularization coefficient/strength is 1/C
	fit_intercept=True
)
# AdaBoost
regr = AdaBoostClassifier()

# model fitting
regr.fit(X, y)  # X: 2d array or df; y: 1d array or Series

# for linear model (logistic regression)
regr.coef_    # numpy array of X coefficients
regr.intercept_    # intercept

# prediction: probability of y=1
predicted = regr.predict_proba(new_X)[:, 1]    # [:, 1] is array of Prob(y=1)
```
## Statistical test: statsmodels
```
import numpy as np
import statsmodels.api as sm

# OLS
model = sm.OLS(y, sm.add_constant(X))    # X: 2d array or df; y: 1d array or Series
# logistic regression
model = sm.Logit(y, sm.add_constant(X))

# model fitting
model_fit = model.fit()  

# results    note the first value corresponds to the intercept
cov = model_fit.cov_params()
std_err = np.sqrt(np.diag(cov))
z_values = model_fit.params / std_err
p_values = model_fit.pvalues

# for OLS only
model_fit.ssr    # RSS

# summary
model_fit.summary()
```
