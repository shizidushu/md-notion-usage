## The Variance-Bias Trade-off

The MSE can be decomposed into more specific pieces. Formally, the MSE of a *model* is

$$\mathrm{MSE}=\frac{1}{n}\sum_{n=1}^n(y_i - \hat{y}_i)^2,$$

where $y_i$ is the outcome and $\hat{y}_i$ is the model prediction of that sample's outcome.


### Linear Models and Least Squares

test $\hat{Y} = \hat{\beta}_0 + \sum_{j=1}^p X_j \hat{\beta}_j$  test

Given a vector of inputs $X^T=(X_1, X_2, \ldots, X_p)$, we predict output $Y$ via the model
$$
\hat{Y} = \hat{\beta}_0 + \sum_{j=1}^p X_j \hat{\beta}_j
$$
The term $\hat{\beta}_0$ is the intercept, also known as the *bias* in machine learning. Often it is convenient to include the constant variable 1 in $X$, include $\hat{\beta_0}$ in the vector of coefficients $\hat{\beta}$, and then write the linear model in vector form as an inner product
$$
\hat{Y} = X^T \hat{\beta}
$$
where $X^T$ denotes vector or matrix transpose ($X$ being a column vector).